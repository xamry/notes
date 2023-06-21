# Java 8 New Features

## Default and Static Methods in interfaces
From Java 8, interfaces are enhanced to have a method with implementation. We can use `default` and `static` keyword to create interfaces with method implementation. Default methods can be overriden while static methods can't.

## Functional Interfaces**
An interface with exactly one abstract method becomes a Functional Interface. We don’t have to use @FunctionalInterface annotation to mark an interface as a Functional Interface, but we should, in order to avoid accidental addition of abstract methods in the functional interfaces. Functional interfaces provide common **functional programming patterns**. Since functional interfaces have only one method, lambda expressions can easily provide the method implementation.
java.lang.Runnable with a single abstract method run() is a great example of a functional interface.
Java 8 introduced a set of functional interfaces, such as Predicate, Function, Consumer, and Supplier, in the `java.util.function` package.

Functional Interfaces are also called SAM (Single Abstract Method) interfaces.

## Lambda Expressions**
Lambda expressions introduced a concise syntax for defining anonymous functions. They enable **functional programming** by treating functions as first-class citizens, allowing the use of functional interfaces and enabling the use of functional programming constructs like streams.
    
## Stream API**
The Stream API `java.util.stream` provides a declarative way to process collections of data in a functional programming style. Streams allow you to perform operations like filtering, mapping, and reducing on collections with ease, making code more readable and concise.
    
## Optional:
The Optional class provides a way to handle potentially null values in a more expressive and safe manner. It encourages developers to explicitly handle cases where a value may be absent, reducing the likelihood of null pointer exceptions.
    
## Date/Time API:
Java 8 introduced the java.time package, which provides a comprehensive set of classes for working with dates, times, durations, and time zones. This new Date/Time API is more intuitive, thread-safe, and offers better performance than the old java.util.Date and java.util.Calendar classes.
    
## Method References: 
Method references allow you to refer to methods or constructors without invoking them explicitly. They provide a shorthand notation for lambda expressions and help in writing more concise and readable code.   
There are four variants of method references.

 1. ### Reference to a Static Method: `ContainingClass::methodName`
 2. ### Reference to an Instance Method: `containingInstance::methodName`
 3. ### Reference to an Instance Method of an Object of a Particular Type: `ContainingType::methodName`
 4. ### Reference to a Constructor: `ClassName::new`

    
## CompletableFuture: 
CompletableFuture is an enhanced version of the Future interface, providing better support for asynchronous programming. It allows chaining of dependent asynchronous tasks and provides methods for handling completion, exceptions, and combining multiple CompletableFuture instances.

## forEach() method in Iterable interface
Java 8 has introduced forEach method in `java.lang.Iterable` interface so that while writing code we focus on business logic. The forEach method takes `java.util.function.Consumer`object as an argument, so it helps in having our business logic at a separate location that we can reuse.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NTM2NDM0OTAsNDUxOTE4NDgwLC0xMj
MzMjg5NjUsLTIzOTAyMDIyOSwxMDU4NzE1NTk1LDMyNDM0MjE0
MSw3ODU3NjQ5MywtMTcwMzYyNTA1MSwzMzU3ODkzLC0xMTYzNz
Y1NzE3LC0xMzg5MDczMTk1LDg1MTc0NzQwMCwtMTgxNDAyMzU2
LC0xNzAyMTY1OTM5LDIwOTMxMDY2MjcsMTkwMDEwODY5MSwyMz
M1MDMwOTNdfQ==
-->