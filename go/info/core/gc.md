<!-- TOC -->
* [GC](#gc)
  * [GC Optimization](#gc-optimization)
  * [Best Practices](#best-practices)
  * [Example](#example)
  * [Conclusion](#conclusion)
<!-- TOC -->

# GC

GoLang's approach to garbage collection is designed for simplicity and efficiency, balancing performance with developer
convenience.

**Automatic Memory Management**: The Go runtime automatically handles the allocation and deallocation of memory. This
means developers don't need to manually free memory, reducing the risk of memory leaks and segmentation faults.

**Concurrent Garbage Collector** - Go uses a concurrent, tri-color mark-and-sweep garbage collector. This means the
collector performs most of its tasks without stopping the program, reducing pause times.

**Tri-Color Mark-and-Sweep Algorithm**: Modern Go uses a form of the tri-color mark-and-sweep algorithm for garbage
collection. This algorithm works in three phases: marking, sweeping, and optionally compacting.

- **Marking**: Identifies which objects are still reachable (in use).
- **Sweeping**: Frees memory occupied by unreachable objects.
- **Compacting** (optional): Compacts memory to address fragmentation issues.

**Concurrency and Performance**: Go's GC is designed to be concurrent; it runs in parallel with other goroutines.
This concurrency minimizes pause times, improving overall application performance.

**GC Tuning**: While Go's GC is automatic, it can be tuned for specific workloads using environment variables (
like `GOGC`) to control the aggressiveness of the collector.

**Memory Allocation** - Go's garbage collector optimizes memory allocation through the use of a technique known as
escape analysis. It determines whether a variable can be safely allocated on the stack or if it needs to be allocated on
the heap.

**GC Pacing** - The runtime paces the garbage collector based on the amount of allocated memory and the time taken
by the previous collection, aiming to maintain low latency and high throughput.

## GC Optimization

**Concurrent Mark and Sweep**

Modern versions of Go use a concurrent mark-and-sweep algorithm, allowing the garbage collector to run concurrently with
the program, reducing pause times.

**Write Barriers**

Write barriers are used during the mark phase. They allow the program to continue running while keeping track of changes
that could affect the set of live objects.

**Garbage Collection Pacing**

The Go runtime dynamically adjusts the pacing of the garbage collector based on the amount of allocated memory and the
time taken in previous collection cycles.

**Heap Compaction**

While Go's garbage collector doesn't fully compact the heap, recent versions have optimizations to reduce fragmentation,
improving memory efficiency.

These aspects of Go's runtime environment, including goroutines, escape analysis, caching mechanisms, and garbage
collection optimizations, are integral to the language's performance characteristics and are designed to make concurrent
programming more efficient and less error-prone.

## Best Practices

- **Minimize Heap Allocations**: Where possible, prefer stack allocations by limiting the scope and lifetime of
  variables.
- **Reuse Objects**: Reusing objects can reduce the pressure on the garbage collector.
- **Avoid Finalizers**: Finalizers can complicate garbage collection and are best avoided unless absolutely necessary.
- **Profile Your Application**: Use Go's built-in profiling tools to understand your application's memory usage and
  garbage collection behavior.

## Example

```go
package main

import (
    "fmt"
    "runtime"
)

func main() {
    printMemStats("Initial")

    for i := 0; i < 10; i++ {
        _ = make([]byte, 1<<20) // Allocating 1 MiB
    }

    printMemStats("After Allocation")

    runtime.GC() // Forcing a garbage collection
    printMemStats("After GC")
}

func printMemStats(msg string) {
    var m runtime.MemStats
    runtime.ReadMemStats(&m)
    fmt.Printf("%s: Alloc = %v MiB", msg, m.Alloc / 1024 / 1024)
    fmt.Printf("\tTotalAlloc = %v MiB", m.TotalAlloc / 1024 / 1024)
    fmt.Printf("\tSys = %v MiB", m.Sys / 1024 / 1024)
    fmt.Printf("\tNumGC = %v\n", m.NumGC)
}
```

In this example, memory allocation is shown before and after garbage collection, illustrating how Go manages memory.

## Conclusion

Go's garbage collector is a key part of its appeal, offering automatic memory management that allows developers to focus
more on their application logic and less on manual memory management. However, understanding how GC works and how it
impacts application performance is crucial. Good practices around memory allocation and object reuse can significantly
improve performance and reduce GC overhead in Go applications.