# Java 5 New Features

## Generics*
Generics allows you to parameterize classes, interfaces, and methods to provide compile-time type safety and reduce the need for explicit type casting.

### Advantages:
 - Type-safety
 - Typecasting not required
 - Compile-time checking

### Type parameters
1.  T - Type
2.  E - Element
3.  K - Key
4.  N - Number
5.  V - Value

### Some specific uses
 - Generic class (MyClass<T>)
 - Generic method (< E > void printArray(E[] elements))
 - Wildcard (? extends MyType)


 
    
## Enhanced for loop
The enhanced for loop, also known as the "for-each" loop, was introduced in Java 5. It provides a concise way to iterate over arrays and collections without the need for explicit indexing or iterators.
    
## Autoboxing and Unboxing
Java 5 introduced autoboxing and unboxing, which provide automatic conversion between primitive types and their corresponding wrapper classes. This simplifies code by eliminating the need for manual conversion between primitives and their wrapper classes.
    
## Enumerations
Java 5 introduced a new enum type, allowing you to define a set of named constants. Enumerations provide type safety and can be used in switch statements and collections.
    
## Varargs
Java 5 introduced the varargs feature, which allows methods to take a variable number of arguments of the same type. It simplifies method calls by eliminating the need to explicitly create an array for variable-length argument lists.
    
## Annotations
Java 5 introduced annotations, which are metadata that can be added to classes, methods, fields, and other program elements. Annotations provide a way to add additional information to the code and can be used by compilers, tools, and frameworks for various purposes.
    
## Enhanced concurrency support
Java 5 introduced the java.util.concurrent package, which provides high-level concurrency utilities such as thread pools, concurrent collections, and atomic variables. These utilities make it easier to write concurrent and multithreaded programs.
    
## Enhanced I/O support
Java 5 introduced the java.nio package, which provides enhanced I/O capabilities, including non-blocking I/O, scatter/gather I/O operations, and file system access improvements.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMjgyMjA2NiwxNDg2Njg5MzAxLC01OT
A4MTIxNTUsLTY2NDQ0NjY2MCwtMTY1NjEzMzk5M119
-->