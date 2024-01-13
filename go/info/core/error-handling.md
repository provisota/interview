<!-- TOC -->
* [Error Handling](#error-handling)
  * [Technical Details of Error Handling in GoLang](#technical-details-of-error-handling-in-golang)
  * [Basic Error Handling](#basic-error-handling)
  * [Custom Error Type](#custom-error-type)
  * [Best Practices for Error Handling in GoLang](#best-practices-for-error-handling-in-golang)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Error Handling

Error handling in GoLang is a critical aspect of writing robust and reliable software. GoLang adopts a straightforward
and explicit approach to error handling, which is distinct from the exception handling mechanisms found in many other
programming languages.

## Technical Details of Error Handling in GoLang

**Error Type**:

- In Go, errors are represented using the `error` type, a built-in interface.
- This interface has a single method `Error()`, which returns a string indicating the nature of the error.

**Creating Errors** - Errors are typically created using the `errors.New` function or by using `fmt.Errorf` if
formatting is required.

**Returning Errors**:

- In Go, functions that can encounter errors typically return an error as their last return value.
- It's idiomatic to check for errors immediately after calling a function that returns an error.

**No Exceptions** - GoLang does not use exceptions. Instead, it uses the returned error to indicate whether an
operation succeeded or failed.

**Custom Error Types**:

- Custom error types can be created by implementing the `error` interface.
- This is useful for representing more complex error conditions and attaching additional context or data to the error.

**Panic and Recover**:

- GoLang provides two built-in functions, `panic` and `recover`, for situations that are not typical errors.
- `panic` halts normal execution, while `recover` can regain control after a `panic` has occurred. These are generally
  used in more severe situations, like runtime errors.

## Basic Error Handling

```go
package main

import (
    "errors"
    "fmt"
    "log"
)

func divide(a, b float64) (float64, error) {
    if b == 0.0 {
        return 0.0, errors.New("division by zero")
    }
    return a / b, nil
}

func main() {
    result, err := divide(10.0, 0.0)
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println("Result:", result)
}
```

## Custom Error Type

```go
package main

import (
    "fmt"
)

type MyError struct {
    Message string
    Code    int
}

func (e *MyError) Error() string {
    return fmt.Sprintf("%d - %s", e.Code, e.Message)
}

func doSomething() error {
    return &MyError{"An error occurred", 404}
}

func main() {
    err := doSomething()
    if err != nil {
        fmt.Println(err)
    }
}
```

## Best Practices for Error Handling in GoLang

- Always check for errors immediately after calling a function that can return an error.
- Return errors for exceptional cases, not for normal control flow.
- Provide clear, descriptive error messages.
- Consider creating custom error types for complex error handling scenarios.
- Use `panic` sparingly, typically for unrecoverable errors or situations where continuing normal execution is
  impossible.

## Conclusion

Error handling in GoLang is integral to writing clean, reliable, and maintainable code. Its explicit nature encourages
developers to handle errors gracefully and think carefully about failure conditions in their code.