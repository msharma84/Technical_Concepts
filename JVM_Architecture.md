# JVM Architecture

The Java Virtual Machine (JVM) is an integral part of the Java ecosystem, responsible for executing Java bytecode.

## Class Loader Subsystem

ClassLoader subsystem is a critical part of the Java runtime environment. It enables dynamic loading of classes, maintains class loading isolation, and ensures that the appropriate classes and resources are available for a Java application to execute. Class loading in Java occurs in three distinct phases:

a) **Loading:** This is the first phase where the class loader loads the class file into memory. It typically involves reading the class file from the file system or another source.

Class Loader Hierarchy: Java uses a hierarchical class loading system with the following key class loaders:

* **Bootstrap Class Loader:** This is the top-level class loader, which is responsible for loading core Java libraries and classes from the Java Standard Library (e.g., java.lang, java.util). It’s typically implemented in native code and is not written in Java. Classes loaded by the bootstrap class loader are considered trusted and part of the core runtime environment.
* **Extension Class Loader:** Also known as the Extension Class Loader, this loader loads classes from the extension directories or JAR files. These are classes that extend the core Java API.
* **Application Class Loader:** This class loader loads classes from the application’s classpath. It’s responsible for loading the classes that are part of the application. Custom class loaders can also be created to load classes from custom sources.

b) **Linking:** This step ensures that the loaded class files are valid and do not violate Java Virtual Machine constraints.

* **Verification:** In this step, the JVM checks the loaded class for proper structure and adherence to Java specifications. It ensures the bytecode is well-formed and doesn’t violate any safety constraints.
* **Preparation:** Memory is allocated for class variables and initialized to default values during preparation.
* **Resolution:** This step involves replacing symbolic references with direct references. For example, resolving a method call to a specific method in a class.

c) **Initialization:** In this phase, the class’s static initializers and static blocks are executed. This is when the class is effectively “initialized.”

## Runtime Data Areas

This region of memory is used to manage and store various data during the execution of a Java program.

a) **Method Area (Method Space):**

* The Method Area, also known as the Method Space, is a logical part of memory where the JVM stores class-level data and metadata.
* It stores information about classes, such as field and method names, their data types, and access modifiers. This area also contains the runtime constant pool, which is a table of symbolic references to methods, fields, and other runtime constants.
* The Method Area is shared among all threads and is a crucial part of maintaining Java’s type and method integrity.
* This area is generally a fixed size, and it can trigger an OutOfMemoryError if it’s exhausted.

b) **Heap:**

The Heap is the runtime data area responsible for storing objects and their associated data. It is where the dynamic memory allocation for objects occurs.

The Heap is divided into two main regions: Young Generation and the Old Generation.

* **Young Generation:** This is where new objects are created. It’s further divided into three regions: Eden Space and two Survivor Spaces (S0 and S1). Objects are initially created in Eden Space. When objects survive one or more garbage collection cycles, they may be promoted to the Survivor Spaces.
* **Old Generation (Tenured Generation):** This area stores long-lived objects that have survived several garbage collection cycles in the Young Generation.
The garbage collector automatically manages the Heap to reclaim memory from no longer reachable objects. When the Heap is exhausted, it can lead to an OutOfMemoryError.

c) **Java Stacks:**

* Each thread in a Java application has its own Java Stack, used for method call execution and managing local variables.
* The Java Stack is organized as a stack of stack frames, each representing a single method call. It includes the method’s local variables, return value, and address (the address to which the method should return after execution).
* The stack ensures that methods execute in a last-in, first-out (LIFO) manner, and it is an essential part of thread execution.

d) **Native Method Stacks:**

* Similar to the Java Stack, the Native Method Stack is used to execute native methods or methods written in languages other than Java (e.g., C or C++).
* Native methods are executed on the native method stack, and it is separate from the Java Stack to maintain isolation between native code and Java code.

e) **Program Counter (PC) Register:**

* Each thread has its own Program Counter Register, which stores the memory address of the currently executing JVM instruction.
* It’s a small, thread-local area that keeps track of the execution point within the currently executing method.

## Execution Engine

It is responsible for responsible for executing Java bytecode. It interprets and/or compiles bytecode into native machine code, facilitating the actual execution of Java applications.

a) **Interpreter:**

* The interpreter is the fundamental component of the Execution Engine. It reads bytecode instructions line by line and executes them.
* Bytecode is a platform-independent representation of Java code, and the interpreter ensures that Java programs can run on any platform with a compatible JVM.
* Interpretation is relatively slow compared to native code execution, but it provides platform independence and allows code to run on any system with a JVM.

b) **Just-In-Time (JIT) Compiler:**

* While the interpreter is essential for platform independence, it is often slow for performance-critical applications. This is where the JIT compiler comes into play.
* The JIT compiler is responsible for converting bytecode into native machine code, which is executed directly by the host CPU.
* The JIT compiler dynamically compiles bytecode into native code at runtime, optimizing the performance of the Java application.
* JIT compilation is done selectively for methods that are frequently executed, known as “hot” methods. This helps to save compilation time and resources.
* The JIT compiler can apply various optimizations, such as method inlining, dead code elimination, and loop unrolling, to make the native code execution more efficient.

c) **Execution of Bytecode:**

* The Execution Engine fetches bytecode instructions from the method area and executes them in the order specified.
* It maintains the program counter (PC) register to keep track of the current instruction.
* Execution includes loading and storing data, performing arithmetic operations, calling methods, and managing control flow (e.g., loops, conditionals).
  
d) **Native Interface:**

* The Native Interface allows Java code to interact with native libraries and languages such as C and C++.
  
e) **Native Method Libraries:**

* This is where native libraries are stored. These libraries are often written in C and C++ and can be called by Java code using the Native Interface.
f) Execution of Java Code:

The JVM executes Java bytecode by fetching instructions, decoding them, and executing the corresponding operations.
The execution engine interacts with the runtime data areas and controls the flow.
g) Garbage Collection: The JVM automatically manages memory, including garbage collection, to free up memory occupied by objects no longer referenced.

h) Java Native Interface (JNI): It allows Java code to call native code and vice versa, enabling interaction with platform-specific libraries.
