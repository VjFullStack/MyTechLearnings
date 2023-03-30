## Q: What is an exception in Java?

A : 
An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions. When an exception occurs, the normal flow of the program is interrupted and the program tries to find a catch block that can handle the exception.
---
## Q: What are the different types of exceptions in Java?
A: 
There are two types of exceptions in Java: checked exceptions and unchecked exceptions. Checked exceptions are checked by the compiler at compile-time, and the programmer is required to handle them or declare that they might be thrown. Unchecked exceptions, on the other hand, are not checked by the compiler at compile-time, and can occur at runtime.
---
## Q: What is the difference between throw and throws in Java?
A: 
"throw" is a keyword in Java that is used to explicitly throw an exception. "throws" is used in the method signature to declare that the method might throw one or more exceptions. When a method throws an exception, the calling method is responsible for handling the exception.
---
## Q: What is the try-catch block in Java?
A: 
The try-catch block is used to handle exceptions in Java. The "try" block contains the code that might throw an exception, and the "catch" block contains the code that handles the exception. If an exception occurs in the "try" block, the program jumps to the corresponding "catch" block to handle the exception.
---
## Q: How do you handle multiple exceptions in Java?
A: 
You can handle multiple exceptions in Java by using multiple catch blocks. Each catch block handles a specific type of exception, and the catch blocks are arranged in the order of the most specific exception to the most general exception. Alternatively, you can use a single catch block with a multi-catch statement that handles multiple exceptions.
---
## Q: What is the finally block in Java?
A: 
The finally block in Java is a block of code that is executed after the try-catch block, regardless of whether an exception occurred or not. The finally block is typically used to release resources, such as closing a file or a database connection, that were acquired in the try block.
---
## Q: Can you explain the concept of custom exceptions in Java?
A: 
Custom exceptions are user-defined exceptions that are created by extending the Exception or RuntimeException class. Custom exceptions allow developers to create their own exceptions with a meaningful name and error message that are specific to their application. They can be thrown and caught like any other exception in Java.
---
