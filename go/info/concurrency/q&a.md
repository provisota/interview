# Q&A
## Questions

1. What is goroutine and its usecases?
2. How to start goroutine?
3. What is channel and its usecases?
4. What is buffered channel?
5. What will happen in case of reading/writing open/closed/nil channel?
6. Which synchronization primitives (from sync/xsync) do you know? Can you provide usecases?
7. select-case operator usecases?
8. Explain the difference between process, thread and goroutin?
9. What is the race condition, data race, and deadlock?
10. How can we wait for a group of goroutines to finish?
11. What is the purpose of atomic package?
12. How to tell if buffered channel is full? How can we handle writing to a full channel?
13. What is the difference betrween concurrency and parallelism?
14. What concurrency patterns do you know? Explain usecases.
15. Explain how golang scheduler works under the hood?
16. What kind of concurrency problems can detect race detector? (data race/ race condition/ deadlock)

## Answers

### 1. Goroutine and Its Use Cases

- **Goroutine**: A lightweight thread managed by the Go runtime. They are used for concurrent execution within a
  program.
- **Use Cases**: Ideal for tasks like handling HTTP requests, background processing, concurrent data processing, and any
  situation where asynchronous processing is beneficial.

### 2. Starting a Goroutine

- To start a goroutine, use the `go` keyword followed by a function call: `go myFunction(parameters)`

### 3. Channels and Their Use Cases

- **Channel**: A mechanism for goroutines to communicate and synchronize execution.
- **Use Cases**: Sending data between goroutines, signaling events, and coordinating concurrent processes like
  implementing a worker pool.

### 4. Buffered Channel

- A buffered channel has a limited capacity, allowing goroutines to send a certain number of values without a
  corresponding receiver for those values.

### 5. Channel Behavior

- **Reading/Writing Open Channel**: Functions normally.
- **Closed Channel**: Reading succeeds with zero values returned; writing causes a panic.
- **Nil Channel**: Reading or writing blocks indefinitely.

### 6. Synchronization Primitives and Use Cases

- **Mutex (`sync.Mutex`)**: For mutual exclusion, protecting shared resources from concurrent access.
- **WaitGroup (`sync.WaitGroup`)**: For waiting for a collection of goroutines to finish.
- **Cond (`sync.Cond`)**: For signaling the waiting goroutines when certain conditions are met.
- **Use Cases**: Managing shared resources, synchronizing goroutine completion, implementing condition-based waiting.

### 7. `select-case` Operator Use Cases

- For handling multiple channel operations, implementing timeouts, non-blocking channel operations, and orchestrating
  multiple communication processes.

### 8. Process, Thread, and Goroutine

- **Process**: An independent execution unit with its own memory space, managed by the OS.
- **Thread**: A lighter execution unit within a process, sharing memory space, managed by the OS.
- **Goroutine**: A much lighter unit than a thread, managed by the Go runtime, multiple goroutines may run on a single
  thread.

### 9. Race Condition, Data Race, and Deadlock

- **Race Condition**: A condition where the system's behavior depends on the sequence or timing of uncontrollable
  events.
- **Data Race**: Occurs when two goroutines access the same variable concurrently and at least one access is a write.
- **Deadlock**: A situation where goroutines are waiting indefinitely for each other to release resources.

### 10. Waiting for Goroutines

- Use a `sync.WaitGroup` to wait for a group of goroutines to finish. Increment the WaitGroup counter for each goroutine
  launched and decrement it (`wg.Done()`) in each goroutine once finished. `wg.Wait()` is used to block until all
  goroutines complete.

### 11. Purpose of Atomic Package

- The `atomic` package provides low-level atomic memory primitives useful for implementing synchronization algorithms
  without the need for locking.

### 12. Handling Full Buffered Channels

- To check if a buffered channel is full, use the `select` statement with a default case. Handling a full channel
  includes blocking the goroutine, dropping the data, or increasing the buffer size.

### 13. Concurrency vs. Parallelism

- **Concurrency**: Managing multiple tasks at once (not necessarily simultaneously).
- **Parallelism**: Executing multiple tasks at exactly the same time, often leveraging multi-core processors.

### 14. Concurrency Patterns

- **Worker Pools**: Distributing tasks across multiple worker goroutines.
- **Pipelines**: Processing data through a series of stages connected by channels.
- **Fan-Out, Fan-In**: Distributing tasks among multiple goroutines and then collecting their results.

### 15. Go Scheduler

- The Go scheduler manages goroutines in a non-preemptive manner, multiplexing them onto multiple OS threads. It uses a
  work-stealing algorithm for load balancing and efficiently utilizes multi-core processors.

### 16. Race Detector Capabilities

- The race detector in Go can detect data races but is not designed to detect race conditions or deadlocks directly. It
  helps in identifying concurrent access issues that could lead to race conditions or deadlocks.