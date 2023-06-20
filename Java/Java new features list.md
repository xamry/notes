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

## New file system API (NIO 2.0)*

### Working with Path
A new `java.nio.file` package consists of classes and interfaces such as `Path`, `Paths`, `FileSystem`, `FileSystems` and others.

### File change notifications
The `WatchService` API lets you receive notification events upon changes to the subject (directory or file)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NjY4MzYwMDUsMTMzNzk4ODA1MCwtMT
E0ODUxMDM1Ml19
-->