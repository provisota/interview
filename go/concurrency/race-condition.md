# Race Condition

A race condition in GoLang occurs when the system's behavior depends on the sequence or timing of uncontrollable events,
particularly in a concurrent environment. It leads to unpredictable and erroneous behavior, making race conditions a
critical issue in concurrent programming.

A race condition arises when two or more goroutines access shared resources and attempt to read and modify them
concurrently without proper synchronization, leading to conflicting changes.

Race conditions are often unpredictable and hard to reproduce as they depend on the specific timing of execution.

They can result in incorrect program behavior, including incorrect data, deadlocks, and program crashes.

Simultaneous access to a shared variable, where at least one goroutine modifies it.

Concurrent read/write operations on maps, slices, or other shared data structures.

GoLang's race detector (enabled with the `-race` flag) is a powerful tool to detect race conditions at runtime. It helps
in identifying the code segments where race conditions occur.

## Best Practices

- **Mutex for Synchronization**: Use `sync.Mutex` or `sync.RWMutex` to synchronize access to shared resources.
- **Atomic Operations**: For simple use cases, consider using atomic operations from the `sync/atomic` package.
- **Design for Concurrency**: Structure your program to minimize shared state and design goroutines that don't step on
  each other's toes.
- **Channel Communication**: Prefer using channels to share data between goroutines, as channels provide inherent
  synchronization.

## Example: Race Condition and Mutex

Here's an example demonstrating a race condition and how to fix it using a mutex:

```go
package main

import (
    "fmt"
    "sync"
)

var (
    counter int
    mutex   sync.Mutex
)

func increment(wg *sync.WaitGroup) {
    mutex.Lock()
    defer mutex.Unlock()
    counter++
    wg.Done()
}

func main() {
    var wg sync.WaitGroup
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go increment(&wg)
    }
    wg.Wait()
    fmt.Println("Final Counter:", counter)
}
```

In this example, the `increment` function is called concurrently by 1000 goroutines. The `sync.Mutex` ensures that only
one goroutine can access the `counter` variable at a time, thus preventing a race condition.

## Conclusion

Race conditions in GoLang are a common pitfall in concurrent programming. They can be subtle and difficult to debug.
Using proper synchronization mechanisms like mutexes, atomic operations, and channels can help prevent race conditions.
Regular testing with the race detector is also crucial in identifying and resolving race conditions, leading to more
stable and reliable concurrent applications.