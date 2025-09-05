![[jO3cAZZWn.png]]

**what happens at runtime**

![[Pasted image 20250425230623.png]]

- JIT compiler converts byte code to machine code


# Features
- Fully Object Oriented
- secure and robust
- Architecture neutral means it can be  run on any architecture(x86, x64,Apple M1)
- In built multithreaded
- high performance and efficient
- interpreted language
- simple and easy to learn



# C++ vs Java
| Feature              | C++                               | Java                                       |
| -------------------- | --------------------------------- | ------------------------------------------ |
| Platform             | Platform-dependent                | Platform-independent                       |
| Memory Management    | Manual (pointers used)            | Automatic (garbage collector)              |
| Multiple Inheritance | Supports multiple inheritance     | Does not support (uses interfaces instead) |
| Pointers             | Used                              | Not used                                   |
| Compilation          | Compiled directly to machine code | Compiled to bytecode for JVM               |
| Header files         | Uses header files                 | No header files, uses packages             |



### **1.3 Keywords, Tokens, Data Types**

#### **Keywords**

- Reserved words that have **special meaning** in Java.
- Examples: `class`, `public`, `static`, `void`, `if`, `else`, `return`, `int`, `new`, `try`, `catch`
#### **Tokens**
- Smallest unit of a Java program.

- Types of Tokens:
    - **Keywords**
    - **Identifiers** :Names used to identify variables, methods, classes.
    - **Literals**: Constants whose values do not change during program
		execution (e.g., 10, 'A', "hello")
    - **Operators** (e.g., +, -, *, /)
    - **Separators** (e.g., `;`, `()`, `{}`)

#### **Data Types**

- **Primitive types**: byte, short, int, long, float, double, Boolean, char
- **Non-primitive types**: Strings, Arrays, Classes

# Variable Scope
- **Local Variable**: A variable declared inside a method, constructor, or block
and accessible only within that block.
- **Global/ Instance Variable**: A variable declared at the class level, outside
of any method, block, or constructor. These are also called instance
variables because they belong to an object.
- static / Class Variable: A variable declared using the static keyword at
the class level. It is shared among all instances of the class.
# Note :Only static method can access static variable




# Packages
A **package** in Java is a way to group related classes and interfaces together. It helps to organize code in a better and cleaner way.

**Why are Packages Used?**

1. **Better Organization:**
    - Packages help to keep similar types of code together.
    - For example, all math-related classes can be in one package like `math`.
2. **Avoid Name Conflicts:**
    - Two classes with the same name can be placed in different packages.
    - For example, `java.util.Date` and `java.sql.Date` are different but allowed.
3. **Access Control:**
    - Packages help control who can use which class or method.
    - If we don’t want other classes to access something, we can keep it inside the same package with default access.
4. **Reusability:**
    - We can use the same package in different programs to avoid writing the same code again.




**How to Create a Package:**
We use the `package` keyword at the top of the Java file.
```
package mypackage;

public class MyClass {
    // code
}

```
**How to Use a Package**
We use the `import` keyword to use classes from another package.
```
import mypackage.MyClass;

public class Test {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
    }
}

```





**Access Specifiers
**
- **public**: Can be accessed from **anywhere** in the program.
- **private**: Can be accessed **only within the class**.
- **protected**: Can be accessed **within the same package** and **by subclasses**.

![[Pasted image 20250425235833.png]]

![[Pasted image 20250425234519.png]]

**POP vs OOP**
![[Pasted image 20250425235120.png]]

# Class

A class is a group of objects which have common properties. It is a template or blueprint from which objects are created

A class in Java can contain:
• Fields
•Methods
•Constructors
•Blocks (Instance Initialization Block (IIB), Static Initialization Block (SIB))
•Nested class and interface


**Method:** A **method** is a block of code that performs a task.



```
class Car {
    int speed;
    void drive() { -> this is method
        System.out.println("Car is running");
    }
}

```


**Types of classes** 

**Static Class:**

•Static keyword can be used with the inner class

•A static inner class is a nested class which is a static member of the outer class.

•It can be accessed without instantiating the outer class, using other static members.
- static class in java is created as a nested classes.
- static class cannot access non-static members of enclosing class
•Just like static members, a static nested class has not have access to the instance variables and methods of the outer class.

**Static member**
- static member belongs to the class not to object/instance of class
- static members shared among all the objects of the class(important point)
- static member initialized once and can be accessed without creating object of the class

**Java Inner Classes:**

•In Java, it is also possible to nest classes (a class within a class). The purpose of nested classes is to group classes that belong together, which makes your code more readable and maintainable.

•To access the inner class, create an object of the outer class, and then create an object of the inner class.

**Private Inner Class:**

•an inner class can be private or protected. If you don't want outside objects to access the inner class, declare the class as private.

**Static Inner Class:**

•An inner class can also be static, which means that you can access it without creating an object of the outer class

**Access Outer Class From Inner Class:**

•One advantage of inner classes, is that they can access attributes and methods of the outer class


# Inheritance
Inheritance allows one class (child) to **inherit** properties from another class (parent).
```
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}
class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

```

**Block:** 
A group of statement enclosed in { } that performs specific task
each time a object is created the block is executed before the constructor


**Method**
a function tat defines the behavior of object of  a class



**Constructor**
- used for initializing object of the class
- a default constructor is automatically called when a object is created
- constructor name should be same as class name
- don't have return type
- it can be overloaded 
- it cannot be abstract, final and synchronized

```
class Student{
	Student(){
	
	}
}
```
**Constructor Types:**
- Default : when there is no constructor written explicitly by the user. it's called automatically
- parametrized: can take multiple arguments to overload itself
- copy constructor: to copy one object to another
**note:**
a constructor can be private to control creation of object of that class


**This:**
- its a reference variable that points to current instance of the class
- distinguishes instance variable with local variable when there name is similar
```
class Person{

	Person(String name){
		this.name=name;
	}
	
	void display(){
	System.out.println("Name"+this.name);
	}
	
	Perosn(){
	this("Choudhary")
	}
}
public class Main{
	public static void main(String[] args){
	Person p1=new Person("Saurabh");
	p1.display();->saurabh
	Person p2=new Person();
	p2.display();-> choudhary
	}
}
``` 
**Constructor Chaining**
**Calling one constructor from another constructor** inside the same class or between parent and child classes.
### There are two types:

1. **Within the same class** (using `this()` keyword)
2. **Between parent and child classes** (using `super()` keyword)

# within the same class
When one constructor **calls another constructor** of the **same class** using `this()`.
```
class Student{
String name;
int rollno;

	Student(){
		this("saurabh",11917);
	System.out.println("Dafualt COnstructor is called");
	}
	Student(String name,int rollno){
		this.name=name;
		this.rollno=rollno;
		System.out.println("Parmetrized constructor is called);
	}
}
```
# **Between parent and child classes**
When a **child class constructor** calls the **parent class constructor** using `super()`.
```
class Person{
System.out.println("Person constructor is called")
}
class Student extends Person{
	Employee(){
	super(); <- this calls parent class constructor
	}
	System.out.println("Student class constructor is called");
}
```
### Important Rules:

- `this()` or `super()` **must be the first statement** in a constructor.   
- You can't use both `this()` and `super()` together in one constructor. 
- If you don’t explicitly write `super()`, Java automatically inserts a default `super()` call (only if the parent has a no-argument constructor). 

# Inheritance
A mechanism  in java that helps in inheriting the attributes and methods of a class in another classes

**why**
- method overriding for runtime polymorphism
- for code reusability

**Terms:**
Parent/superclass
child/subclass
extend keyword is used for extending parent class by a child class

```
class Animal{
	void eat(){
		System.out.println("Dog eats");
	}
}
class Dog extends Animal{
	void bark(){
		System,out.println("Dog barks");
	}
}

publc class Main{
	public static void main(){
		Dog d1=new Dog();
		d1.eat();
		d1.bark();
	}
}
```

**Types of Inheritance**
![[Pasted image 20250427113828.png]]
## 1. **Single Inheritance**

(One parent → One child)
Trick: A->B
```
class A {
    int x = 10;
}

class B extends A {
    int y = 20;
}

class Test {
    public static void main(String[] args) {
        B obj = new B();
        System.out.println(obj.x); // from A
        System.out.println(obj.y); // from B
    }
}

```

## 2. **Multilevel Inheritance**

(Parent → Child → Grandchild)

```
class A {
    int x = 10;
}

class B extends A {
    int y = 20;
}

class C extends B {
    int z = 30;
}

class Test {
    public static void main(String[] args) {
        C obj = new C();
        System.out.println(obj.x); // from A
        System.out.println(obj.y); // from B
        System.out.println(obj.z); // from C
    }
}

```

## 3. **Hierarchical Inheritance**

(One parent → Many children)

```
class A {
    int x = 10;
}

class B extends A {
    int y = 20;
}

class C extends A {
    int z = 30;
}

class Test {
    public static void main(String[] args) {
        B obj1 = new B();
        System.out.println(obj1.x); // from A
        System.out.println(obj1.y); // from B
        
        C obj2 = new C();
        System.out.println(obj2.x); // from A
        System.out.println(obj2.z); // from C
    }
}

```

## 4. **Multiple Inheritance**

(Java **does not support multiple inheritance with classes** ❌, but supports it with interfaces ✅)

```
interface A {
    int x = 10;
}

interface B {
    int y = 20;
}

class C implements A, B {
    int z = 30;
}

class Test {
    public static void main(String[] args) {
        C obj = new C();
        System.out.println(A.x); // from A
        System.out.println(B.y); // from B
        System.out.println(obj.z); // from C
    }
}

```

# Abstraction
Abstraction is a process of hiding the implementation details of an
object and showing only the essential features. It focuses on what
an object does rather than how it does it.

 Abstraction is achieved using:
 - Abstract Class
 - Interface
# Abstract Class
- A class that **cannot be instantiated** (you can't create an object of it).
- It can have **abstract methods** (without a body) **and** **normal methods** (with a body).
- use Abstract keyword to make a class  and a method abstract
- Can have constructors
- `extends` keyword
-  it can have static methods also
- It can have final methods

**Note**
A **final** method is declared with the final keyword
and cannot be overridden by subclasses.

• Prevents method overriding.
• Can be inherited but not modified.
• Abstract methods cannot be final.


```
Abstract class A{
	abstract void run();

	void display(){
		System.out.println("Display From A");
	}
	class B extends A{
		void run(){
			System.out.println("run from class B");
		}
		
	}
	class Test{
		puclic static void main(String[] saurabh){
			B obj=new B();
			obj.run();
			obj.display();
		}
	}
}
	
```

# Interface
- make java fully abstracted
- all methods are public and abstract by default
- interface can be implemented by a class using keyword "implements"
- No constructors
- `implements` keyword
- An interface is a blueprint of a class that contains abstract methods
```
Interface A{
	void show();
}
class B implements A{
	public void show(){
		System.out.println("show from class B");
	}
}
class Test{
	public static void main(String[] args){
		B obj=new B();
		obj.show();
	}
}
```

**Note:**
Java does not support multiple inheritance through classes primarily to avoid
ambiguity (diamond problem)and complexity).

- When a class inherits from more than one class, it can lead to confusion
about which methods, fields, or behavior belong to which parent class,
making the code difficult to maintain, debug, and extend
- Example: If two parent classes provide different implementations of the
same method, the child class would be confused about which method to
inherit.

**Q. Why Diamond Problem Occurs**
when a class inherits from two classes that both inherit from the same parent class.
Because of this, the bottom class gets **two copies** of the top parent class — and the program gets **confused**:
- Which copy should it use?
- How should it handle things like shared variables or methods?


```
interface A{
	default void show(){
		System.out.println("Hello from class A");
	}
}
interface B extends A{
		default void show(){
			System.out.println("Hello from B");
		}
}
interface C extends B{
	default void show(){
		System.out.println("Hello from C");
	}
}
class D implements B,C{
	public void show(){
		B.super.show();
	}
	public static void main(String[] args){
		D obj=new D();
		obj.show();
	}
}

```
- You **cannot call** both `B.super.show()` and `C.super.show()` together if they are connected.

# Encapsulation
- wrapping of data members and member methods in a single unit i.e., object is called Encapsulation.
- hides the internal representation of object from external world and can be accessed by controlled mechanism
- Improves security of data

# How
- data fields are made private and private members can be accessed by private method
- Encapsulated data is accessed and modified using Accessor(getter) and mutator(setter) function


```
class Employee{
	private String name;
	private int age;

	public void setName(String Name){
		this.name=name;
	}
	public String getName(){
		return name;
	}
}
public class Main{
	public void main(String[] args){
		Employee obj=Employee();
		obj.SetName("Saurabh");
		
	    System.out.println("Employee Name: " + emp.getName());
	}
}
```

| **Feature**         | **Encapsulation**                                        | **Abstraction**                                                       |
| ------------------- | -------------------------------------------------------- | --------------------------------------------------------------------- |
| **Meaning**         | Hiding **data** and **restricting direct access** to it. | Hiding **complex details** and showing only the **important things**. |
| **Focus**           | **Protect** the data.                                    | **Simplify** the system for the user.                                 |
| **How?**            | Using `private`, `getter` and `setter` methods.          | Using `abstract classes`, `interfaces`, or `abstract methods`.        |
| **Example**         | Making variables private and accessing them via methods. | Showing only a simple "Start Car" button, hiding engine complexity.   |
| **Goal**            | **Control** how data is accessed and modified.           | **Hide** complexity and make the system easier to use.                |
| **In simple words** | **Data hiding**                                          | **Implementation hiding**                                             |
|                     |                                                          |                                                                       |
**Hiding Complexities**
```
abstract class Vehicle {
    abstract void start();
}

class Car extends Vehicle {
    void start() {
        System.out.println("Car started with key");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.start(); // User only cares about start(), not how it works internally
    }
}

```
# Polymorphism
 The ability of a single method or object to perform different tasks. It allows different classes to define the same method, but with different behaviors, enabling the method to behave differently based on the object that is calling it.
```
class Calculator {
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
}
```
# Types of polymorphism
**1)Compile Time
- Achieved by defining multiple methods with same name but different parameter
- The method to be invoked is determined at compiled time
- Method Overloading
2)Run Time
- a subclass provides a specific implementation for a method that is already defined in its superclass. The overridden method in the subclass must have the same name, return type, and parameters as the method in the superclass.
- which method to invoked is determined at runtime
-  Method Overriding

**Method Overloading**
- when a class have multiple methods with the same name, but different parameters/signature( either in number, types, or both).
- Then overloading allows to perform similar operation with different inputs.
- Return type can be the same or different, but it alone cannot be used to differentiate overloaded methods
```
class Calculator {
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
}

```

 **Method Overriding
 - a subclass provides a specific implementation for a method that is already defined in its superclass. The overridden method in the subclass must have the same name, return type, and parameters as the method in the superclass.
 - The **child class gives its own version** of the method.
 - The same method can behave differently depending on the subclass object
 - Allows subclasses to define their own specific behaviors while still keeping the same method signature
 ```
 class ANimal{
	 void sound(){
		 System.out.println("Animal makes sound");
	 }
 }
 class Dog extends Animal{
	 @override <- annotation
	 void sound(){
		  System.out.println("Dog Barks");
	 }
 }
 public class main(){
	 public static void main(){
		 Animal obj=new Dog() <-upcasting happening
		 obj.sound(); <- dog barks 
	 }
 }
```

### 📚 What is Upcasting?
- **Upcasting** means **treating a child class object** like a **parent class object**.
- We assign a **child object** to a **parent class reference**.

| Feature                 | Method Overloading                                                   | Method Overriding                                                        |
| ----------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Meaning**             | Same method **name**, but **different parameters** (in same class).  | Same method **name**, **same parameters** (in parent and child classes). |
| **Where it happens?**   | **Within one class**.                                                | **Between two classes** (Parent → Child).                                |
| **Purpose**             | To **increase readability** (many ways to do similar things).        | To **change behavior** in child class.                                   |
| **Inheritance needed?** | ❌ Not needed.                                                        | ✅ Required (inheritance).                                                |
| **Polymorphism Type**   | **Compile-time Polymorphism** (early binding).                       | **Runtime Polymorphism** (late binding).                                 |
| **Return Type**         | Can be **different** or **same**.                                    | Must be **same** (or subtype).                                           |



# Static and Dynamic Binding

| Feature               | Static Binding (Early Binding)                             | Dynamic Binding (Late Binding)          |
| --------------------- | ---------------------------------------------------------- | --------------------------------------- |
| **When it happens?**  | During **compile time**.                                   | During **runtime**.                     |
| **Speed**             | **Faster** (already decided at compile time).              | **Slower** (decided at runtime).        |
| **Type of methods**   | Mostly for **private**, **final**, and **static** methods. | Mostly for **overridden methods**.      |
| **Polymorphism type** | **Compile-time Polymorphism**.                             | **Runtime Polymorphism**.               |
| **Example**           | **Method overloading**.                                    | **Method overriding**.                  |
| **Control**           | Done by **compiler**.                                      | Done by **JVM (Java Virtual Machine)**. |
### ✨ In one simple line:
 **Static Binding**: Compiler decides method to call.
 **Dynamic Binding**: JVM decides method to call **at runtime**.

**Static Binding Example (Compile time binding):**
```
class MathOperation {
    static void add(int a, int b) {
        System.out.println("Sum: " + (a + b));
    }
    
    public static void main(String[] args) {
        MathOperation.add(5, 10); // Bound at compile time
    }
}

```
👉 `add()` is a **static method**, so the call is decided at **compile time**.

**Dynamic Binding Example (Runtime binding):**
```
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal obj = new Dog(); // Upcasting
        obj.sound();            // Bound at runtime
    }
}

```
👉 `sound()` is **overridden**, so which version to call (`Animal` or `Dog`) is decided at **runtime

# Exception Handling 

**Exception**
- exception is an error/problem that occurs when a program is running and can be fixed.
- Examples
	• Trying to divide a number by zero.
	• Opening a file that doesn’t exist.
	• Entering text where a number is expected
	
When an exception occurs, the program might crash or behave unexpectedly. To this, we handle exceptions using special code (like try-catch) to fix the issue or show a helpful message to the user. This way, the program can continue running smoothly.


**Error**
- this is a serious problem that stops the program completely and cannot be fixed by the program itself.
- Examples
	- OutOfMemoryError

| Feature              | Error                                                              | Exception                                                   |
| -------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------- |
| **Meaning**          | Serious problems that **cannot** be handled by the program.        | Problems that **can** be handled by the program.            |
| **Type**             | **Unrecoverable**.                                                 | **Recoverable**.                                            |
| **Examples**         | `OutOfMemoryError`, `StackOverflowError`.                          | `NullPointerException`, `ArithmeticException`.              |
| **Caused by**        | Issues **outside** the program (like hardware crash, memory full). | Issues **inside** the program (like wrong code, bad input). |
| **Handling**         | Cannot be handled using `try-catch`.                               | Can be handled using `try-catch`.                           |
| **When it happens?** | Usually at **runtime**.                                            | Usually at **runtime** (but can be compile-time too).       |

**Error Example:**
```

e.g1:
public class Main {
    public static void main(String[] args) {
        main(args); // Recursive call without end
    }
}
// ❌ StackOverflowError will happen (cannot catch it easily).



e.g2:

public class ErrorExample
{
public static void main(String[] args)
{
// Try to allocate a huge amount of memory
int[] largeArray = new int[Integer.MAX_VALUE];
}
}
// ❌ JVM will run out of memory will happen (cannot catch it easily).
```


**Exception Example:**
```
public class Main {
    public static void main(String[] args) {
        try {
            int result = 5 / 0; 
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero!");
        }
    }
}

```



![[1_dK0sEcnhdaCxjkLuI1N4zQ.webp]]

**Note:**
- Checked exception are must be handled by the try-catch block.

**Why do we need of exception handling**
- Prevent system crash
- keep program running in flow
- helps in easy debugging

**Steps to perform Exception Handling**
- Exception handling allows to run program smoothly even if an exception occurs.
- By helping in detecting, report, and managing the exceptions
**Steps:**

1. find/hit an error
2. inform that error has occurred
3. Receive/catch the error information
4. handle the exception by  try-catch, try-multiple catch, throw, throws, finally.

**Try-Catch**
👉 `try-catch` is like saying:
- "**Try** to do something."
- "**Catch** the error if something goes wrong and handle it."

**Structure:**
- **`try { }`** block → You put the code that **might** cause a problem here.
- **`catch { }`** block → If there’s an error, this block **catches** it and lets you decide what to do.

Try-Catch Example
```
public class ErrorExample{
public static void main(String[] args){

// Try to allocate a huge amount of memory
int[] largeArray = new int[Integer.MAX_VALUE];
}
}
```


Example of `try` with multiple `catch` blocks:
```
public class Main {
    public static void main(String[] args) {
        try {
            // Trying multiple operations that might cause different exceptions
            int a = 10;
            int b = 0; // Division by zero will happen here
            int result = a / b;
            System.out.println("Result: " + result);

            int[] arr = {1, 2, 3};
            System.out.println(arr[5]); // ArrayIndexOutOfBoundsException
        }
        catch (ArithmeticException e) {
            // This will catch division by zero
            System.out.println("Error: Cannot divide by zero!");
        }
        catch (ArrayIndexOutOfBoundsException e) {
            // This will catch array index out of bounds error
            System.out.println("Error: Array index is out of bounds!");
        }
        catch (Exception e) {
            // This will catch any other type of exception
            System.out.println("Error: Something went wrong!");
        }
    }
}

```

### **Why use multiple `catch` blocks?**

- **More precise error handling**: Each `catch` block can handle a specific type of exception.  
- **Easier debugging**: You know exactly which error occurred based on the type of exception.
- **Cleaner code**: You don't have to handle all exceptions the same way. You can give them different messages or solutions.

**Note**
- The **specific exceptions** (like `ArithmeticException`, ArrayIndexOutOfBoundsException) should come **before** the **general `Exception`** catch block.  
- If `Exception` is placed first, the other `catch` blocks won't get a chance to run because `Exception` will catch all exceptions (including more specific ones).


**Throw/Custom Exception**
The throw keyword is used to explicitly throw an exception from a method
or a block of code

```
public class Main {
    public static void main(String[] args) {
        int age = 15;
        
        if (age < 18) {
            throw new ArithmeticException("You are too young!"); 
        }
        
        System.out.println("You are allowed.");
    }
}

```

**Throws**
- Used in the **method signature** to **declare that a method can throw one or more exceptions**.
- It is used when you **expect** an exception to occur inside the method, but you don't want to handle it inside that method.
- The **caller** of the method (like `main` in the example) must either handle the exception or declare it again using `throws`.
```
import java.io.*; // For IOException

public class Main {
    public static void main(String[] args) {
        try {
            readFile();
        }
        catch (IOException e) {
            System.out.println("Problem reading the file!");
        }
    }

    public static void readFile() throws IOException {
        FileReader file = new FileReader("abc.txt"); // File may not exist
    }
}

```

| **Feature**  | **`throw`**                                    | **`throws`**                                         |
| ------------ | ---------------------------------------------- | ---------------------------------------------------- |
| **Usage**    | To **throw** an exception manually.            | To **declare** that a method may throw an exception. |
| **Location** | Inside the method or block of code.            | In the method signature (header).                    |
| **Purpose**  | Used to **explicitly throw** an exception.     | Used to **declare** exceptions a method can throw.   |
| **Example**  | `throw new IllegalArgumentException("Error");` | `public void myMethod() throws IOException {}`       |


| Term             | Meaning                                                                                         | Where Used                                 | Example                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------- |
| **`final`**      | A **keyword** that means "cannot be changed."                                                   | Variables, Methods, Classes                | `final int x = 5;` (x can't change now)  <br>`final class Car {}` (Car can't be extended) |
| **`finally`**    | A **block** that _always_ executes after a `try-catch`, no matter what.                         | Exception Handling                         | `try { } catch (Exception e) { } finally { System.out.println("Always runs"); }`          |
| **`finalize()`** | A **method** called by the **Garbage Collector** before destroying an object (rarely used now). | Object cleanup (Deprecated in modern Java) | `protected void finalize() throws Throwable { }`                                          |

**Summary in one-liners:**

- **`final`** = _"You can't change this."_
- **`finally`** = _"This code will always run after try-catch."_
- **`finalize()`** = _"Before Java destroys an object, it can clean up with this method (but it's outdated)."_


**Why Do we need collection framework**
- fixed size 
- no in-built method
- no flexibility to store multiple data type
Java Collection resolved the above issues and allowed to have dynamic resizing, prebuilt data structure, faster performance, generic data type support, easy manipulation


**Java Collection Framework**
-  collection of classes and interfaces which helps in storing and processing the data efficiently.
- has several useful classes which have tons of functions which makes a programmer tasks super easy.


![[Pasted image 20250427183414.png]]

|Feature|**Array**|**Linked List**|
|---|---|---|
|**Storage**|Elements are stored _contiguously_ in memory.|Elements are stored _anywhere_; each element (node) points to the next.|
|**Access Speed**|**Fast** (direct access by index, `O(1)`).|**Slow** (must go node by node, `O(n)`).|
|**Insertion/Deletion**|Expensive (may need to shift elements).|Easy (just change a few pointers).|
|**Size**|Fixed size (unless using dynamic arrays like `ArrayList`).|Dynamic size (grows/shrinks easily).|
|**Memory Usage**|Less overhead (just data).|More overhead (data + pointer).|
|**Best for**|Frequent access to elements.|Frequent insertion/deletion operations.|

![[Pasted image 20250427183623.png]]

**Hashset**
- java.util.HashSet Class
- It is a **collection** in Java that **stores unique elements only**
- **No duplicates** allowed.
- **Order is not guaranteed** (elements can appear in any order). 
- It uses a **hash table** internally (which makes operations very fast).


TODO: ArrayList, LinkedList, HashMap, TreeMap, HashSet

---
# Multi-Threading
- the ability to execute multiple threads concurrently within a single
program
- A thread is a light weight program that allows parallel execution of tasks ,improving efficiency and performance of system.
![[Pasted image 20250427194808.png]]

**Why use Multithreading?**
- Better performance
- Resource sharing
- Responsiveness 
- Parallel Processing
- better CPU utilization

**Thread Life Cycle**
![[Pasted image 20250427195333.png]]

| Stage                           | What Happens (Simple)                                                                                                               |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **1. New (Created)**            | You create a thread, but it hasn’t started yet. _(Baby thread is born, but still sleeping.)_                                        |
| **2. Runnable**                 | You called `start()`, and now the thread is ready to run. _(The baby is awake and waiting to be picked to play.)_                   |
| **3. Running**                  | The thread is picked by the CPU and is now actually running code. _(The baby is playing happily.)_                                  |
| **4. Blocked/Waiting/Sleeping** | The thread is temporarily paused (maybe waiting for a resource or told to sleep). _(The baby is waiting for milk or taking a nap.)_ |
| **5. Terminated (Dead)**        | The thread finishes its work or is killed. _(The baby is done playing and goes to sleep permanently.)_                              |
```
NEW → RUNNABLE → RUNNING → (WAITING/BLOCKED/SLEEPING) → RUNNING → TERMINATED

```

Example:
```
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class LifeCycle {
    public static void main(String[] args) {
        MyThread t = new MyThread(); // NEW
        t.start(); // RUNNABLE → RUNNING
    }
}

```

### 1. **New (Created)**

- A **thread object is created**, but it is **not yet running**.
-  It is just **sitting there**, waiting for you to tell it to start.
```
Thread t = new Thread(); // Thread created, but not started.
```
### 2. **Runnable**

-  You call the **`start()`** method.
-  The thread is **ready** to run but **waiting** for the CPU to assign time.
-  Many threads can be runnable at the same time, but CPU picks one.
```
t.start(); // Now it is Runnable

```

### 3. **Running**

- The thread is **picked by CPU** and is **actually executing** its `run()` method.
-  Only one thread per CPU core is running at a time (unless multiple cores are involved).
### 4. **Blocked / Waiting / Sleeping (Not Running)**

There are **three sub-cases** here:

|Type|What it means|
|---|---|
|**Blocked**|Waiting for a lock (e.g., another thread holds a resource).|
|**Waiting**|Waiting indefinitely for another thread's signal.|
|**Sleeping**|Thread is paused for a specific time (e.g., sleep for 2 seconds).|
```
Thread.sleep(2000); // Sleep for 2 seconds
```

### 5. **Terminated (Dead)**

- The thread finishes **normally** (completed `run()`) **or** it is **forcefully stopped** due to an error or by being killed.
-  A terminated thread **cannot be restarted**.


-----
**Thread Priority**
- **Every thread** in Java has a **priority** (an integer between **1 and 10**).
- It **hints** to the CPU about _which thread is more important_ and _should be picked first_.
- **Higher priority = more chance** of running earlier (but not guaranteed!).
- **Priority can influence**, but it does **not guarantee** execution order but CPU can ignore priority.

| Priority Constant      | Value | Meaning                 |
| ---------------------- | ----- | ----------------------- |
| `Thread.MIN_PRIORITY`  | 1     | Least important thread  |
| `Thread.NORM_PRIORITY` | 5     | Normal/default priority |
| `Thread.MAX_PRIORITY`  | 10    | Most important thread   |

```
Thread t1 = new Thread();
t1.setPriority(Thread.MAX_PRIORITY); // Set priority to 10

System.out.println(t1.getPriority()); // Prints 10

```

```
class MyThread extends Thread {
    public void run() {
        System.out.println(Thread.currentThread().getName() + " Priority: " + Thread.currentThread().getPriority());
    }
}

public class TestPriority {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        t1.setPriority(Thread.MIN_PRIORITY);  // Priority 1
        t2.setPriority(Thread.NORM_PRIORITY); // Priority 5
        t3.setPriority(Thread.MAX_PRIORITY);  // Priority 10

        t1.start();
        t2.start();
        t3.start();
    }
}

```


|**Method**|**Description**|**Example Usage**|
|---|---|---|
|`start()`|Starts a thread by calling its `run()` method **in a new thread**.|`t1.start();`|
|`run()`|Defines the code executed by the thread (**does NOT start** a new thread if called directly).|`t1.run();` _(Not recommended)_|
|`sleep(ms)`|Pauses the thread for **ms milliseconds**, then resumes automatically.|`Thread.sleep(1000); // Pauses for 1 second`|
|`join()`|Makes one thread **wait** for another to finish before proceeding.|`t1.join(); // Waits for t1 to finish`|
|`yield()`|**Suggests** that the current thread pause and let others run.|`Thread.yield();`|
|`isAlive()`|Returns `true` if the thread is **still running**, otherwise `false`.|`t1.isAlive();`|
|`setName(String name)`|Sets the **name** of a thread.|`t1.setName("Worker");`|
|`getName()`|Gets the **name** of a thread.|`System.out.println(t1.getName());`|
|`setPriority(int p)`|Sets the **priority** of a thread (`1` to `10`, default `5`).|`t1.setPriority(Thread.MAX_PRIORITY);`|
|`getPriority()`|Returns the **priority** of a thread.|`System.out.println(t1.getPriority());`|
|`interrupt()`|**Interrupts** a sleeping or waiting thread.|`t1.interrupt();`|
|`isInterrupted()`|Checks if the thread has been **interrupted**.|`t1.isInterrupted();`|
|`wait()`|Causes the thread to **wait** until another thread calls `notify()` or `notifyAll()`.|Inside synchronized block: `t1.wait();`|
|`notify()`|Wakes up **one** waiting thread.|Inside synchronized block: `t1.notify();`|
|`notifyAll()`|Wakes up **all** waiting threads.|Inside synchronized block: `t1.notifyAll();`|



**why we need thread synchronization**
When multiple threads access **shared resources** (like a variable or object) **simultaneously**, we might run into issues where the threads interfere with each other, leading to **inconsistent results** . This is known as a **race condition**.

**Key Issues Without Synchronization:**
**Race Condition**: When multiple threads access shared data at the same time and modify it, causing unexpected results.
**Data Inconsistency**: If multiple threads read and write to shared resources simultaneously, you might get inconsistent or corrupted data.
**Deadlock** happens when two or more threads are waiting for each other to release resources. This leads to a standstill, where no thread can continue.

**How Synchronization Works:**

**Synchronized Methods**: 
- You can mark methods as `synchronized` so that only **one thread** can execute them at a time.
```
class Counter {
    private int count = 0;
    
    // Synchronized method to prevent race condition
    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

```

**Synchronized Blocks**: 
- You can also synchronize only a specific part of code (not the entire method), giving more control over what gets locked.
- Allows multiple threads to execute non-critical sections of code simultaneously.

```
class Counter {
    private int count = 0;
    
    public void increment() {
        synchronized(this) { // Lock on this object
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}

```
**Static Synchronization**
- If a method is static, synchronization applies to the class-level lock instead of an instance
- Used when multiple threads access static resources
- Synchronizes **static methods** (methods that belong to the class, not any object instance) so that only one thread can access the **static method** at a time, even across all instances of the class.
- **Static methods** belong to the class, not any specific instance. Therefore, they **share the same lock** across all instances of the class.
- This means, if one thread is accessing a **static synchronized method**, no other thread can access any other **static synchronized method** of the same class until the first one finishes.
- For **normal synchronization**, each object instance gets its own lock.
- For **static synchronization**, the **class itself** gets the lock — no matter which instance of the class is involved.

```
class SharedResource {
    synchronized static void printData(int n) {
        // Printing multiplication table for 'n'
        for (int i = 1; i <= 5; i++) {
            System.out.println(n * i);  
            try { 
                Thread.sleep(500);
            } catch (InterruptedException e) { 
                e.printStackTrace();
            }
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> SharedResource.printData(2)); 
        Thread t2 = new Thread(() -> SharedResource.printData(3)); 

        
        t1.start();
        t2.start();
    }
}


```
----
**Inter thread Communication cooperation**

Thread intercommunication refers to the process where **multiple threads** cooperate and communicate with each other to achieve a specific task or share data.
- inter-thread communication is mainly achieved using methods like `wait()`, `notify(), and `notifyAll()` — all of which are part of the Object class

- **wait()**:
    - **Pauses the current thread** until another thread **notifies** it.
    - Must be used **within a synchronized block** (because it works with the intrinsic lock of the object).
- **notify()**:
    - **Wakes up one thread** that is waiting on the same object.
    - If multiple threads are waiting, the choice of which thread to wake up is not guaranteed.
- **notifyAll()**:
    - **Wakes up all threads** that are waiting on the same object.

----
# Wrapper Class
- convert primitive data types into objects
- support **autoboxing** and **unboxing**, which automatically converts primitives to objects and vice versa.


![[Pasted image 20250427220531.png]]
![[Pasted image 20250427220549.png]]


 **Autoboxing** :Primitive → Object
 ```
 Integer obj = 10; 
```
 Unboxing: Object → Primitive
```
int num = obj; 
```

![[Pasted image 20250427220940.png]]

|**Wrapper Class**|**Common Methods**|**Description**|
|---|---|---|
|**Integer**|`parseInt(String s)`|Converts a `String` to an `int`.|
||`valueOf(String s)`|Converts a `String` to an `Integer` object.|
||`intValue()`|Returns the `int` value of the `Integer` object.|
||`compareTo(Integer anotherInteger)`|Compares two `Integer` values.|
|**Double**|`parseDouble(String s)`|Converts a `String` to a `double`.|
||`valueOf(String s)`|Converts a `String` to a `Double` object.|
||`doubleValue()`|Returns the `double` value of the `Double` object.|
||`compareTo(Double anotherDouble)`|Compares two `Double` values.|
|**Character**|`charValue()`|Returns the `char` value of the `Character` object.|
||`isDigit(char ch)`|Checks if a character is a digit.|
||`isLetter(char ch)`|Checks if a character is a letter.|
||`isWhitespace(char ch)`|Checks if a character is a whitespace.|
|**Boolean**|`parseBoolean(String s)`|Converts a `String` to a `boolean`.|
||`valueOf(String s)`|Converts a `String` to a `Boolean` object.|
||`booleanValue()`|Returns the `boolean` value of the `Boolean` object.|

```
public class IntegerExample {
    public static void main(String[] args) {
      
        String str = "123";
        int num = Integer.parseInt(str); 
        System.out.println("Parsed int: " + num);

        Integer integerObj = Integer.valueOf(str);
        System.out.println("Integer object: " + integerObj);

        Integer int1 = 10, int2 = 20;
        int comparison = int1.compareTo(int2); 
        System.out.println("Comparison result: " + comparison);
    }
}

```
---
# File Handling

file handling is primarily done through the **java.io package**. You can perform operations like reading, writing, creating, and deleting files using several classes like `File`, `FileReader`, `BufferedReader`, `FileWriter`, `BufferedWriter`, etc.

### **Key Steps in File Handling**:
1. **Create a file**: Use the File class and its createNewFile() method
2. **Write to a file**: Utilize FileWriter or BufferedWriter to write data efficiently.
3. **Read from a file** : Use Scanner or BufferedReader for reading file contents
4. **Close the file** (Always important to release system resources  
5. **Delete a file**: Apply the delete() method of the File class to remove a file
6. **Exception Handling** (For any errors like file not found or access issues.


**Creating a File**
```
import java.io.File;
import java.io.IOException;

public class FileCreation {
    public static void main(String[] args) {
        // Create a file object
        File file = new File("example.txt");

        try {
            // Create a new file if it doesn't exist
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}

```

**Writing to a File**
```
import java.io.FileWriter;
import java.io.BufferedWriter;
import java.io.IOException;

public class FileWriteExample {
    public static void main(String[] args) {
        // Create a FileWriter object to write to the file
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"))) {
            writer.write("Hello, this is a sample text.");
            writer.newLine(); // Add a new line
            writer.write("This is another line.");
            System.out.println("Data written to the file.");
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}

```

**Reading from a File**
```
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;

public class FileReadExample {
    public static void main(String[] args) {
        // Create a FileReader object to read the file
        try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            // Read each line from the file
            while ((line = reader.readLine()) != null) {
                System.out.println(line);  // Print the line
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}

```


**Delete a file**
```
import java.io.File;

public class FileDeleteExample {
    public static void main(String[] args) {
        File file = new File("example.txt");

        if (file.delete()) {
            System.out.println("File deleted: " + file.getName());
        } else {
            System.out.println("Failed to delete the file.");
        }
    }
}

```
---
**Stream Class**
- **Streams** are part of the **java.io package** and are used to read and write data to files, network connections, or other input/output devices
- The **Stream** class allows you to handle data in a **sequential** manner.
- Java has two types of streams:
	- 1. **Byte Streams**: TByte streams handle raw binary data using InputStream and
OutputStream.
    - **InputStream** (used for reading bytes)
    - **OutputStream** (used for writing bytes)
2. **Character Streams**: Character streams handle text-based data using Reader and Writer
classes.
    - **Reader** (used for reading characters)
    - **Writer** (used for writing characters)




![[Pasted image 20250427223255.png]]


# Byte Stream
- used to read and write binary data (e.g., images, audio, video, and files) one byte at a time in Java
- Works with 8-bit bytes for efficiency.
-  **InputStream** (used for reading bytes)
-  **OutputStream** (used for writing bytes)

**Input Stream
- The **`InputStream`** class is used for reading **byte data**. 
- It is the superclass for all classes that read bytes in Java
- InputStream represents the **source** of data that can be read in a stream

#### **Basic Methods of InputStream**:

- **`read()`**: Reads the next byte of data from the input stream. 
- **`read(byte[] b)`**: Reads bytes into an array.
- **`skip(long n)`**: Skips over the specified number of bytes.
- **`available()`**: Returns the number of bytes that can be read without blocking.



```
import java.io.*;

public class InputStreamExample {
    public static void main(String[] args) {
        try (FileInputStream fileInput = new FileInputStream("example.txt")) {
            int data;
            while ((data = fileInput.read()) != -1) {  // Read byte by byte until EOF
                System.out.print((char) data);  // Print the byte as a character
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```


**Output stream**
- The **`OutputStream`** class is used for writing **byte data**
- It is the superclass for all classes that write bytes in Java
- OutputStream represents the **destination** where data can be written.

#### **Basic Methods of OutputStream**:

- **`write(int b)`**: Writes the specified byte to the output stream.
- **`write(byte[] b)`**: Writes an array of bytes to the output stream.
- **`flush()`**: Forces any buffered output to be written.
- **`close()`**: Closes the stream and releases resources.



```
import java.io.*;

public class OutputStreamExample {
    public static void main(String[] args) {
        try (FileOutputStream fileOutput = new FileOutputStream("example_output.txt")) {
            String data = "Hello, world!";
            byte[] bytes = data.getBytes();
            fileOutput.write(bytes);  // Write bytes to the file
            System.out.println("Data written to the file.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

|**Aspect**|**InputStream**|**OutputStream**|
|---|---|---|
|**Purpose**|Used for reading byte data|Used for writing byte data|
|**Direction**|Data flows **into** the program|Data flows **out of** the program|
|**Common Classes**|FileInputStream, BufferedInputStream, etc.|FileOutputStream, BufferedOutputStream, etc.|
|**Read Method**|`read()` (reads one byte)|`write()` (writes one byte)|
|**Buffering Support**|BufferedInputStream adds buffering|BufferedOutputStream adds buffering|


---

**ByteArrayInputStream & ByteArrayOutputStream**
-  handling byte arrays as input and output streams instead of files.
- Reads data from a byte array as an input stream.
- These classes work in memory (RAM), making them faster than file-based streams.

**ByteArrayInputStream (Reading from Byte Array)**
- Reads data from a byte array as an input stream.
- Used for processing data in memory without accessing files.

```
ByteArrayInputStream bais = new ByteArrayInputStream(byteArray);
```

**ByteArrayOutputStream (Writing to Byte Array)**
- Writes data to a byte array instead of a file
- Useful for modifying, compressing, or buffering data in memory before writing to disk or network
```
ByteArrayOutputStream baos = new ByteArrayOutputStream();
```

---
**BufferedInputStream & BufferedOutputStream**

- reducing the number of I/O operations to improve performance.
-  Instead of reading/writing one byte at a time, they use a buffer.

BufferedInputStream (Reading Data)
```
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("filename.txt"));
```

BufferedOutputStream (Writing Data)
```
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("filename.txt"));
```

---
**Character Stream**
- used to read and write text data
- Character Streams work with 16-bit Unicode characters
- suitable for reading and writing text files.
- used for **handling character-based data** (like text data)

### **Key Classes in Character Streams**

1. **Reader** (abstract class): The superclass for all character-based input streams.
2. **Writer** (abstract class): The superclass for all character-based output streams.

### **Basic Methods in Reader and Writer**

#### **Reader Methods**:

- **`read()`**: Reads a single character.
- **`read(char[] cbuf)`**: Reads a sequence of characters into an array.
- **`close()`**: Closes the stream and releases any system resources.

#### **Writer Methods**:

- **`write(int c)`**: Writes a single character.
- **`write(char[] cbuf)`**: Writes an array of characters.
- **`flush()`**: Ensures that any buffered characters are written to the destination.
- **`close()`**: Closes the stream and releases any system resources.


**Reading from a File (FileReader)**
```
import java.io.*;

public class CharacterStreamReader {
    public static void main(String[] args) {
        try (FileReader reader = new FileReader("input.txt")) {
            int data;
            while ((data = reader.read()) != -1) {  // Reads one character at a time
                System.out.print((char) data);  // Print the character
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

**Writing to a File (FileWriter)**
```
import java.io.*;

public class CharacterStreamWriter {
    public static void main(String[] args) {
        try (FileWriter writer = new FileWriter("output.txt")) {
            String data = "Hello, this is a text file using character streams!";
            writer.write(data);  // Write the string of characters to the file
            System.out.println("Data written to the file.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

---
**BufferedReader and BufferedWriter**
- **BufferedReader** and **BufferedWriter** are more efficient than the basic `FileReader` and `FileWriter` because they use internal buffering. This reduces the number of I/O operations by reading and writing large chunks of data at once, rather than one character at a time.

**Using BufferedReader to Read Lines**
```
import java.io.*;

public class BufferedCharacterStreamReader {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("input.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {  // Reads one line at a time
                System.out.println(line);  // Print each line
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

**Using BufferedWriter to Write Lines**
```
import java.io.*;

public class BufferedCharacterStreamWriter {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            writer.write("Hello, World!");
            writer.newLine();  // Adds a line break
            writer.write("This is written using BufferedWriter.");
            writer.flush();  // Make sure everything is written to the file
            System.out.println("Data written to the file.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```


|**Aspect**|**Byte Streams**|**Character Streams**|
|---|---|---|
|**Handle**|Raw binary data (bytes)|Text data (characters)|
|**Classes**|`InputStream`, `OutputStream`|`Reader`, `Writer`|
|**Example Classes**|`FileInputStream`, `FileOutputStream`|`FileReader`, `FileWriter`|
|**Use Case**|For reading/writing binary files (like images, audio, etc.)|For reading/writing text files (like `.txt`, `.csv`)|
|**Encoding**|Does not handle character encoding|Handles character encoding (like UTF-8, UTF-16)|
|**Buffering Support**|BufferedInputStream, BufferedOutputStream|BufferedReader, BufferedWriter|


---
**CharArrayReader**
- It **reads characters** from a **character array**
- `read()`: Reads one character at a time.
- `close()`: Closes the stream.

**CharArrayWriter**
- It **writes characters** into an internal **character array**
- it grows automatically as you add more characters.
- **Important Methods**:

- `write(int ch)`: Writes a single character.
- `write(String str)`: Writes a string.
- `toCharArray()`: Returns the internal array.
- `toString()`: Returns everything written as a **String**.
- `close()`: Closes the stream.

**CharArrayReader Example**
```
import java.io.CharArrayReader;
import java.io.IOException;

public class CharArrayReaderExample {
    public static void main(String[] args) throws IOException {
        char[] data = {'H', 'e', 'l', 'l', 'o'};
        CharArrayReader reader = new CharArrayReader(data);

        int ch;
        while ((ch = reader.read()) != -1) {
            System.out.print((char) ch);
        }
        reader.close();
    }
}

```



**CharArrayWriter Example**
```
import java.io.CharArrayWriter;
import java.io.IOException;

public class CharArrayWriterExample {
    public static void main(String[] args) throws IOException {
        CharArrayWriter writer = new CharArrayWriter();
        
        writer.write('H');
        writer.write('i');
        writer.write(' ');
        writer.write("there!");

        // Convert written data to String
        String result = writer.toString();
        System.out.println(result);

        writer.close();
    }
}

```
---
**Serialization**
-  process of **converting** a **Java object** into a **stream of bytes**.
- This allows the object to be **saved** into a file, database, or sent over a network
**Deserialization**
- Turning those **bytes** back into the **original Java object**.

**Why Do We Need Serialization?**
- **Save object state**: Store objects in files/databases for later use.
- **Send objects over a network**: Like sending a message in a multiplayer game.
- **Deep copy objects**: Make a complete clone of an object.

**Serialization**
```
import java.io.Serializable;

class Student implements Serializable {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

```

**Serialization (Save Object to File)**
```
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class Student implements Serializable {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

public class SerializeExample {
    public static void main(String[] args) {
        try {
            Student s1 = new Student(101, "Alice");

            FileOutputStream fileOut = new FileOutputStream("student.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);

            out.writeObject(s1); // Writing the object
            out.close();
            fileOut.close();

            System.out.println("Object has been serialized.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

**Deserialization (Load Object from File)**
```
import java.io.FileInputStream;
import java.io.ObjectInputStream;

public class DeserializeExample {
    public static void main(String[] args) {
        try {
            FileInputStream fileIn = new FileInputStream("student.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);

            Student s = (Student) in.readObject(); // Reading the object
            in.close();
            fileIn.close();

            System.out.println("Object has been deserialized.");
            System.out.println("ID: " + s.id);
            System.out.println("Name: " + s.name);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
Note:`.ser` file -> A file that stores the serialized object
```

---
**`transient` Keyword**
- If you mark a variable `transient`, it **won't be saved** during **serialization**.
- Sometimes you don't want to save sensitive or useless data (like passwords or temporary data).
```
import java.io.Serializable;

class User implements Serializable {
    String name;
    transient String password; // won't be saved

    User(String name, String password) {
        this.name = name;
        this.password = password;
    }
}

```
---

**`clone()` Method**
- **Clone** means **making a copy** of an object.
- Class must implement `Cloneable` interface and override `clone()` method.
```
class Student implements Cloneable {
    int id;

    Student(int id) {
        this.id = id;
    }

    public Object clone() throws CloneNotSupportedException {
        return super.clone(); // default cloning
    }
}

public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
        Student s1 = new Student(10);
        Student s2 = (Student) s1.clone();
        System.out.println(s2.id); // Output: 10
    }
}

```

---
**Lambda Expression**
- A **shortcut** way to write methods (especially small ones) — like anonymous methods.
- Makes code **short** and **clean**.
```
// Without Lambda
Runnable r1 = new Runnable() {
    public void run() {
        System.out.println("Running thread");
    }
};

// With Lambda
Runnable r2 = () -> System.out.println("Running thread");

```

---
**Functional Interface**
- An interface with **only ONE abstract method**.
- It is needed for **Lambda expressions** to work
```
@FunctionalInterface
interface MyFuncInterface {
    void display(); // Only one method
}

public class Test {
    public static void main(String[] args) {
        MyFuncInterface obj = () -> System.out.println("Hello Functional Interface!");
        obj.display();
    }
}

```
---
**Annotation**
- **Special tags** in Java that give extra information to the compiler or tools.
- To control behavior or simplify code.
```
@Override 
public String toString() {
    return "I am an object.";
}

@Deprecated
void oldMethod() {
    System.out.println("This method is old and not recommended.");
}

`@Override` tells compiler **"I am overriding a method"**.  
`@Deprecated` warns you **"Don't use this method anymore"**.

```
---
**Method Reference**
- A **shortcut** to call a method directly **without writing a lambda body**.
```
import java.util.function.Consumer;

public class Test {
    static void show(String s) {
        System.out.println(s);
    }

    public static void main(String[] args) {
        Consumer<String> c = Test::show; // Method reference
        c.accept("Hello Method Reference!");
    }
}

```

---
Stream Operations
- when you apply operations on stream of data like filtering, mapping, reducing, collecting etc.
- Makes **processing collections** easy and short.
```
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        numbers.stream()
               .filter(n -> n % 2 == 0)   // Keep only even numbers
               .forEach(System.out::println); // Print each number
    }
}

```
![[Pasted image 20250427233656.png]]


---
**Database Connectivity in Java**
**What is it?**

- JDBC = **Java Database Connectivity**
- It is a way for Java programs to **connect to a database**, **insert**, **update**, **delete**, and **read** data.

**Types of JDBC Drivers**

|Driver Type|Description|Notes|
|---|---|---|
|Type-1|JDBC-ODBC Bridge Driver|Old, not used anymore|
|Type-2|Native-API Driver|Needs database-specific libraries|
|Type-3|Network Protocol Driver|Connects via a middle server|
|Type-4|Thin Driver|**Direct** connection to database (MOST USED)|
![[Pasted image 20250427234756.png]]

**How to create connection with database**
```
1.First, add the MySQL JDBC jar file to your project
2.code below
import java.sql.*;

public class DBConnectExample {
    public static void main(String[] args) {
        try {
            // 1. Load driver class
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 2. Create connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/college", "root", "password");

            System.out.println("Connected to Database!");

            con.close(); // 3. Close connection
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

**CRUD Operations (Create, Read, Update, Delete)**

## a) **Create (Insert Data)**
```
Statement stmt = con.createStatement();
stmt.executeUpdate("INSERT INTO students (id, name) VALUES (1, 'Amit')");

```
b) **Read (Select Data)**
```
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM students");

while (rs.next()) {
    System.out.println(rs.getInt(1) + " " + rs.getString(2));
}

```
c) **Update (Change Data)**
```
Statement stmt = con.createStatement();
stmt.executeUpdate("UPDATE students SET name='Rahul' WHERE id=1");

```
d) **Delete (Remove Data)**
```
Statement stmt = con.createStatement();
stmt.executeUpdate("DELETE FROM students WHERE id=1");

```

---
**Model View Controller**
- it's a design pattern used for development of software's
-  An application is divided into three parts respectively Model, view, controller
- This separation helps in organizing code, making it easier to manage, test, and scale.

|Part|Meaning|Example|
|---|---|---|
|**Model**|Logic/Database|Java class that talks to database|
|**View**|UI/Front End|JSP, HTML, GUI|
|**Controller**|Brain|Java servlet or controller that connects model and view|
![[Pasted image 20250427235135.png]]

**How MVC Works in Project Development?**
Step 1: User requests a webpage (View).
Step 2: Controller processes the request.
Step 3: Model fetches required data.
Step 4: Controller sends data to View.
Step 5: View displays the response to the
user.

---
**Sequences (in Oracle Database)**
- Used to **auto-generate numbers** (like for **id fields**).
```
CREATE SEQUENCE student_seq
START WITH 1
INCREMENT BY 1;

```

When inserting:
```
INSERT INTO students(id, name) VALUES(student_seq.NEXTVAL, 'Amit');

```

---
**DUAL Table (Oracle only)**
- Its a dummy table and  used when you just want to **run calculations or functions** without using any real table.
- **DUAL** is a **special system table** created **by Oracle itself**.

```
SELECT SYSDATE FROM DUAL; <-This gives today's date.
```

It is used **internally** for quick operations like:
- Fetching **system date** (`SELECT SYSDATE FROM DUAL`)
- Doing **calculations** (`SELECT 2+2 FROM DUAL`)

Why can't we **DELETE** or **TRUNCATE** the default **DUAL** table?
- Because DUAL is a protected system table that Oracle uses internally, so you are not allowed to DELETE or TRUNCATE it.

If **you create your own DUAL table** (a copy), then **you can delete/truncate** **your own** DUAL —  because **only system DUAL** is protected.

```
CREATE TABLE my_dual AS SELECT * FROM DUAL;
DELETE FROM my_dual;  -- Allowed
TRUNCATE TABLE my_dual;  -- Allowed

```
---
**Data Type Management in Java and SQL**

| SQL Type | Java Type     |
| -------- | ------------- |
| INT      | int           |
| VARCHAR  | String        |
| DATE     | java.sql.Date |
| FLOAT    | float         |
| BOOLEAN  | boolean       |

---
- **A script is a small program** that tells the computer or web browser **what to do step-by-step.**
- A **script** is a set of **instructions** written in a simple programming language to **automate tasks** or **make things happen**.
```
<script>
  alert("Hello, World!");
</script>

```


## ⭐ Client-Side Scripting
- Runs **on the user's computer** (in the browser).
- Happens **after** the webpage is loaded.
- Mostly **makes the page interactive** (animations, forms, popups, etc.). 
- **Examples of client-side languages**:  
    ➔ JavaScript, HTML, CSS

### 📌 Example:
- You click a button ➔ JavaScript shows a popup immediately.
- **No need** to talk to the server again.


## ⭐ Server-Side Scripting
- Runs **on the server** (before the webpage is sent to the user).
- Happens **before** the page reaches the browser.
- Mostly **handles logic, databases, security**, etc.
- **Examples of server-side languages**:  
    ➔ Java, PHP, Python (Django, Flask), Node.js, Ruby, etc.
### 📌 Example:
- You log in ➔ Server checks your username and password in a database ➔ Then sends you the correct page (success or failure).


|Feature|Client-Side Scripting|Server-Side Scripting|
|---|---|---|
|Where it runs|In your browser (Chrome, etc.)|On the server (backend)|
|Example languages|JavaScript|Java, PHP, Python, Node.js|
|Main job|Make page interactive|Handle data, security, databases|
|When it happens|After page loads|Before page loads|
|Example|Popup after clicking a button|Checking login credentials|


Suppose you submit a login form
- **Client-side script**:  
    ➔ Quickly checks if you left the username field empty (without asking the server).
- **Server-side script**:  
    ➔ Checks if the username and password are correct inside a database.
---
- A **web application** is a **program** that you can **use through a web browser** (like Chrome, Firefox) by visiting a website. e.g. Gmail, fb, yt. 
- A **web server** is a **computer** that **stores** websites and **sends** them to your browser when you ask for them. When you visit `www.google.com`, a **web server** sends Google's homepage to you.

**mnemonics**
**Web server** = delivers the website  
**Web application** = the website you use

---
**CGI (Common Gateway Interface)**
- **CGI** is a way for a **web server** (like Apache) to **run programs (c/c++/pyhton/java** when a user sends a request (like filling a form and clicking submit).
- The **CGI program** takes **input** from the user, **processes it**, and then **gives output** (like HTML page) back to the browser.

Imagine you fill a form:

- Name: John
- Age: 22

When you click "Submit", the server **runs a CGI program** (maybe a Python file) which reads your **Name** and **Age**, and **responds** with a page like:

> "Hello John, you are 22 years old."



## How CGI Works (Step-by-Step):

1. User fills a form and submits it.
2. Web server sees that it needs to run a **CGI program**.
3. Server **starts the program**.
4. The program **reads data** (user input).
5. The program **processes data**.
6. The program **sends back an HTML page** to the browser.


**Note:**
- CGI is **slow** because **a new process** starts every time someone sends a request.
- Nowadays, faster technologies like **Servlets**, **JSP**, **PHP**, **Node.js** are used instead of CGI.
- But CGI was **one of the first** ways to make **dynamic websites** (websites that react to user input).

![[Pasted image 20250429005530.png]]

---
**Web Container**(**Apache Tomcat**)

Think of the **Web Container** as a **theater** and the **Servlet** as an **actor**.  
The **theater (Web Container)** manages everything — lights, sound, stage — and allows the **actor (Servlet)** to perform (process request and response).

- it's a environment where JSP and servlet runs and their req and res are handled

**Key Responsibilities**
- It loads **Servlets** when requested by the client.
- It manages the lifecycle of **Servlets**: initialization, handling requests, and destruction.
- It receives **HTTP requests** from the client (browser).
- It sends requests to the appropriate **Servlets** and **JSPs** for processing.
- It maps **URLs** (from client requests) to the corresponding **Servlets**. Example: `/login` might map to a `LoginServlet`.
- It manages **sessions** using cookies
- The web container can **forward** a request to another **Servlet** or **JSP** for further processing.
- It can **include** the response of another **Servlet/JSP** in the current one.
- It can handle **security configurations** (like user authentication and authorization) to control access to certain resources.


### **Web Container Life Cycle:**

1. **Initialization**: The container loads the **Servlet** (as per the `web.xml` or annotations).
2. **Request Handling**: It invokes the `service()` method of the **Servlet** (e.g., `doGet()` or `doPost()`).
3. **Destruction**: The container calls the `destroy()` method of the **Servlet** when it's shutting down or no longer needed.



![[Pasted image 20250429010613.png]]

---
# 🌟 Why do we need **Servlet** and **JSP**?

### 1. **Servlet** (Java Program)

- **Purpose**:  
    To **handle requests** (from browser) and **send responses** (back to browser) using Java code.
- **Example Work**:
    - Taking **form data** (like login form).
    - Connecting to **databases** (like MySQL).
    - Performing **calculations** or **business logic**.
- **Why needed**:  
    Without servlets, Java couldn't talk to web browsers directly.  
    Servlets made it possible to **create dynamic web applications** (not just static HTML pages).

### 2. **JSP** (Java Server Pages)

- **Purpose**:  
    To **make web pages** (HTML) **dynamic** by easily **embedding Java code** inside HTML.
- **Example Work**:
    - Displaying **user names** after login.
    - Showing **dynamic content** like products list from database.
- **Why needed**:  
    Writing **HTML** in a **Servlet** is **very messy** because you have to use `out.println("<html>")` again and again.  
    **JSP** makes it **easy** by allowing **HTML and Java** to be **mixed naturally**.

# Servlet lifecycle
- **Servlet** is a Java class that runs on a server and handles requests from web browsers process them and respond back.
- **Lifecycle Steps:**
1. **Loading and Instantiation**: Servlet class is loaded into memory.
2. **Initialization (`init()` method)**: Called once when servlet is created.
3. **Request Handling (`service()` method)**: Called every time a client sends a request.
4. **Destruction (`destroy()` method)**: Called when server shuts down or servlet is no longer needed.

![[Pasted image 20250429011218.png]]



```
public class MyServlet extends HttpServlet {
    public void init() {
        System.out.println("Servlet Initialized");
    }
    public void service(HttpServletRequest req, HttpServletResponse res) {
        System.out.println("Request handled");
    }
    public void destroy() {
        System.out.println("Servlet Destroyed");
    }
}

```


![[Pasted image 20250429005659.png]]

---
# Generic Servlet
- **GenericServlet** is a class that makes it easy to create servlets.
- It does **not care about HTTP** (just basic requests).
- We override the `service()` method.

```
public class A extends GenericServlet {
    public void service(A req, A res) {
        System.out.println("SimpleServlet handling request");
    }
}

```

---
**HTTP Servlet**
- **HttpServlet** is a special servlet for **web-based (HTTP)** requests.
- We override `doGet()` (for getting data) and `doPost()` (for sending data).

```
public class A extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        System.out.println("Handling GET request");
    }
}


```

---
## Linking Servlet to HTML

- Create a simple **HTML form**.
- Submit the form to the **servlet**.
- **In Servlet**, it handles the request.

HTML
```
<form action="MyServlet" method="get">
  <input type="text" name="username">
  <input type="submit" value="Submit">
</form>

```

Servlet
```
public class A extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        String name = req.getParameter("username");
        System.out.println("Name entered: " + name);
    }
}

```
When a user enters "Alice" and clicks submit:

- Browser will send a request like: `http://your-server/A?username=Alice`
- Your `doGet()` method runs.
- The server prints: `Name entered: Alice`


---
## HTTPServlet Request and Response

- **Request (`HttpServletRequest`)**: Reads data from the client (browser).
- **Response (`HttpServletResponse`)**: Sends data back to the client.
```
public void doGet(HttpServletRequest req, HttpServletResponse res) {
    String user = req.getParameter("user");
    res.setContentType("text/html");
    PrintWriter out = res.getWriter();
    out.println("<h1>Hello " + user + "</h1>");
}

```

---

**Servlet with JDBC**
- Use **JDBC** to connect Servlet with a **Database** 

```
public void doGet(HttpServletRequest req, HttpServletResponse res) {
    try {
        // Load MySQL JDBC Driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        
        // Connect to database
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password"
        );
        
        // Create Statement and Execute Query
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        
        // Print Result
        while (rs.next()) {
            System.out.println(rs.getString("name"));
        }
        
        // Close connection
        con.close();
    } catch (Exception e) {
        System.out.println(e);
    }
}


```
----
**JSP (Java Server Pages)**

- **Declare variables or methods**.
```
<%! int count = 0; %> <- variable declaration
<%! public int add(int a, int b) { return a + b; } %> <- method declartion

```

- JSP Directives: Give **Instructions** to JSP Engine like Importing Java classes.
```
<%@ page import="java.util.Date" %>
```

- JSP Scriptlets:**Write Java code inside JSP** page.
```
<%
    String user = request.getParameter("name");
    out.println("Hello " + user);
%>

```

- JSP Include Tag: **Include** another file into your JSP.
```
<jsp:include page="header.jsp" />
```

- JSP Page Tag: Set properties of the page (like language, error page etc.)
```
<%@ page language="java" contentType="text/html" pageEncoding="UTF-8"%>
```


**Note:**
- JSPs are **HTML pages with Java code** inside them.
- Servlet is **backend logic**, JSP is **frontend view**. 
---
**Web application directory structure**
![[Pasted image 20250429011322.png]]


---
## 1. ✨ `HttpServletRequest`

- Helps to **read** information from the **client request**.
- Some common methods:

|**Method**|**Purpose**|**Example**|
|---|---|---|
|`getParameter("name")`|Get **form field value**.|Get username from login form.|
|`getMethod()`|Get **HTTP method** (GET or POST).|Know how the form was submitted.|
|`getRequestURI()`|Get **requested URL path**.|Check which page user is asking for.|


## 2. ✨ `HttpServletResponse`

- Helps to **create and send** a **response** to the client.
- Some common methods:

|**Method**|**Purpose**|**Example**|
|---|---|---|
|`setContentType("text/html")`|Set type of response.|To tell browser it’s HTML.|
|`getWriter()`|Get object to **write response** (text/HTML).|Send HTML code to browser.|
|`sendRedirect("page.jsp")`|Redirect client to another page.|After successful login, move to dashboard.|


```
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class WelcomeServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // Get user input from form
        String name = request.getParameter("username");
        
        // Set content type and respond
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h1>Welcome, " + name + "!</h1>");
    }
}

```


---
#  literally Hate java from the bottom of my heart. Rust is way easier than Java

**What is Spring?
-  **Spring** is a **Java framework** that **helps you build powerful and organized Java applications** easily.  
- It gives ready-made tools, so you don't have to write everything from scratch.

![[0_qTIkBrhl90wcE6oK.png]]

Spring framework is organized into 20 modules which can again be grouped into Core Container, Web, Data Access/Integration, AOP, Aspect, Instrumentation, Messaging, and Test, as shown in the following image.
![[Pasted image 20250429015904.png]]

- This modular structure helps developers to use only the required modules without loading the whole framework.


---

**Spring IoC (Inversion of Control)**
- Normally, you create objects yourself using `new`.  
- In **Spring IoC**, the **container** (Spring Framework) **creates and manages objects** for you
🔵 You tell Spring **"I need an object like this"**,  
🔵 and Spring **gives you** that object when you need it.

---
**Dependency Injection (DI)**
- When an object **needs another object** to work, Spring **injects** (gives) it automatically.
- Spring handles it for you in the background.
- **Benefit:** You write **less code** and it becomes **easier to manage**.
- The objects managed by the container are called Spring Beans
- It manages the complete lifecycle of objects from creation to deletion




TODO: **How Spring Container Creates a Bean Object**

----
**What is Hibernate?**
- java tool helps in storing java  objects in database automatically
- No need to write boring SQL queries manually! Hibernate converts your Java classes into database tables. (This is called **ORM**.)
**ORM(Object Relational Mapping)**
- **ORM** means **mapping Java objects to database tables**. e.g. A Java `Student` class maps to a `student` table in MySQL.
**Hibernate Annotations**
- Instead of XML files, you can use **annotations** (like `@Entity`, `@Id`, etc.) directly in your Java code to define mapping.
```
@Entity
@Table(name = "student")
public class Student {
    @Id
    private int id;

    private String name;
}

```



![[Pasted image 20250429023609.png]]

---

## Hibernate Configuration

-  Hibernate needs a **configuration file** (usually `hibernate.cfg.xml`) to know:
- Which database to connect to (MySQL, Oracle, etc.)d
- Database username and password 
- Dialect (which SQL language version to speak)
- Mappings (classes ↔ tables)

---

**Hibernate CRUD operations**
- CRUD = **Create, Read, Update, Delete**

```
session.save(student);   // Create
session.get(Student.class, id);   // Read
session.update(student); // Update
session.delete(student); // Delete
```
---

**SessionFactory**
- It is like a **factory** that creates **Session** objects.
- **Session** = Hibernate's way to **talk to the database**.
- We use a `SessionFactory` to **get Sessions**.

---

**Transactions**
- When you want to **do multiple changes safely**, you use a **Transaction**.
- Make a group of DB changes **safe** and **atomic**
- **Atomic** means something that happens **completely** or **not at all** — no in-between.
- Example:
   - Insert data
   -  Update data
   -  If something fails, rollback everything.

**ACID Properties**

|Property|Meaning (in simple words)| Example                                                           |
| ------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
|**A - Atomicity**|All or nothing. A transaction must fully complete or fully fail.| Money transfer: ₹1000 either fully sent or not sent at all.       |
|**C - Consistency**|Data must always stay correct and follow all rules.| Balance must match before and after a transfer.                   |
|**I - Isolation**|Each transaction should run independently, without affecting others.| Two people booking the same seat won't clash.                     |
|**D - Durability**|Once a transaction is committed, it is permanently saved (even if system crashes).| After booking a ticket, it stays booked even after server restart 


**Trick**:
- **Atomicity** → "All or Nothing."
- **Consistency** → "Data remains valid."
- **Isolation** → "Transactions don't disturb each other."
- **Durability** → "Changes stay even after failures."


**Simple Hibernate code** showing how to use a **Transaction**:
```
// Import required Hibernate classes
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class Main {
    public static void main(String[] args) {
        // Step 1: Create a SessionFactory
        SessionFactory factory = new Configuration()
                                    .configure("hibernate.cfg.xml")
                                    .buildSessionFactory();
        
        // Step 2: Open a Session
        Session session = factory.openSession();
        
        try {
            // Step 3: Begin a Transaction
            Transaction tx = session.beginTransaction();
            
            // Step 4: Do some work (example: Save a Student object)
            Student s1 = new Student();
            s1.setId(1);
            s1.setName("John Doe");
            
            session.save(s1); // Saving object to database
            
            // Step 5: Commit the Transaction
            tx.commit();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Step 6: Close the Session
            session.close();
            factory.close();
        }
    }
}



Notes:
- `session.beginTransaction()` → Starts a new database transaction.
    
- `session.save(s1)` → Saves a new Student record into the database.
    
- `tx.commit()` → Confirms (finalizes) the changes into the database.
    
- If anything fails, Hibernate will throw an error, and you can handle it.
```

```
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.Table;

@Entity
@Table(name = "student")
public class Student {
    @Id
    private int id;
    private String name;

    // Getters and Setters
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```



# Common Hibernate Annotation 

| Annotation                | Meaning (Simple)                                             | Example                                               |
| ------------------------- | ------------------------------------------------------------ | ----------------------------------------------------- |
| `@Entity`                 | Marks a class as a **table** in the database.                | `@Entity public class Student`                        |
| `@Table(name="...")`      | Gives a **custom table name**.                               | `@Table(name="students")`                             |
| `@Id`                     | Marks a **primary key** field.                               | `@Id private int id;`                                 |
| `@GeneratedValue`         | Tells Hibernate to **auto-generate** primary key values.     | `@GeneratedValue(strategy = GenerationType.IDENTITY)` |
| `@Column(name="...")`     | Maps a field to a **specific column name**.                  | `@Column(name="student_name")`                        |
| `@OneToOne`               | Sets up a **1-to-1 relationship** between two tables.        | Example: One Student ↔ One Address                    |
| `@OneToMany`              | Sets up a **1-to-many relationship**. (One → Many)           | Example: One Teacher → Many Students                  |
| `@ManyToOne`              | Sets up a **many-to-one relationship**. (Many → One)         | Example: Many Students → One School                   |
| `@ManyToMany`             | Sets up a **many-to-many relationship**.                     | Example: Students ↔ Courses                           |
| `@JoinColumn(name="...")` | Defines the **foreign key** column name.                     | `@JoinColumn(name="address_id")`                      |
| `@Transient`              | Tells Hibernate to **ignore a field** (don't save it to DB). | `@Transient private int temp;`                        |

**Mnemonic**
- `@Entity` → Class is a Table
- `@Id` → Primary Key
- `@GeneratedValue` → Auto-Increment Key
- `@Column` → Column Name
- `@OneToOne`, `@OneToMany`, `@ManyToOne` → Relationships
- `@Transient` → Ignore Field



---

|Tightly Coupled|Loosely Coupled|
|---|---|
|Classes are hard-linked.|Classes depend on interfaces/abstractions.|
|Hard to change one part.|Easy to change or replace parts.|
|Difficult for testing.|Easy to test.|
|Not flexible.|Very flexible.|
|Example: Car creates PetrolEngine itself.|Example: Car gets any Engine (Petrol or Diesel) from outside.|
```
class PetrolEngine {
    void start() {
        System.out.println("Petrol engine started");
    }
}

class Car {
    PetrolEngine engine = new PetrolEngine();  // Directly creating PetrolEngine inside Car

    void startCar() {
        engine.start();
        System.out.println("Car started");
    }
}

Problem:
- Car is tightly connected to PetrolEngine.  
- If you want to use a DieselEngine, you have to **change the Car class code
```




---
# **Explain working of Spring and Hibernate**
# Spring

- **Spring** is like a **helper framework** that **manages your Java objects** for you.
- You don't need to manually create objects with `new` again and again.
- Spring **injects objects automatically** wherever needed (this is called **Dependency Injection**).
- It helps you **write less code**, manage everything smartly, and **connect different parts** of your app easily.
    
###  Example:

- You say: "Spring, I need a `StudentService`."
- Spring says: "Okay, here it is! Already created for you."

---

#  Hibernate 

- **Hibernate** is a **tool** that helps Java programs **talk to the database** easily.
- You don't need to write complicated **SQL queries**.
- You just create **normal Java classes** (like `Student`, `Teacher`), and Hibernate **saves/reads them** into database tables automatically.
- It uses **ORM** — Object-Relational Mapping (Java Object ↔ Table Row).

###  Example:
- You create a `Student` object and say: "Hibernate, please save this."
- Hibernate says: "Okay, I will insert it into the `students` table."

---

# How **Spring + Hibernate** work together

- **Spring** manages **the Java objects** (students, services, etc.).
- **Hibernate** manages **the database work** (save students, fetch students, etc.).
- Spring **injects** Hibernate's tools into your app **automatically**

---

#  Super Simple Flow:

1. You create a Java object (like `Student`).
2. Spring injects Hibernate’s session to you.
3. You tell Hibernate: "Save this student."
4. Hibernate talks to the database and saves it.