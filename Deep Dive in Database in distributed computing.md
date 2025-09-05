Databases are modular systems and consist of multiple parts: a transport layer accept‐
ing requests, a query processor determining the most efficient way to run queries, an
execution engine carrying out the operations, and a storage engine.




**Storage Engines**
Database management systems are applications built on top of storage engines, offering a
schema, a query language, indexing, transactions, and many other useful features.

To compare databases, it’s helpful to understand the use case in great detail and define
the current and anticipated variables, such as:
• Schema and record sizes
• Number of clients
• Types of queries and access patterns
• Rates of the read and write queries
• Expected changes in any of these variables
Knowing these variables can help to answer the following questions:
• Does the database support the required queries?
• Is this database able to handle the amount of data we’re planning to store?
• How many read and write operations can a single node handle?
• How many nodes should the system have?
• How do we expand the cluster given the expected growth rate?
• What is the maintenance process?

One of the popular tools used for benchmarking, performance evaluation, and com‐
parison is Yahoo! Cloud Serving Benchmark (YCSB) used for stress testing and benchmarking of independent database.


**Database management** can be used for multipurpose like for
- hot data(real time data) 
- cold data (long lived data) storage
- time series data storage
- complex analytical queries
- large blob(binary large object)
**DBMS are majorly divided into three categories**
	- online transactional processing databases
	- online analytical processing databases
	- hybrid combo of both
**Online transaction processing (OLTP) databases**
These handle a large number of user-facing requests and transactions. Queries
are often predefined and short-lived.
**Online analytical processing (OLAP) databases**
These handle complex aggregations. OLAP databases are often used for analytics
and data warehousing, and are capable of handling complex, long-running ad
hoc queries.
**Hybrid transactional and analytical processing (HTAP)**
These databases combine properties of both OLTP and OLAP stores.



**DBMS Architecture**
![[Pasted image 20250530110236.png]]

- when a req received in the form of query ,the query processor parse the query, interprets, and validate the query.
- later access controls are checks are performed after the query is interpreted.
- the parse query is passed to query optimizer which eliminates impossible and redundant  parts of the query and executes it based on  internal statistics (index cardinality, approximate intersection size, etc.) and data placement (which nodes in the cluster hold the data and the costs associated with its transfer).
- The optimizer handles both relational operations required for query resolution, usually presented as a dependency tree, and optimizations, such as index ordering, cardinality estimation, and choosing access methods.
- The query is usually presented in the form of an execution plan (or query plan): a
sequence of operations that have to be carried out for its results to be considered
complete
- The execution plan is handled by the execution engine, which collects the results of
the execution of local and remote operations. Remote execution can involve writing
and reading data to and from other nodes in the cluster, and replication.
- The execution plan is handled by the execution engine, which collects the results of
the execution of local and remote operations. Remote execution can involve writing
and reading data to and from other nodes in the cluster, and replication.
Local queries (coming directly from clients or from other nodes) are executed by the
storage engine. 

# Storage Engine
The storage engine has several components with dedicated
responsibilities:
### **1. Transaction Manager**

- **Function**: Ensures that transactions are **executed atomically**, **consistently**, **isolatedly**, and **durably**—commonly known as the **ACID properties**.
    
- **Goal**: Prevent the database from ending up in a **logically inconsistent state**, even in the case of failures (like crashes or power loss).
    
- **Example tasks**:
    
    - Coordinating commit and rollback operations
        
    - Handling concurrency and recovery
    
 ### **2. Lock Manager**

- **Function**: Manages **locks on database objects** (like rows, tables, or pages).
    
- **Goal**: Prevents **concurrent transactions** from violating the database’s **physical integrity** by controlling access.
    
- **Example tasks**:
    
    - Applying shared/exclusive locks
        
    - Detecting and resolving deadlocks
        

---

### **3. Access Methods (Storage Structures)**

- **Function**: Define how data is **physically organized and accessed** on disk.
    
- **Goal**: Support efficient storage and retrieval of data.
    
- **Common structures**:
    
    - **Heap files**: Unordered collections of records
        
    - **B-Trees**: Balanced tree structures for indexed access (used in many DBMSs)
        
    - **LSM Trees (Log-Structured Merge Trees)**: Efficient for write-heavy workloads
        

---

### **4. Buffer Manager**

- **Function**: Handles **caching of data pages in memory** to minimize expensive disk I/O.
    
- **Goal**: Improve **performance** by keeping frequently accessed data in RAM.
    
- **Responsibilities**:
    
    - Page replacement strategies (e.g., LRU)
        
    - Managing dirty pages (those modified in memory but not yet written to disk)
### 5.**Recovery Manager**

- **Function**: Ensures the database can **recover to a consistent state** after a failure (e.g., crash, power loss, or system error).
    
- **Goal**: Enforce the **Durability** and part of the **Atomicity** property from ACID.
    

---

### **Key Responsibilities:**

1. **Logging (Write-Ahead Logging - WAL)**
    
    - Every change is first recorded in a **log file** before it's applied to the database.
        
    - Logs are stored persistently to survive crashes.
        
2. **Checkpointing**
    
    - Periodically writes a snapshot of the current state to minimize recovery time.
        
    - Helps limit how much of the log needs to be replayed during recovery.
        
3. **Crash Recovery**
    
    - **Redo**: Re-applies committed transactions whose changes may not have made it to disk.
        
    - **Undo**: Reverts incomplete or uncommitted transactions.
        
4. **Coordination with Other Managers**
    
    - Works closely with the **Transaction Manager** and **Buffer Manager** to track and apply or roll back operations safely.
        

---

### **Example Scenario:**

Suppose a system crashes while a transaction was halfway through updating several records:

- The **recovery manager** examines the log.
    
- It identifies **committed** and **uncommitted** transactions.
    
- It **re-applies (redo)** committed transactions to ensure durability.
    
- It **reverses (undo)** uncommitted transactions to maintain consistency.
