# Concurrency Patterns in Go

GoLang is designed with first-class support for concurrency, making it a great choice for building concurrent
applications. Understanding and applying concurrency patterns effectively is key to leveraging Go's concurrency
capabilities.

**Goroutines**

Basic units of concurrency in Go. They are functions or methods that run concurrently with other functions or methods.

**Channels**

Used for communication between goroutines. Channels can be buffered or unbuffered and are crucial for coordinating and
synchronizing concurrent operations.

**Select Statement**

Allows a goroutine to wait on multiple communication operations, blocking until one of its cases can proceed.

## Common Concurrency Patterns

1. [Worker Pools](#worker-pools)
2. [Pipeline](#pipeline)
3. [Fan-Out, Fan-In](#fan-out-fan-in)
4. [Pub/Sub](#pubsub)
5. [Timeouts and Tickers](#timeouts-and-tickers)

### Worker Pools

Used to manage a finite number of workers (goroutines) that handle a stream of jobs. This pattern helps control the
number of goroutines running in parallel, which is efficient for resource management.

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func worker(id int, jobs <-chan int, results chan<- int) {
	for j := range jobs {
		fmt.Println("worker", id, "processing job", j)
		time.Sleep(time.Second)
		results <- j * 2
	}
}

func main() {
	const numJobs = 5
	jobs := make(chan int, numJobs)
	results := make(chan int, numJobs)

	for w := 1; w <= 3; w++ {
		go worker(w, jobs, results)
	}

	for j := 1; j <= numJobs; j++ {
		jobs <- j
	}
	close(jobs)

	for a := 1; a <= numJobs; a++ {
		<-results
	}
}
```

### Pipeline

Involves chaining stages, where each stage is a sequence of operations run in a goroutine. Data passes through channels
from one stage to the next.

```go
package main

import "fmt"

func gen(nums ...int) <-chan int {
	out := make(chan int)
	go func() {
		for _, n := range nums {
			out <- n
		}
		close(out)
	}()
	return out
}

func sq(in <-chan int) <-chan int {
	out := make(chan int)
	go func() {
		for n := range in {
			out <- n * n
		}
		close(out)
	}()
	return out
}

func main() {
	// Set up the pipeline.
	c := gen(2, 3, 4)
	out := sq(c)

	// Consume the output.
	for result := range out {
		fmt.Println(result)
	}
}

```

### Fan-Out, Fan-In

'Fan-out' refers to starting multiple goroutines to handle input from a channel. 'Fan-in' is the process of combining
results from multiple goroutines into a single channel.

```go
package main

import (
	"fmt"
	"sync"
)

func producer(nums []int, ch chan<- int) {
	for _, n := range nums {
		ch <- n
	}
	close(ch)
}

func squareWorker(in <-chan int, out chan<- int) {
	for n := range in {
		out <- n * n
	}
	close(out)
}

func main() {
	nums := []int{2, 4, 6, 8, 10}
	ch := make(chan int, len(nums))
	out := make(chan int, len(nums))

	go producer(nums, ch)

	var wg sync.WaitGroup
	for i := 0; i < 2; i++ {
		wg.Add(1)
		go func() {
			squareWorker(ch, out)
			wg.Done()
		}()
	}

	go func() {
		wg.Wait()
		close(out)
	}()

	for result := range out {
		fmt.Println(result)
	}
}

```

In this example, jobs are fanned out to multiple workers, and their results are collected (fanned in) into a single
results channel.

### Pub/Sub

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

type PubSub struct {
	mu     sync.RWMutex
	subs   map[string][]chan string
	closed bool
}

func NewPubSub() *PubSub {
	return &PubSub{
		subs: make(map[string][]chan string),
	}
}

func (ps *PubSub) Subscribe(topic string) <-chan string {
	ps.mu.Lock()
	defer ps.mu.Unlock()

	ch := make(chan string, 1)
	ps.subs[topic] = append(ps.subs[topic], ch)
	return ch
}

func (ps *PubSub) Publish(topic, msg string) {
	ps.mu.RLock()
	defer ps.mu.RUnlock()

	if ps.closed {
		return
	}

	for _, ch := range ps.subs[topic] {
		ch <- msg
	}
}

func (ps *PubSub) Close() {
	ps.mu.Lock()
	defer ps.mu.Unlock()

	if !ps.closed {
		ps.closed = true
		for _, subs := range ps.subs {
			for _, ch := range subs {
				close(ch)
			}
		}
	}
}

func main() {
	ps := NewPubSub()
	sub := ps.Subscribe("myTopic")

	go func() {
		for msg := range sub {
			fmt.Println("Received:", msg)
		}
	}()

	ps.Publish("myTopic", "hello")
	ps.Publish("myTopic", "world")

	time.Sleep(time.Second)
	ps.Close()
}

```

### Timeouts and Tickers

Using the `time.After` and `time.Ticker` functions for operations that should not wait indefinitely or need to execute
at regular intervals.

In Go, timeouts and tickers are important for managing time-sensitive operations and recurring tasks. Let's discuss each
and provide examples:

**Timeouts**

Timeouts are crucial for preventing a Go program from waiting indefinitely. You can implement timeouts
using `time.After` in combination with `select` statements.

```go
package main

import (
	"fmt"
	"time"
)

func operation(done chan bool) {
	time.Sleep(2 * time.Second) // Simulate a task that takes 2 seconds
	done <- true
}

func main() {
	done := make(chan bool, 1)
	go operation(done)

	select {
	case <-done:
		fmt.Println("Operation successful")
	case <-time.After(1 * time.Second):
		fmt.Println("Operation timeout")
	}
}
```

In this example, the operation is simulated with a 2-second sleep. The main goroutine waits for the operation to send a
signal on the `done` channel or for a 1-second timeout, whichever occurs first.

**Tickers**

Tickers are used for doing something repeatedly at regular intervals.

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	ticker := time.NewTicker(1 * time.Second)
	done := make(chan bool)

	go func() {
		for {
			select {
			case <-done:
				return
			case t := <-ticker.C:
				fmt.Println("Tick at", t)
			}
		}
	}()

	// Stop the ticker after 5 seconds
	time.Sleep(5 * time.Second)
	ticker.Stop()
	done <- true
	fmt.Println("Ticker stopped")
}
```

In this example, a ticker is set to tick every second. The goroutine runs a loop, selecting over the ticker's channel.
It prints the current time at each tick. After 5 seconds, the main goroutine stops the ticker and signals the goroutine
to finish.

**Combining Timeouts and Tickers**

You can also combine timeouts and tickers to perform time-based operations where each iteration of a task has its own
timeout.

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	ticker := time.NewTicker(2 * time.Second)
	for i := 0; i < 3; i++ {
		select {
		case <-ticker.C:
			fmt.Println("Tick", i)
			// Simulate a task with a possible timeout
			select {
			case <-time.After(1 * time.Second):
				fmt.Println("Task timeout on tick", i)
			case <-task():
				fmt.Println("Task completed on tick", i)
			}
		}
	}
	ticker.Stop()
}

func task() <-chan bool {
	done := make(chan bool)
	go func() {
		// Simulate variable task duration
		time.Sleep(time.Duration(500+rand.Intn(1500)) * time.Millisecond)
		done <- true
	}()
	return done
}
```

In this combined example, a ticker triggers a task at regular intervals. Each task has its own timeout set
with `time.After`. This pattern is useful when you need to enforce timeouts on repetitive tasks.

These examples illustrate basic usage of timeouts and tickers in Go. Depending on your specific requirements, you might
need to adjust these patterns to fit your application's architecture and error handling strategies.

## Graceful Goroutine Termination

Graceful termination of goroutines in Go is essential for preventing resource leaks and ensuring that your program exits
cleanly. This usually involves signaling goroutines to stop and waiting for them to finish their current work. There are
several ways to achieve this, but a common and effective method is using channels and the `context` package.

### Using Channels

You can signal goroutines to stop by closing a channel. Goroutines check whether the channel is closed before continuing
their work.

#### Example:

```go
package main

import (
	"fmt"
	"time"
)

func worker(stopChan <-chan struct{}) {
	for {
		select {
		case <-stopChan:
			fmt.Println("Worker shutting down")
			return
		default:
			// Do some work...
			fmt.Println("Worker is working...")
			time.Sleep(500 * time.Millisecond)
		}
	}
}

func main() {
	stopChan := make(chan struct{})
	go worker(stopChan)

	// Run the worker for 2 seconds
	time.Sleep(2 * time.Second)
	close(stopChan) // Signal the worker to stop

	// Give some time for the worker to shut down
	time.Sleep(500 * time.Millisecond)
}
```

In this example, the worker goroutine periodically checks if `stopChan` is closed. If it is, the worker stops.

### Using the `context` Package

The `context` package provides more control and is particularly useful when you have multiple goroutines that you need
to stop.

#### Example:

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func worker(ctx context.Context) {
	for {
		select {
		case <-ctx.Done():
			fmt.Println("Worker shutting down")
			return
		default:
			// Do some work...
			fmt.Println("Worker is working...")
			time.Sleep(500 * time.Millisecond)
		}
	}
}

func main() {
	ctx, cancel := context.WithCancel(context.Background())
	go worker(ctx)

	// Run the worker for 2 seconds
	time.Sleep(2 * time.Second)
	cancel() // Signal the worker to stop

	// Give some time for the worker to shut down
	time.Sleep(500 * time.Millisecond)
}
```

In this example, the `context` package is used to create a `context.Context` with a `cancel` function. When `cancel` is
called, `ctx.Done()` is closed, and the worker stops.

### Things to Note

1. **Waiting for Goroutines**: In these examples, `time.Sleep` is used to wait for the goroutines to finish. In a real
   application, you would typically use `sync.WaitGroup` or similar mechanisms to wait for all goroutines to complete
   their work.

2. **Handling Resources**: Make sure to release any resources (like network connections, file handles, etc.) that the
   goroutine may be holding before it terminates.

3. **Idempotency**: Ensure that the stopping mechanism is idempotent; calling it multiple times should not cause an
   error or panic.

Graceful termination of goroutines helps to create robust and reliable Go applications, especially in the context of
long-running processes or server applications.

## Proper Error Handling

Proper error handling in goroutines is crucial in Go to ensure robust and stable applications, especially since
goroutines run independently of their spawning thread. Since goroutines have their own execution path, errors that occur
inside them should be communicated back to the main program or the goroutine's caller. Here are some strategies for
handling errors in goroutines:

### 1. Using Channels for Error Propagation

One common way to handle errors in goroutines is to use a channel to send errors back to the main goroutine.

#### Example:

```go
package main

import (
	"errors"
	"fmt"
	"time"
)

func doTask(i int, errCh chan<- error) {
	if i%2 == 0 {
		errCh <- errors.New("even number error")
	} else {
		errCh <- nil // Send nil if no error
	}
}

func main() {
	errCh := make(chan error, 1) // Buffered channel

	for i := 1; i <= 5; i++ {
		go doTask(i, errCh)

		err := <-errCh // Receive an error from the channel
		if err != nil {
			fmt.Println("Error:", err)
		} else {
			fmt.Println("Task completed successfully")
		}
	}

	time.Sleep(time.Second) // Wait for goroutines to finish
}
```

In this example, each goroutine sends an error or `nil` to the `errCh` channel, which the main goroutine reads from.

### 2. Using `sync.WaitGroup` and Error Handling

When dealing with multiple goroutines, you can use a `sync.WaitGroup` to wait for all goroutines to complete and collect
errors in a thread-safe manner.

#### Example:

```go
package main

import (
	"errors"
	"fmt"
	"sync"
)

func doTask(i int, wg *sync.WaitGroup, errCh chan<- error) {
	defer wg.Done()

	if i%2 == 0 {
		errCh <- errors.New("even number error")
	} else {
		errCh <- nil
	}
}

func main() {
	var wg sync.WaitGroup
	errCh := make(chan error, 10)

	for i := 1; i <= 10; i++ {
		wg.Add(1)
		go doTask(i, &wg, errCh)
	}

	wg.Wait()
	close(errCh)

	for err := range errCh {
		if err != nil {
			fmt.Println("Error:", err)
		}
	}
}
```

In this example, a `sync.WaitGroup` ensures that the main goroutine waits for all child goroutines to complete, and
errors are communicated through a channel.

### 3. Using `context.Context` for Error Propagation

The `context.Context` can be used to propagate errors, especially when you need to handle timeouts or cancellations.

#### Example:

```go
package main

import (
	"context"
	"errors"
	"fmt"
	"time"
)

func doTask(ctx context.Context, i int) error {
	// Simulate a task
	time.Sleep(100 * time.Millisecond)

	if i%2 == 0 {
		return errors.New("even number error")
	}
	return nil
}

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), 500*time.Millisecond)
	defer cancel()

	errCh := make(chan error, 1)

	for i := 1; i <= 5; i++ {
		go func(i int) {
			err := doTask(ctx, i)
			select {
			case <-ctx.Done():
				return // Ignore this error because the context is done
			case errCh <- err:
			}
		}(i)
	}

	for i := 1; i <= 5; i++ {
		select {
		case <-ctx.Done():
			fmt.Println("Context timed out")
			return
		case err := <-errCh:
			if err != nil {
				fmt.Println("Error:", err)
			} else {
				fmt.Println("Task completed successfully")
			}
		}
	}
}
```

In this example, `context.Context` is used to manage timeout and error propagation.

### Best Practices:

- Always make sure to handle errors from all goroutines.
- Use buffered channels to prevent goroutines from blocking when sending errors.
- Ensure that resources are properly cleaned up after goroutines are done, especially in the presence of errors.
- Be cautious of goroutine leaks; make sure goroutines exit under all conditions.

## Resource Cleanup

Resource cleanup in goroutines is critical to prevent resource leaks, such as open files, network connections, or memory
allocations. Proper cleanup ensures that resources are released when they are no longer needed. In Go, this is often
achieved through the use of `defer` statements, proper error handling, and the `context` package for managing the
lifecycle of goroutines. Here are some strategies and examples:

### 1. Using `defer` for Cleanup

The `defer` statement is used to ensure that functions are executed after the surrounding function completes, which is
useful for cleanup tasks.

#### Example: File Handling

```go
package main

import (
	"fmt"
	"os"
)

func processFile(filename string) error {
	file, err := os.Open(filename)
	if err != nil {
		return err
	}
	defer file.Close() // Ensures file is closed when the function exits

	// Process the file...

	return nil
}

func main() {
	err := processFile("example.txt")
	if err != nil {
		fmt.Println("Error:", err)
	}
}
```

In this example, `defer file.Close()` ensures that the file is closed when `processFile` exits, regardless of whether it
exits normally or due to an error.

### 2. Cleanup in Goroutines with Error Handling

When dealing with goroutines, especially those that may encounter errors, it’s important to handle both the error and
cleanup aspects.

#### Example: Concurrent HTTP Requests

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
	"sync"
)

func fetchURL(wg *sync.WaitGroup, url string) {
	defer wg.Done()

	resp, err := http.Get(url)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	defer resp.Body.Close() // Ensure response body is closed

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Error reading body:", err)
		return
	}

	fmt.Println("Response:", string(body))
}

func main() {
	var wg sync.WaitGroup
	urls := []string{"http://example.com", "http://example.org"}

	for _, url := range urls {
		wg.Add(1)
		go fetchURL(&wg, url)
	}

	wg.Wait()
}
```

In this example, `defer resp.Body.Close()` ensures that the response body is closed after handling each HTTP request.

### 3. Using `context.Context` for Managing Goroutine Lifecycle

The `context` package is often used to control the lifecycle of goroutines, especially when you need to cancel them or
when they are part of a larger operation that may be cancelled or timeout.

#### Example: Cancelable Goroutines

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func operation(ctx context.Context, duration time.Duration) {
	select {
	case <-ctx.Done():
		fmt.Println("Operation cancelled")
	case <-time.After(duration):
		fmt.Println("Operation completed")
	}
}

func main() {
	ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	defer cancel()

	go operation(ctx, 3*time.Second)

	time.Sleep(1 * time.Second) // Simulate work
}
```

In this example, `operation` will be cancelled if it runs longer than the timeout specified by the context.

### Best Practices for Resource Cleanup:

- Use `defer` for resource cleanup to ensure resources are released even if an error occurs.
- Ensure that goroutines release resources, like network connections or file handles, as soon as they are done with
  them.
- Use `context.Context` to manage the lifecycle of goroutines, especially for long-running or cancellable operations.
- Handle errors properly in goroutines and ensure that cleanup occurs in the presence of errors.
- Avoid goroutine leaks by ensuring they can always exit, especially in long-running applications.

## Best Practices

- **Avoid Shared State**: Prefer channel communication over shared memory to avoid complex and error-prone
  synchronization.
- **Graceful Goroutine Termination**: Design goroutines that can be stopped gracefully, typically using a `done`
  channel.
- **Proper Error Handling**: Handle errors in concurrent processes effectively, especially when dealing with multiple
  goroutines.
- **Resource Cleanup**: Ensure resources like channels and network connections are properly closed or cleaned up.

## Conclusion

Concurrency patterns in GoLang, when used properly, can lead to highly efficient and maintainable code. The key to
effective concurrent programming in Go is understanding how to structure programs to leverage goroutines and channels,
and the various patterns like worker pools, pipelines, and fan-out/fan-in provide a robust framework for doing so. These
patterns are essential for writing scalable, concurrent applications in Go.