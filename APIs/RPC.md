The conceptualization of RPC (Remote Procedure Call) wasn't a sudden "Eureka!" moment but a gradual evolution of ideas to solve a fundamental problem: **making communication between programs on different machines look and feel as simple as calling a function in your own program.**

Here’s a breakdown of how it was conceptualized, from the core idea to its deep implementation principles.

### 1. The Foundational Problem: The Complexity of Networks

In the early days of networking, programs communicated using explicit, low-level socket programming. To request a service from another machine (a "server"), a client program had to:

1. **Create a socket.**
    
2. **Manage the connection** (handshake, etc.).
    
3. **Serialize** its request data into a raw byte stream (a very error-prone process).
    
4. **Send** the bytes over the network.
    
5. **Wait** for a response.
    
6. **Deserialize** the response byte stream back into meaningful data.
    
7. **Handle** all possible errors: network failures, timeouts, server crashes, etc.
    

This was complex, tedious, and not reusable. Developers wanted to abstract this away.

### 2. The Core Conceptual Leap: Abstraction

The key conceptual leap of RPC is **abstraction through language-level semantics**. The goal was to make a network call **look identical** to a local call. The idea was:

> "Why can't I just call a function like `result = getEmployeeDetails(employee_id)`, and have the system automatically handle the fact that the `getEmployeeDetails` function's code is running on a machine across the country?"

This abstraction is powerful because it:

- **Hides complexity:** The programmer doesn't think about sockets or byte streams.
    
- **Promotes modularity:** Services can be developed and updated independently.
    
- **Leverages existing skills:** Programmers already know how to call functions.
    

### 3. The "Deep" Conceptual Architecture: The RPC Model

To make this abstraction work, a specific model was conceptualized. This model involves several key components that work together to create the illusion of a local call.

![[Pasted image 20250904114334.png]]

The client code makes a call to what it believes is a local function. In reality, it's calling a **Client Stub** (a proxy generated automatically by the RPC system).

**On the Client Side:**

1. **The Client Stub** takes the function arguments and **marshals** (or serializes) them into a standardized, flat byte stream suitable for network transmission. This involves handling different data representations (e.g., big-endian vs. little-endian numbers).
    
2. The stub uses the underlying RPC runtime to **transport** this message packet to the remote server machine. It blocks the client thread and waits for a response.
    

**On the Server Side:**  
3. A **Server Stub** (or skeleton) is listening on the network. It **unmarshals** (deserializes) the incoming byte stream back into meaningful data structures in the server's memory.  
4. The server stub makes a **local call** to the actual server function (`getEmployeeDetails`) and passes it the unmarshalled arguments.  
5. The server function runs exactly as if it were called locally and returns a result.

**The Process Repeats in Reverse:**  
6. The Server Stub **marshals** the return value (or any error) into a network message.  
7. It sends the response packet back to the client machine.  
8. The Client Stub **unmarshals** the response.  
9. The client stub returns the value to the original client code, which wakes up and continues execution, completely unaware of the network journey.

### 4. Key Deep Technical Challenges & Solutions

Conceptualizing the model was one thing; making it work robustly in the real world required solving deep technical challenges:

- **Binding:** How does the client know which server to talk to? This led to the concept of a **Name Service** or **Directory Service**. Servers register their availability with this service, and clients consult it to find a server's network address.
    
- **Parameter Passing:** How do you pass complex data types (e.g., structs, objects, pointers)? The solution was a strict **Interface Definition Language (IDL)**. Developers define the function signatures and data types in this neutral language. Tools then **generate the client and server stubs** automatically in the target programming language, handling all the marshaling/unmarshaling logic.
    
- **Semantics of Failure:** A local call either works or your program crashes. A remote call can fail in many new ways. This forced a deep conceptualization of different failure modes:
    
    - **At-Least-Once:** The RPC system might retry on failure, risking the operation being executed multiple times. (Okay for `read()`, bad for `transferMoney()`).
        
    - **At-Most-Once:** The system ensures a request is executed only once, even if retries happen. This is much harder to implement.
        
    - **Maybe:** No guarantees; the client simply doesn't know what happened. (Simplest but least useful).
        
- **Performance:** The overhead of marshaling and network travel is immense compared to a local call. This drove the need for highly efficient serialization protocols (like Protocol Buffers, Message Pack, Avro).



























































### The Real-World Example: Google Search

Imagine you enter a search query, "best hiking trails near me," into Google. This single request does not get answered by one single server. It triggers a cascade of hundreds of **microservices** communicating with each other through RPC to compose the results page you see.

Here’s how RPC works at a production level in this scenario:

---

### 1. The Components (Microservices)

A single Google Search request interacts with dozens of specialized services, each responsible for a piece of the puzzle:

- **Web Search:** Finds relevant web pages.
    
- **Spell Checker ("Did you mean...?"):** Checks your query spelling.
    
- **Local Search:** Finds "near me" results.
    
- **Image Search:** Prepares image results.
    
- **Ads Service:** Selects and retrieves relevant advertisements.
    
- **User Profiling Service** (anonymized): Personalizes results based on past behavior.
    
- **Feature Flag Service:** Determines if you're in an A/B test group for a new feature.
    

### 2. The RPC Call in Action

Let's zoom in on the **Spell Checker** service.

1. **The Client:** The main "Search Frontend" service receives your query `"best hikng trails"` (note the typo). It determines that it needs to call the Spell Checker service.
    
2. **The Stub & Marshaling:**
    
    - The Search Frontend doesn't know how to talk to the Spell Checker directly. Instead, it has a **client stub** for the Spell Checker's interface. This stub was automatically generated from a **Protocol Buffer (protobuf) `.proto` file**.
        
    - The `.proto` file is the **Interface Definition Language (IDL)**. It defines the contract:
    
```message SpellCheckRequest {
  string query = 1;
  string user_language_code = 2;
}

message SpellCheckResponse {
  string corrected_query = 1;
  double confidence_score = 2;
}

service SpellCheckerService {
  rpc CorrectSpelling(SpellCheckRequest) returns (SpellCheckResponse);
}
```
1. - The Search Frontend code calls the stub method: `CorrectSpelling("best hikng trails", "en")`. This looks and feels like a local function call.
        
    - The **client stub** takes the `SpellCheckRequest` object and **marshals** it—serializing it into a highly efficient, compact binary format using the protobuf protocol.
        
2. **Network Communication:**
    
    - The marshaled binary packet is sent over the network via **gRPC** (Google's high-performance open-source RPC framework), which runs on HTTP/2.
        
    - **Service Discovery:** The client stub doesn't have a hardcoded server IP. It asks a central **service discovery** system (like Google's internal systems or, in the open-source world, **Consul** or **etcd**): "Where can I find an available instance of `SpellCheckerService`?" It gets back a list of healthy servers and connects to one.
        
3. **On the Server Side:**
    
    - A **server stub** (skeleton) on a Spell Checker server is listening for incoming gRPC requests on an HTTP/2 port.
        
    - It **unmarshals** the binary packet, reconstructing a perfect `SpellCheckRequest` object in the server's memory.
        
    - It then calls the **actual business logic**—the `CorrectSpelling` method in the Spell Checker's code, passing the request object. This method runs its complex machine learning models to determine that "hikng" is likely "hiking".
        
4. **The Return Journey:**
    
    - The server code returns a `SpellCheckResponse` object with `corrected_query: "best hiking trails"`.
        
    - The **server stub** marshals this response object back into a binary packet.
        
    - The gRPC runtime sends the packet back over the network to the waiting Search Frontend.
        
5. **Resuming the Client:**
    
    - The **client stub** unmarshals the response binary into a `SpellCheckResponse` object.
        
    - The original function call in the Search Frontend code now returns, providing the corrected query. The programmer who wrote the Search Frontend code has no idea about the network call; they just have the result.
        

### Why This is "Production Level": Key Characteristics

This isn't a academic exercise; it's engineering built for scale, reliability, and performance.

- **Performance:** gRPC uses **HTTP/2** for multiplexing (multiple calls over one connection), protobuf for **binary serialization** (smaller/faster than JSON/XML), and is built for low latency.
    
- **Scalability:** The Client Stub queries a **service discovery** system. This allows the Spell Checker service to have thousands of instances running globally. The system can load balance requests and automatically route traffic away from failed instances.
    
- **Robustness & Observability:**
    
    - **Deadlines/Timeouts:** The client sets a deadline (e.g., 100ms). If the Spell Checker doesn't respond in time, the RPC is canceled to prevent cascading failures.
        
    - **Retries:** The client can be configured to safely retry failed requests (e.g., for transient network errors).
        
    - **Monitoring:** Every single RPC is automatically traced and monitored. Google can see a detailed trace of the entire search request, showing how long each internal RPC (to spell check, ads, web search, etc.) took. Tools like **OpenTelemetry** and **Jaeger** bring this capability to the open-source world.
        
- **Polyglotism:** The Search Frontend might be written in C++, the Spell Checker in Python for its data science libraries, and the Ads service in Java. Because the interface is defined in the language-neutral protobuf IDL, all these services can communicate seamlessly. The RPC framework generates the correct stubs for each language.
    
- **Security:** In a modern production environment, these RPCs are authenticated and encrypted (using TLS/mTLS) so that only authorized services can talk to each other.









### 1. How the `.proto` File is Written

The `.proto` file is written in **Protocol Buffer Language**. It's not a programming language; it's an **Interface Definition Language (IDL)**. Its purpose is to define the contract between the client and server: what services are available, what methods they have, and what messages (data structures) are passed back and forth.

Here’s a concrete example for a simple user authentication service:

protobuf
```

// 1. Declate the syntax version. Always use proto3 for new projects.
syntax = "proto3";

// 2. Optional: Define the package name for namespace handling.
// This helps prevent naming conflicts between different projects.
package auth;

// 3. Optional: Define a Go package option (language-specific options exist).
option go_package = "github.com/yourproject/gen/auth";

// 4. Define the Messages (data structures/objects).
// This is like defining a class in Java or a struct in Go/C++.

message LoginRequest {
  string username = 1;  // Field Type | Field Name | Field Number
  string password = 2;
  // Field numbers are unique identifiers used in the binary encoding.
  // They are more efficient than using the field name.
}

message LoginResponse {
  string user_id = 1;
  string auth_token = 2;
  int64 token_expires_at = 3; // A Unix timestamp
}

message UserProfileRequest {
  string user_id = 1;
}

message UserProfile {
  string user_id = 1;
  string username = 2;
  string email = 3;
}

// 5. Define the Service (the API interface).
// This is like defining an interface in Java or an abstract class.
service AuthService {
  // Simple RPC: client sends a request, waits for a single response.
  rpc Login(LoginRequest) returns (LoginResponse) {};

  // Server-side streaming RPC: client gets a stream to read a sequence of messages.
  // Useful for getting ongoing updates or a large chunk of data broken into parts.
  rpc StreamUserProfileUpdates(UserProfileRequest) returns (stream UserProfile) {};

  // Client-side streaming RPC: client sends a stream of requests.
  // Useful for uploading large data or batched inputs.
  rpc UpdateProfile(stream UserProfile) returns (UserProfile) {};

  // Bidirectional streaming RPC: both sides send a stream of messages.
  // Useful for a live chat or a complex negotiation.
  rpc LiveChat(stream ChatMessage) returns (stream ChatMessage) {};
}
```
**Key Points:**

- **Messages** are your data transfer objects (DTOs).
    
- **Services** are your APIs. Each `rpc` keyword defines a remote method.
    
- **Streaming** keywords (`stream`) enable more complex communication patterns beyond simple request-response.
    

---

### 2. How the Stub is Defined: gRPC vs. Writing Your Own

This is the crucial part of your question.

#### **Is the stub defined by gRPC?**

**Yes, absolutely.** This is the primary job of the gRPC framework.

You **do not write the stub yourself**. Instead, you use the `protoc` (Protocol Buffer Compiler) tool with the gRPC plugin for your chosen language.

**The Process:**

1. **You write** the `.proto` file (as shown above).
    
2. **You run** the `protoc` compiler on that file.
    
3. **`protoc` + the gRPC plugin generate** the code for you in your target language (Go, Python, Java, etc.).
    

This generated code contains:

- **Client Stubs:** Classes that implement the service interface defined in your `.proto` file. Your application code calls methods on these classes. They handle all the marshaling, networking, and unmarshaling transparently.
    
- **Server Stubs (or Skeletons):** Abstract classes that _you_ must extend. They provide the boilerplate code for unmarshaling the incoming request, marshaling the outgoing response, and then calling the actual method that you, the programmer, will write.
    

#### **Can we write our own stub?**

**Theoretically, yes. Practically, you almost never should.**

**Why you _could_:**  
The `.proto` file is just a contract. The protocol (how data is encoded over the wire) is open and well-documented. You could, in theory, write your own code generator that reads a `.proto` file and outputs client and server code in a language that gRPC doesn't officially support. This is how the gRPC ecosystem expands.

**Why you _shouldn't_ (for your own application):**

1. **It's Incredibly Complex:** You would have to perfectly implement the Protobuf binary encoding/decoding (marshaling/serialization), which is a non-trivial task.
    
2. **You'd Have to Implement the gRPC-over-HTTP/2 Protocol:** This includes managing HTTP/2 connections, frames, headers, and all the complex state management that comes with it.
    
3. **You Lose All Tooling:** The entire ecosystem of gRPC tools (debuggers, health checks, load balancers, interceptors) would not work with your custom implementation.
    
4. **It's a Maintenance Nightmare:** You would be responsible for maintaining your custom RPC framework forever, fixing its bugs, and keeping up with any changes to the protocol. This is a massive undertaking.
    

### The Workflow in Practice

Here’s what you, the developer, actually do:

1. **Write:** `auth.proto`
    
2. **Generate:** Run a command like this to generate the stubs:
```
# Example for Go
protoc --go_out=. --go-grpc_out=. auth.proto

# Example for Python
protoc --python_out=. --grpc_python_out=. auth.proto

```

- This generates files like `auth.pb.go` (for Protobuf messages) and `auth_grpc.pb.go` (for gRPC services).
    
- **Implement the Server:** You write the "business logic" by creating a struct in Go (or a class in Python/Java) that **inherits from the generated server stub** and implements the actual methods.
    
    
```
// Go Example
type myAuthServer struct {
    pb.UnimplementedAuthServiceServer // This is the generated server stub
}

// You implement the Login method that was defined in the .proto file.
func (s *myAuthServer) Login(ctx context.Context, req *pb.LoginRequest) (*pb.LoginResponse, error) {
    // Your actual business logic here!
    // Check the database, validate credentials, create a token.
    if req.Username != "admin" || req.Password != "secret" {
        return nil, status.Error(codes.Unauthenticated, "bad credentials")
    }
    return &pb.LoginResponse{UserId: "123", AuthToken: "generated_jwt_token"}, nil
}
```

**Use the Client:** In your client application, you use the **generated client stub**.

```

go

// Go Client Example
func main() {
    conn, _ := grpc.Dial("localhost:8080", grpc.WithTransportCredentials(insecure.NewCredentials()))
    defer conn.Close()

    client := pb.NewAuthServiceClient(conn) // <-- This is the generated client stub

    // This call looks local but triggers the entire RPC process.
    response, err := client.Login(context.Background(), &pb.LoginRequest{
        Username: "admin",
        Password: "secret",
    })
}
```
**In summary: You define the contract in a `.proto` file. The gRPC tooling generates the stubs for you. You fill in the business logic on the server side and use the generated client to make calls.** Writing your own stub is an advanced, complex task reserved for extending the gRPC ecosystem to new languages, not for building everyday applications.