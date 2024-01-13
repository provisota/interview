# Go Runtime/Scheduler

The Go runtime scheduler is a key component of GoLang's concurrency model. It manages the execution of goroutines, Go's
lightweight and independently executing functions.

**M:N Scheduling**

Go's scheduler implements M:N scheduling, where M goroutines are multiplexed onto N OS threads. This allows many more
goroutines than the number of available threads.

**Goroutines**

Goroutines are the basic unit of execution in Go. They are much lighter than OS threads, typically requiring less memory
and overhead to create and switch between.

**Non-blocking I/O**

The Go scheduler is integrated with [Go's network poller](#go-network-poller), allowing goroutines to block on I/O
without blocking the underlying thread, thereby freeing it to run other goroutines.

**Cooperative Scheduling**

Goroutines are cooperatively scheduled. This means that a goroutine keeps running until it voluntarily yields control,
usually by performing a blocking operation like I/O, synchronization, or calling `runtime.Gosched()`.

## Go Network Poller

Go's network poller is an internal feature of the Go runtime that efficiently manages network I/O operations, allowing
goroutines to block on network I/O without blocking the entire operating system thread. This is a key part of Go's
concurrency model and its ability to handle a large number of concurrent network connections efficiently.

### Overview

1. **Non-Blocking I/O**: Go's network poller uses non-blocking I/O operations under the hood. When a goroutine performs
   a network I/O operation (like reading from a TCP connection), it doesn't block the entire thread. Instead, if the I/O
   operation cannot be completed immediately (for instance, if no data is available for a read operation), the goroutine
   is paused, and the thread is freed up to run other goroutines.

2. **OS Integration**: The network poller integrates closely with the operating system's event notification mechanisms (
   like epoll on Linux, kqueue on BSD, and IOCP on Windows). These mechanisms notify the poller when I/O operations on
   file descriptors (like sockets) are ready to proceed.

3. **Goroutine Resumption**: When the network poller receives a notification that an I/O operation can proceed, it
   schedules the corresponding goroutine for execution. The goroutine then resumes as if it had been blocked, but
   without having tied up an OS thread while waiting.

### Benefits

- **Efficiency**: This model is much more efficient than having one OS thread per connection, which is a traditional
  model in many other languages and frameworks. It allows Go programs to scale to handle tens of thousands of concurrent
  connections with minimal overhead.

- **Simplicity**: From a programmer's perspective, network I/O in Go still looks like synchronous, blocking operations.
  This makes it much easier to write and understand than explicitly asynchronous I/O code, as seen in other languages.

### Example Usage

When writing Go code that performs network operations, you don't need to do anything special to take advantage of the
network poller. It's automatically used by standard library functions like `net.Dial`, `net.Listen`, and methods
on `net.Conn` objects.

```go
conn, err := net.Dial("tcp", "example.com:80")
if err != nil {
    log.Fatal(err)
}
defer conn.Close()

// Use conn for network I/O; the network poller automatically manages the I/O operations
```

### Limitations

- **File I/O**: The network poller is optimized for network I/O and doesn't handle file I/O. File I/O in Go is blocking
  at the thread level.

- **Custom Schedulers**: Since the network poller is an internal part of the Go runtime, it's not something that can be
  easily replaced or customized.

The Go network poller is a great example of how Go's runtime and standard library work together to make concurrent
programming more efficient and easier for developers. It abstracts away the complexities of non-blocking I/O,
epoll/kqueue/IOCP, allowing developers to focus on the logic of their applications.

## How the Go Scheduler Works

The Go scheduler is a key component of Go's runtime system, enabling the language's powerful concurrency model. It's
responsible for distributing Go's goroutines over available CPU cores for execution. Unlike traditional operating system
schedulers, the Go scheduler is designed specifically to work with goroutines, which are much lighter than OS threads.

### Key Concepts

1. **Goroutines**: These are lightweight threads managed by the Go runtime, not the OS. They are much cheaper to create
   and destroy compared to OS threads.

2. **M (Machine)**: Represents an OS thread. M executes Go code and needs a P to execute Go code.

3. **P (Processor)**: A resource that holds a context for executing Go code. It's a logical construct that determines
   the number of OS threads that can execute user-level Go code simultaneously.

4. **G (Goroutine)**: A goroutine waiting to be executed.

### How the Scheduler Works

1. **M-P-G Relationship**: The scheduler maps `M`s to `P`s to execute `G`s. Each `P` can have multiple `G`s queued up
   for execution, and the scheduler assigns these `G`s to an `M` for execution. A single `M` can only execute one `G` at
   a time.

2. **Work Stealing**: When an `M` finishes executing a `G`, it needs a new `G` to execute. It first looks in its local
   run queue (attached to its `P`). If it finds a `G` there, it executes it. If not, it tries to steal a `G` from
   another `P`'s run queue.

3. **Syscall and I/O Handling**: When a `G` makes a syscall or gets blocked in I/O, its `M` is detached and can pick up
   another `G` to execute. This ensures that other `G`s can execute while one is waiting for I/O or syscalls. The `G`
   blocked in I/O or syscall is later picked up by a different `M`.

4. **Synchronization and Preemption**: To keep all CPUs utilized and to ensure that no single `G` hogs the CPU, the
   scheduler periodically checks and preempts long-running `G`s. This is done every few milliseconds (as of Go 1.14,
   it's done using asynchronous preemption).

5. **Netpoller Integration**: For network I/O, Go's netpoller can put `G`s to sleep without occupying an `M`, and wake
   them up when I/O is ready, at which point they get scheduled again.

### Scheduler Design Philosophy

- **Concurrency with Lightweight Goroutines**: By making goroutines cheap to create and manage, Go allows for easy
  concurrency.

- **Efficient with CPU and Memory**: By using a small number of OS threads and managing goroutines efficiently, Go
  programs can run with less memory and CPU overhead compared to traditional threading models.

- **Fairness and Responsiveness**: The work-stealing algorithm and preemption ensure that no goroutine is starved and
  that all get a chance to run.

- **Simplicity**: From a developer's standpoint, the scheduler's complexities are hidden. You write straightforward
  concurrent code with goroutines and channels, and the scheduler takes care of the rest.

### Example Usage

When you write Go code, you don't interact directly with the scheduler. You simply start goroutines:

```go
go func() {
    // some work
}()
```

The scheduler handles the execution of this goroutine alongside others, balancing them across available threads and
cores.

### Conclusion

Go's scheduler is a powerful abstraction layer that allows developers to write concurrent code without having to deal
with the complexities of thread management or CPU-bound scheduling. Its design promotes efficient and scalable
concurrency, making Go a strong choice for high-concurrency applications.

## Goroutine States

Goroutines in Go can be in several different states during their lifecycle. Understanding these states is crucial for
grasping how Go's concurrency model and scheduler work. Here are the primary states a goroutine can be in:

### 1. Runnable

In this state, the goroutine is ready to run but is not currently executing. Runnable goroutines are waiting in a queue
for a turn to be scheduled on an available thread (M).

A goroutine that has just been created is in the runnable state. It's also the state a goroutine re-enters after being
unblocked or when it yields the processor.

### 2. Executing

The goroutine is currently executing on a thread (M). Only one goroutine can execute on a single thread at any given
time.

This is the state when a goroutine's code is actively running.

### 3. Waiting (Blocked)

The goroutine is in a waiting state and not doing any work. This state occurs when the goroutine is blocked, waiting for
some event (like I/O operation completion, channel send/receive operation, waiting on mutex, etc.).

Common examples include waiting for data from a network connection, waiting for a timer, or waiting for another
goroutine to send data on a channel.

### 4. Sleeping

Similar to waiting, but it specifically refers to goroutines that are paused for a set amount of time.

A goroutine goes into a sleeping state when it calls `time.Sleep` or when a timer is set.

### 5. Dead

The goroutine has finished its execution and is no longer active.

This state is reached after a goroutine successfully completes its work and exits or if it exits prematurely due to an
unhandled error.

### 6. Suspended (or Preempted)

In newer versions of Go (especially since Go 1.14), a running goroutine can be preempted to prevent it from monopolizing
the thread. The scheduler might suspend a goroutine that has been running for too long to give other goroutines a chance
to run.

This state is part of Go's strategy to improve fairness and prevent long-running goroutines from causing starvation of
other goroutines.

### Understanding Goroutine States

- **Transitioning Between States**: Goroutines switch between these states during their lifecycle, managed by the Go
  scheduler.
- **Visibility to Developers**: These states are mostly abstracted away from the developer. You don't typically manage
  these states directly in your Go code; instead, you focus on the logic of goroutines and channels.
- **Debugging and Profiling**: Understanding these states is helpful during debugging and performance profiling, as they
  can provide insights into concurrency issues, bottlenecks, or performance problems in Go programs.

The Go scheduler efficiently manages these states, abstracting much of the complexity away from the programmer, allowing
focus on the concurrent logic of the application rather than on low-level threading and synchronization details.

## Goroutine Scheduling

Goroutine scheduling in Go is handled by the Go runtime scheduler, which is a part of the Go runtime. This scheduler is
different from traditional thread schedulers found in operating systems. Its main purpose is to distribute Goroutines -
the lightweight, user-space threads in Go - across available OS threads in an efficient manner.

### Key Principles of Goroutine Scheduling

1. **M:N Scheduling**: The Go runtime implements M:N scheduling, which multiplexes `M` goroutines onto `N` OS threads.
   This allows efficient use of system resources, as goroutines are much lighter than threads, both in terms of memory
   overhead and context switching costs.

2. **Goroutines (G)**: These are the entities that run Go code. They are lightweight and cheap to create and destroy.

3. **Machine (M)**: Represents an actual OS thread. M executes Go code or Go's runtime code.

4. **Processor (P)**: A resource that represents the capability to execute Go code. It holds the context required for
   executing goroutines and has a local run queue of goroutines.

### Scheduling Process

1. **Assignment of P to M**: When an OS thread (M) is initialized, it acquires a P. The P maintains a local run queue of
   goroutines that are ready to be executed.

2. **Executing Goroutines**: M takes a goroutine (G) from the run queue of its P and executes it.

3. **Syscall and Blocking Calls**: If a goroutine makes a blocking syscall or gets blocked in some other way (like
   channel operations), the P is detached from M, and M is either parked or gets a new P to continue executing other
   goroutines. This ensures that system calls or blocking operations don’t stall the execution of other goroutines.

4. **Work Stealing**: If an M finds its local run queue empty, it tries to steal goroutines from other P's run queue.

5. **Preemption**: Since Go 1.14, goroutines are preemptible. This means that a goroutine that's running for too long
   can be stopped in the middle of its execution to allow other goroutines to run. This prevents a single goroutine from
   monopolizing the CPU.

6. **Network Poller**: The Go scheduler integrates with a network poller to efficiently handle I/O operations.
   Goroutines waiting for I/O are parked in such a way that they don’t consume any CPU resources.

### Scheduling in Practice

- When writing Go code, you don't interact directly with the scheduler. You simply start goroutines using the `go`
  keyword.
- The scheduler handles the complexity of managing goroutines, allowing you to focus on the application logic.

### Considerations

- **Concurrency vs. Parallelism**: While the scheduler enables concurrency (multiple goroutines executing in an
  interleaved manner), parallel execution depends on having multiple threads (M) running on multiple CPU cores.
- **Tuning**: You can control the number of system threads that execute user-level Go code by setting the `GOMAXPROCS`
  variable. By default, it's set to the number of CPU cores available.

### Conclusion

Go's scheduler is an efficient and sophisticated tool that abstracts the complexities of concurrency and parallelism. It
allows developers to write highly concurrent programs without delving into the intricacies of thread management and
synchronization.

## Goroutine Yielding

## Goroutine Preemption

## Goroutine Stacks

## Goroutine Scheduling Events

### Goroutine Scheduling in Practice

### Goroutine Scheduling Best Practices

## Goroutine Local Storage

### Goroutine Local Storage Best Practices

## Best Practices

- **Leverage Goroutines for Concurrency**: The scheduler is designed to efficiently manage thousands of goroutines.
  Utilize them for concurrent tasks.
- **Avoid Long-Running Goroutines**: Since Go uses cooperative scheduling, long-running goroutines can potentially block
  the execution of other goroutines.
- **Be Mindful of Blocking Operations**: Blocking operations in a goroutine can impact the performance and
  responsiveness of your application.
- **Use Default GOMAXPROCS**: The Go runtime sets `GOMAXPROCS` (maximum number of OS threads that can execute user-level
  Go code simultaneously) intelligently by default. Only change it if there's a good reason.

## Example: Demonstrating Goroutine Scheduling

```go
package main

import (
    "fmt"
    "runtime"
    "time"
)

func printNumbers() {
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Printf("%d ", i)
    }
}

func main() {
    fmt.Println("GOMAXPROCS:", runtime.GOMAXPROCS(0)) // Print the number of OS threads

    go printNumbers()
    go printNumbers()

    time.Sleep(time.Second)
    fmt.Println("\nFinished")
}
```

In this example, two goroutines are running concurrently. The Go scheduler efficiently manages their execution on the
available OS threads.

## Conclusion

The Go runtime scheduler is a powerful feature that enables the efficient and easy handling of concurrency in Go
applications. Its design allows for massive concurrency with minimal overhead, making Go an ideal language for
high-concurrency tasks. Understanding how the Go scheduler works and its interaction with goroutines and OS threads is
key to writing efficient Go applications, especially those that require high levels of concurrency.