# Goroutine

Goroutines are a fundamental feature of GoLang, providing a lightweight and efficient means of handling concurrent
operations. They are one of the primary reasons for Go's popularity in network programming and concurrent applications.

In Go, a goroutine is a lightweight thread managed by the Go runtime. All Go programs start as a single process, and at
least one goroutine is created to execute the main function.

**Lightweight Threads**

Goroutines are lightweight threads managed by the Go runtime. They are much more lightweight compared to OS threads,
both in terms of memory overhead and setup/teardown time.

**Concurrency Model**

GoLang uses a M:N threading model where M goroutines are multiplexed over N OS threads. The Go runtime schedules these
goroutines onto the available threads for execution, handling the details like thread creation and switching.

**Creating Goroutines**

A goroutine is created simply by prefixing a function call with the `go` keyword. This launches the function
asynchronously.

**[Synchronization](#synchronization)**

Synchronization between goroutines can be achieved using channels or synchronization primitives from the `sync`
package like `WaitGroup`, `Mutex`, etc.

**[Channels](../core/collections.md#channels-special-use-cases)**

Channels in Go are used for communication between goroutines and can be thought of as pipes using which goroutines
communicate.

**Main Function Flow**

The `main` function is the entry point of a Go program. It runs in its own goroutine. When `main` returns, the program
exits. Other goroutines can be spawned from the main function or from any other
goroutine.

**Parallel Execution**

While the `main` function is essential, a significant feature of Go is the ability to concurrently run functions as
goroutines, enabling parallel execution.

## Synchronization

In Go, goroutines are lightweight threads managed by the Go runtime. Synchronizing them is crucial for coordinating
access to shared resources and ensuring correct program execution. Go provides several mechanisms for synchronization,
primarily through the `sync` and `atomic` packages.

### Using `atomic` Package

The `atomic` package provides low-level atomic memory primitives useful for implementing synchronization algorithms.

1. **Atomic Operations:**
   Atomic operations include `Load`, `Store`, `Add`, `CompareAndSwap`, etc., which are used for atomic manipulation of
   variables.

   **Example:**
   ```go
   var count int32

   func increment() {
       atomic.AddInt32(&count, 1)
   }

   func getCount() int32 {
       return atomic.LoadInt32(&count)
   }
   ```

2. **Use Cases:**
   Atomic operations are generally used for small operations like incrementing a counter, where the overhead of mutex
   locking is not justified. They are also useful in scenarios where you need to perform non-blocking updates to a
   value.

### Choosing Between `sync` and `atomic`

- **Use `sync`** for higher-level synchronization (e.g., locking, signal/wait mechanisms). It's more straightforward and
  idiomatic in Go for most common use cases.
- **Use `atomic`** for low-level, lock-free programming, particularly when you're dealing with simple atomic counters or
  state flags. It's more performant but requires a deeper understanding of memory ordering constraints.

Both packages play a crucial role in writing concurrent Go programs, and their usage depends on the specific
requirements and complexity of the task at hand.

## Best Practices

- **Avoid Excessive Goroutines**: While goroutines are cheap, creating an excessive number can still lead to performance
  issues. It's essential to balance concurrency needs with system resources.
- **Synchronize Access to Shared Data**: Use mutexes or other synchronization methods to manage access to shared
  resources.
- **Graceful Goroutine Termination**: Ensure goroutines terminate gracefully, especially when dealing with network
  connections or other resources.
- **Proper Error Handling**: Errors in goroutines should be properly handled, typically via channel-based communication.

## Example: Basic Goroutine and Channel Communication

```go
package main

import (
    "fmt"
    "time"
)

func printNumbers(c chan int) {
    for i := 1; i <= 5; i++ {
        c <- i // Send number to channel
        time.Sleep(1 * time.Second)
    }
    close(c) // Close the channel
}

func main() {
    c := make(chan int)
    go printNumbers(c) // Start goroutine

    for num := range c {
        fmt.Println("Received:", num)
    }
}
```

In this example, `printNumbers` is executed as a goroutine. It communicates with the main function through a
channel `c`. This illustrates basic asynchronous execution and inter-goroutine communication.

## Threads vs. Goroutines

Understanding the difference between threads (as used in many programming languages) and goroutines (specific to GoLang)
is crucial for effective concurrent programming in Go. s

**OS Threads**

Traditional threads are managed by the operating system.

Each thread has its own stack, and switching between threads involves significant overhead due to context switching.

**Goroutines**

Goroutines are managed by the Go runtime, not the operating system.

They are much more lightweight than threads in terms of memory and setup/teardown overhead.

Multiple goroutines can be multiplexed onto a smaller number of OS threads by the Go scheduler.

**Stack Size**

OS threads typically have a fixed stack size (often quite large).

Goroutines start with a small stack that grows and shrinks as required.

**Scheduling**

Threads are preemptively scheduled by the OS.

Goroutines are cooperatively scheduled by the Go runtime. This means the Go runtime controls the scheduling of
goroutines, which includes determining when a goroutine should yield to another.

**Concurrency Model**

Threads are part of a multi-threading model, where concurrency is achieved by running multiple threads possibly on
multiple CPUs.

Goroutines are part of GoLang's concurrency model, which emphasizes simplicity and efficiency, making it easier to write
concurrent programs.

#### Best Practices

- **Use Goroutines for Concurrency in Go**: They are a core part of the language and are designed to be simple,
  efficient, and integrated with Go’s other features like channels.
- **Manage Goroutine Lifecycle**: Always ensure that goroutines exit properly and do not leave hanging goroutines.
- **Avoid Excessive Goroutines**: While lightweight, they still consume resources. Balance the number of goroutines with
  the workload and system capabilities.
- **Prefer Channels for Synchronization**: Channels in Go are a powerful way to synchronize and communicate between
  goroutines.

#### Example: Comparing Goroutines

```go
package main

import (
    "fmt"
    "time"
)

func task(id int) {
    for i := 0; i < 5; i++ {
        fmt.Printf("Task %d: %d\n", id, i)
        time.Sleep(time.Second)
    }
}

func main() {
    for i := 0; i < 3; i++ {
        go task(i) // Launching a goroutine
    }

    time.Sleep(5 * time.Second) // Wait for goroutines to finish
}
```

In this example, three goroutines run concurrently. Each goroutine prints its id and a counter. This simple
demonstration showcases the ease of using goroutines for concurrent tasks.

#### Conclusion

Goroutines are a more lightweight and flexible alternative to traditional threads, offering efficient concurrency
management with less overhead. They are a fundamental part of GoLang's design, making concurrent programming more
accessible and scalable. By leveraging goroutines and channels, GoLang developers can build highly concurrent systems
that are easier to understand and maintain compared to traditional multithreaded applications.

## Conclusion

Goroutines are a cornerstone of Go's approach to concurrency and parallelism. They enable efficient and straightforward
concurrent programming, allowing Go programs to handle multiple tasks simultaneously in a scalable way. Proper use of
goroutines, along with effective synchronization and error handling strategies, can lead to the development of
high-performance and responsive applications.