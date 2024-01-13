<!-- TOC -->
* [Context](#context)
  * [Best Practices](#best-practices)
  * [Example](#example)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Context

The `context` package in GoLang plays a crucial role in managing the lifecycle of processes and is particularly useful
in handling cancellation, timeouts, and passing request-scoped values across API boundaries.

**Purpose** - The primary use of a context is to provide a way to cancel branches of a program's execution,
propagate deadlines, and pass request-scoped values.

**Cancellation** - Contexts are often used to signal when a function should stop execution and return, typically
because the result is no longer needed, often due to user cancellation or a timeout.

**Deadlines and Timeouts** - Contexts can carry deadlines and cancel operations if they exceed these time limits.

**Values** - Contexts can also carry request-scoped values, like authentication tokens or session data, across
API boundaries.

**Types of Contexts**:

- `context.Background()`: Used at the top level; not cancelable.
- `context.TODO()`: Used when it's unclear which Context to use or it's not yet available.
- `context.WithCancel()`: Creates a new Context that can be canceled manually.
- `context.WithDeadline()`: Creates a Context that automatically cancels at a specific time.
- `context.WithTimeout()`: Similar to `WithDeadline` but specifies a time duration instead of a fixed time.

## Best Practices

- **Do Not Store State**: Contexts should not be used to pass optional parameters or to store state. They are for
  control signals.
- **Thread-Safe**: The values stored inside a context must be safe for concurrent use.
- **Pass Contexts in Functions**: Contexts should be passed as the first parameter in a function, typically named `ctx`.
- **One Context per Request**: In server applications, create one Context per request, and pass it down.
- **Cancellation Propagation**: Ensure that cancellation signals are propagated promptly.

## Example

Here's an example demonstrating the use of context for cancellation:

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func operation(ctx context.Context, duration time.Duration) {
    select {
    case <-time.After(duration):
        fmt.Println("Operation completed")
    case <-ctx.Done():
        fmt.Println("Operation canceled")
    }
}

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 100*time.Millisecond)
    defer cancel()

    go operation(ctx, 200*time.Millisecond)

    select {
    case <-ctx.Done():
        switch ctx.Err() {
        case context.DeadlineExceeded:
            fmt.Println("Main: Deadline exceeded")
        case context.Canceled:
            fmt.Println("Main: Canceled")
        }
    }
}
```

In this example, an operation is performed in a goroutine, which completes either when its operation is done or when the
context is canceled, whichever happens first.

## Conclusion

The `context` package is a powerful tool in GoLang for managing scopes of operations, particularly in a concurrent
environment. It's essential for writing robust, scalable, and well-organized Go applications, especially those dealing
with network requests, long-running operations, and handling cancellation and timeouts effectively. Proper use of
context ensures better control and management of go routines and resource utilization.