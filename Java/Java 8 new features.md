# Java 8 New Features

## Functional Interfaces**
Java 8 introduced a set of functional interfaces, such as Predicate, Function, Consumer, and Supplier, in the java.util.function package. These interfaces provide common functional programming patterns and enable lambda expressions and method references.

## Lambda Expressions**
Lambda expressions introduced a concise syntax for defining anonymous functions. They enable **functional programming** by treating functions as first-class citizens, allowing the use of functional interfaces and enabling the use of functional programming constructs like streams.
    
## Stream API**
The Stream API provides a declarative way to process collections of data in a functional programming style. Streams allow you to perform operations like filtering, mapping, and reducing on collections with ease, making code more readable and concise.
    
## Default and Static Methods in interfaces: 
Default methods, also known as defender methods or virtual extension methods, allow interfaces to have concrete method implementations. This feature enables backward compatibility for existing interfaces while allowing them to evolve by adding new methods.
    
## Optional:
The Optional class provides a way to handle potentially null values in a more expressive and safe manner. It encourages developers to explicitly handle cases where a value may be absent, reducing the likelihood of null pointer exceptions.
    
## Date/Time API:
Java 8 introduced the java.time package, which provides a comprehensive set of classes for working with dates, times, durations, and time zones. This new Date/Time API is more intuitive, thread-safe, and offers better performance than the old java.util.Date and java.util.Calendar classes.
    
## Method References: 
Method references allow you to refer to methods or constructors without invoking them explicitly. They provide a shorthand notation for lambda expressions and help in writing more concise and readable code.
    
## Parallel Streams:
Java 8 added the ability to easily parallelize operations on streams. By using parallel streams, developers can take advantage of multicore processors and distribute the workload across multiple threads to achieve better performance for computationally intensive tasks.
    
## CompletableFuture: 
CompletableFuture is an enhanced version of the Future interface, providing better support for asynchronous programming. It allows chaining of dependent asynchronous tasks and provides methods for handling completion, exceptions, and combining multiple CompletableFuture instances.

## forEach() method in Iterable interface
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NTk0NzU4NDcsLTE3MDIxNjU5MzksMj
A5MzEwNjYyNywxOTAwMTA4NjkxLDIzMzUwMzA5M119
-->