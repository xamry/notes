# Java 5 New Features

## GenericsJava 5 introduced generics, which allow you to parameterize classes, interfaces, and methods to provide compile-time type safety and reduce the need for explicit type casting. Generics enable the creation of type-safe collections and improve code readability.
    
2.  Enhanced for loop: The enhanced for loop, also known as the "for-each" loop, was introduced in Java 5. It provides a concise way to iterate over arrays and collections without the need for explicit indexing or iterators.
    
3.  Autoboxing and Unboxing: Java 5 introduced autoboxing and unboxing, which provide automatic conversion between primitive types and their corresponding wrapper classes. This simplifies code by eliminating the need for manual conversion between primitives and their wrapper classes.
    
4.  Enumerations: Java 5 introduced a new enum type, allowing you to define a set of named constants. Enumerations provide type safety and can be used in switch statements and collections.
    
5.  Varargs: Java 5 introduced the varargs feature, which allows methods to take a variable number of arguments of the same type. It simplifies method calls by eliminating the need to explicitly create an array for variable-length argument lists.
    
6.  Annotations: Java 5 introduced annotations, which are metadata that can be added to classes, methods, fields, and other program elements. Annotations provide a way to add additional information to the code and can be used by compilers, tools, and frameworks for various purposes.
    
7.  Enhanced concurrency support: Java 5 introduced the java.util.concurrent package, which provides high-level concurrency utilities such as thread pools, concurrent collections, and atomic variables. These utilities make it easier to write concurrent and multithreaded programs.
    
8.  Enhanced I/O support: Java 5 introduced the java.nio package, which provides enhanced I/O capabilities, including non-blocking I/O, scatter/gather I/O operations, and file system access improvements.

# Java 7 New Features

## String in Switch
We can now use strings in the switch statement. Earlier, only primitive types and enumerated types were allowed as switch expressions.

## Diamond Operator
Also called type inference for generic instance creation. It allows you to omit the type parameters when creating an instance of a generic class if the compiler can infer the type from the context.

## Try-with-resources (Automatic resource management)
You can declare resources within the try statement, and the JVM will automatically close those resources when they are no longer needed, even if an exception occurs. The resources that should be auto closed must implement `java.lang.AutoCloseable interface

## Improved Exception Handling
Multi-catch blocks allow you to catch multiple exceptions in a single catch block, reducing code duplication.

## Binary Literals and Underscores in Numeric Literals
We can specify binary literals using the prefix "0b" or "0B". Also, we can use underscores in numeric literals to improve readability. For example, you can write large numbers as 1_000_000 instead of 1000000.

## Fork/Join Framework**
Ths framework provides support for parallel programming by allowing efficient task decomposition and work distribution across multiple processor cores. 
The core classes supporting the Fork-Join mechanism are `ForkJoinPool` and `ForkJoinTask`. The `ForkJoinPool` is basically a specialized implementation of `ExecutorService` implementing the  **work-stealing_ algorithm**.

## New file system API (NIO 2.0)*

### Working with Path
A new `java.nio.file` package consists of classes and interfaces such as `Path`, `Paths`, `FileSystem`, `FileSystems` and others.

### File change notifications
The `WatchService` API lets you receive notification events upon changes to the subject (directory or file)

## Other improvements
### Dynamism support
Java is a statically typed language, as against dynamically typed languages such as Ruby, Python and Clojure. A new feature called **invokedynamic** in Java 7 extends the support of dynamic languages.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3Mzg2NzA0MjEsMTEyMDYzNTM4MCwtMT
A4NzEzODMwLC0xNTY2ODM2MDA1LDEzMzc5ODgwNTAsLTExNDg1
MTAzNTJdfQ==
-->