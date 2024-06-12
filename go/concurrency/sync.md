# Synchronization Primitives

In concurrent programming with GoLang, synchronization primitives are essential tools for managing access to shared
resources and coordinating the execution flow of goroutines. Go provides several built-in synchronization primitives in
the `sync` package, each designed for specific use cases.

**Mutex (Mutual Exclusion Lock)**

A Mutex is used to provide a locking mechanism to ensure that only one goroutine is accessing the critical section
of code at any point in time. `sync.Mutex` and `sync.RWMutex` (for read-write scenarios) are the primary mutex types.

**WaitGroup**

`sync.WaitGroup` is used for waiting for a collection of goroutines to finish executing. The main goroutine calls `Add`
to set the number of goroutines to wait for. Then each of the goroutines runs and calls `Done` when finished.
Meanwhile, `Wait` can be used to block until all goroutines have finished.

**Once**

`sync.Once` is used to ensure that a piece of code is executed only once, regardless of how many goroutines are calling
it. This is particularly useful for initialization.

**Cond (Condition Variable)**

A `sync.Cond` is a rendezvous point for goroutines waiting for or announcing the occurrence of an event. It's used with
a Mutex or RWMutex to synchronize changes to shared state.

## Best Practices

- **Avoid Deadlocks**: Ensure that locks are not held longer than necessary and avoid complex interdependencies that can
  lead to deadlocks.
- **Prefer Channel Communication**: Wherever possible, use channels to communicate between goroutines rather than
  sharing memory directly.
- **Use the Right Primitive**: Choose the synchronization primitive that best fits your use case to avoid
  over-complication.
- **Document Concurrency Assumptions**: Clearly document the assumptions and design decisions behind the use of
  synchronization primitives in your code.

## Using `sync` Package

1. **Mutexes (`sync.Mutex` and `sync.RWMutex`):**
   Mutexes are used for mutually exclusive locking. `sync.Mutex` provides basic locking and unlocking functionality,
   ensuring that only one goroutine accesses a shared resource at a time. `sync.RWMutex` is a reader/writer mutex,
   allowing multiple readers or one writer.

   **Example:**
   ```go
   var mu sync.Mutex
   var count int

   func increment() {
       mu.Lock() // Lock the mutex
       count++
       mu.Unlock() // Unlock the mutex
   }
   ```

2. **WaitGroups (`sync.WaitGroup`):**
   WaitGroups are used to wait for a collection of goroutines to finish executing.

   **Example:**
   ```go
   var wg sync.WaitGroup

   for i := 0; i < 10; i++ {
       wg.Add(1) // Increment the WaitGroup counter
       go func(i int) {
           defer wg.Done() // Decrement the counter when the goroutine completes
           fmt.Println(i)
       }(i)
   }

   wg.Wait() // Wait for all goroutines to finish
   ```

3. **Once (`sync.Once`):**
   `sync.Once` is used to ensure that a piece of code is only executed once, regardless of how many goroutines reach
   that code.

   **Example:**
   ```go
   var once sync.Once

   initFunc := func() {
       fmt.Println("Initialized only once")
   }

   for i := 0; i < 10; i++ {
       go func() {
           once.Do(initFunc)
       }()
   }
   ```

4. **Cond (`sync.Cond`):**

`sync.Cond` is a synchronization primitive in Go that can be used to wait for or announce the occurrence of certain
conditions in your program. It's particularly useful when one or more goroutines need to wait for a certain condition to
be true before continuing their execution. Here's a simple example to illustrate its use:

First, we need to import the necessary packages and set up our shared data structure.

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

// Item - a simple struct representing an item that can be produced and consumed.
type Item struct {
    Name string
}
```

```go
// Shared data structure
var (
    itemQueue = make([]Item, 0)
    mutex     sync.Mutex
)

// Condition variable
var itemAvailable = sync.NewCond(&mutex)
```

The producer will add items to the queue and notify the consumer that an item is available.

```go
func produce(name string) {
    mutex.Lock()
    item := Item{Name: name}
    itemQueue = append(itemQueue, item)
    fmt.Printf("Produced: %s\n", item.Name)
    itemAvailable.Signal() // Notify one waiting goroutine, if any.
    mutex.Unlock()
}
```

The consumer will wait for items to be available and then process them.

```go
func consume() {
    mutex.Lock()
    for len(itemQueue) == 0 {
        itemAvailable.Wait() // Wait for a signal that an item is available.
    }

    // Consume the first item in the queue.
    item := itemQueue[0]
    itemQueue = itemQueue[1:]
    fmt.Printf("Consumed: %s\n", item.Name)
    mutex.Unlock()
}
```

Finally, let's create some goroutines to simulate the producer and consumer.

```go
func main() {
    go consume()
    go produce("item1")
    go produce("item2")

    // Sleep to allow time for goroutines to complete their tasks.
    time.Sleep(1 * time.Second)
}
```

- **Mutex Locking**: We use a mutex to protect access to the shared queue (`itemQueue`).
- **Condition Variable**: The `sync.Cond` variable (`itemAvailable`) is used to wait for a condition (item available in
  the queue) and to notify waiting goroutines when that condition occurs (when a new item is produced).

This is a basic example. In real-world applications, you may have multiple producers and consumers, and you might need
to handle more complex conditions and data structures.

## Example: Using Mutex and WaitGroup

```go
package main

import (
    "fmt"
    "sync"
)

var (
    mutex   sync.Mutex
    balance int
)

func deposit(value int, wg *sync.WaitGroup) {
    mutex.Lock()
    fmt.Printf("Depositing %d to account with balance: %d\n", value, balance)
    balance += value
    mutex.Unlock()
    wg.Done()
}

func main() {
    var wg sync.WaitGroup
    wg.Add(2)
    go deposit(100, &wg)
    go deposit(200, &wg)
    wg.Wait()

    fmt.Printf("New Balance: %d\n", balance)
}
```

In this example, `sync.Mutex` is used to synchronize access to a shared resource (`balance`), and `sync.WaitGroup` is
used to wait for both deposit operations to complete.

## Conclusion

Synchronization primitives in GoLang are crucial for writing concurrent and parallel programs, especially when dealing
with shared resources or coordinating between multiple goroutines. Proper understanding and use of these primitives help
in writing robust and deadlock-free Go applications. The choice of the right synchronization tool and adherence to best
practices in concurrency control are pivotal to the development of effective GoLang applications.