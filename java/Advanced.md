# Advanced language knowledge and techniques

## Concurrency
Concurrency in Java is the ability to execute several tasks or processes simultaneously but independent of each other. It is achieved using threads and can be managed using various tools provided by the Java Concurrency API.

## Async Processing
Asynchronous processing in Java is a way of executing tasks concurrently, but not waiting for them to finish before moving on to other tasks. This can be achieved using the `CompletableFuture` class in Java.

## Debugging
Debugging in Java is the process of finding and resolving defects or problems within the program that prevent correct operation of computer software or a system.

## Profiling
Profiling in Java is a process that involves dynamic program analysis that measures, for example, the space (memory) or time complexity of a program, the usage of particular instructions, or the frequency and duration of function calls.

## Questions
1. What does Java have for concurrency?
2. How to access or modify a variable in a thread-safe way?
3. How to run a thread?
4. What is a thread pool and how does it work?
5. How to synchronize threads?
6. What are Callable and Futures?
7. What is a race condition and why do they happen? How to find and solve it?
8. What is thread starvation and how to solve it?
9. What are concurrent collections and how do they work?
10. How to profile a remote application?
11. Application fails with OOM. What to check and how to solve?

## Answers
1. Java provides a rich set of features for concurrency including threads, the `synchronized` keyword, locks, the `volatile` keyword, atomic variables, and the `java.util.concurrent` package.
2. You can access or modify a variable in a thread-safe way using `synchronized` blocks or methods, or by using classes from the `java.util.concurrent.atomic` package.
3. You can run a thread by creating a new instance of the `Thread` class and calling its `start` method.
4. A thread pool is a group of pre-instantiated, idle threads which stand ready to be given work. It is represented by the `ExecutorService` interface in Java.
5. You can synchronize threads using `synchronized` blocks or methods, locks from the `java.util.concurrent.locks` package, or by using `wait`, `notify`, and `notifyAll` methods.
6. `Callable` and `Future` are interfaces provided by Java that are used for computation that will be completed at some time in the future. A `Callable` returns a value and a `Future` provides methods to check if the computation is complete, to wait for its completion, and to retrieve the result of the computation.
7. A race condition occurs when two or more threads can access shared data and they try to change it at the same time. It can be prevented by ensuring that shared resources are locked while being accessed by a thread.
8. Thread starvation is a situation where a thread is unable to gain regular access to shared resources and is unable to make progress. This happens when shared resources are made unavailable for long periods by "greedy" threads. It can be mitigated by using a fair lock policy.
9. Concurrent collections in Java like `ConcurrentHashMap`, `CopyOnWriteArrayList`, etc., are designed to allow concurrent access to the collection and modifications of it without the need for external synchronization.
10. You can profile a remote application using profiling tools that support remote profiling, like VisualVM, YourKit, etc.
11. If an application fails with an OutOfMemoryError (OOM), you should first check the heap size settings. If the heap size is too small, you might need to increase it. If the heap size is sufficient, then you might have a memory leak in your application that you need to find and fix. You can use profiling tools to analyze memory usage.