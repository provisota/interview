# Questions

1. What is the difference between `Array` and `Slice` and their usecases?
2. What is pointer? What is value? What are key differences between them?
3. Which visibility scopes do you know? How implement closure?
4. What are interfaces and their usecases?
5. What is empty interface, and its usecases?
6. What data types can serve as map keys?
7. Explain the difference between error handling and panic? When to use each? Is it possible to proceed when panic
   occurs?
8. How can you hide (encapsulate) implementation details?
9. What are struct tags and their usecases?
10. Can you describe what is context and its usecases?
11. What is GC and how it works in Go?
12. How data is carried in function/method calls (input, return arguments)?
13. How interfaces are implemented under the hood?
14. Usecases for unsafe code?
15. What is escape analysis and how to do it?

# Answers

1. An array has a fixed size, while a slice is dynamic. Arrays are useful when the number of elements is known ahead of
   time, while slices are more flexible and can grow as needed.
2. A pointer stores the memory address of a value, while a value is the data itself. Pointers allow for indirect
   manipulation of values and sharing of values, while values are used for direct manipulation.
3. Go has block scope, function scope, and package scope. A closure is a function that references variables from outside
   its body.
4. Interfaces define a set of methods. Any type that implements those methods satisfies the interface. They are used for
   achieving polymorphism and decoupling dependencies.
5. An empty interface can hold values of any type. It's often used when the type of value is not known or can vary.
6. Any type that is comparable (can be used with the == operator) can serve as a map key. This includes basic types like
   int and string, as well as arrays and structs.
7. Error handling is done by returning and checking for errors. Panic is used to halt the program when an unrecoverable
   error occurs. It's generally recommended to use error handling over panic.
8. Encapsulation is achieved through the use of packages and the exportation rules of Go.
9. Struct tags are string annotations in struct fields. They are often used with the reflection package to provide
   additional information about the fields.
10. The context package is used to carry request-scoped values, cancellation signals, and deadlines across API
    boundaries and between processes.
11. Garbage Collection (GC) is an automatic memory management system that frees up memory that is no longer in use. In
    Go, GC is concurrent and has low latency.
12. Data is carried in function/method calls through input parameters and return values.
13. Interfaces are implemented implicitly in Go. Under the hood, an interface value holds a pair: the concrete value
    assigned to the interface, and that value's type descriptor.
14. The unsafe package allows for bypassing Go's type safety. It's generally recommended to avoid using it unless
    absolutely necessary.
15. Escape analysis determines whether a variable can be safely allocated on the stack instead of the heap. It's done by
    the compiler.