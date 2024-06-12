<!-- TOC -->
* [Control Flow](#control-flow)
  * [If-Else Statements](#if-else-statements)
  * [Switch Statements](#switch-statements)
  * [For Loops](#for-loops)
  * [Defer Statement](#defer-statement)
  * [Goto Statement](#goto-statement)
  * [Break and Continue](#break-and-continue)
  * [Best Practices in Control Flow:](#best-practices-in-control-flow)
<!-- TOC -->

# Control Flow

Control flow in GoLang, like in most programming languages, dictates the order in which instructions are executed.
GoLang provides several constructs for managing control flow:

## If-Else Statements

The `if` statement in Go is used to execute a block of code based on a condition. It can be followed by an
optional `else` block.

```go
if condition {
    // executed if condition is true
} else {
    // executed if condition is false
}
```

Go also supports an `else if` ladder for multiple conditions.

## Switch Statements

The `switch` statement in Go is a multi-way branch statement. It provides an efficient way to dispatch execution to
different parts of code based on the value of an expression.

```go
switch expression {
case value1:
    // code block
case value2:
    // code block
default:
    // code block (optional)
}
```

Go's switch is more flexible than in some other languages: cases don't need to be constants, and the values do not need
to be integers.

## For Loops

The `for` loop is the only looping construct in Go. It can be used in several ways:

- Traditional for loop:
  ```go
  for initializer; condition; post {
      // code block
  }
  ```
- While-style loop (by omitting the initializer and post):
  ```go
  for condition {
      // code block
  }
  ```
- Infinite loop (by omitting the condition):
  ```go
  for {
      // code block
  }
  ```

## Defer Statement

The `defer` statement in Go is used to schedule a function call to be run after the completion of the execution of the
function in which `defer` is called. It's often used for cleanup activities.

```go
defer fmt.Println("Executed after the surrounding function completes")
```

## Goto Statement

Though generally advised against due to the potential for making code less readable, Go does support the `goto`
statement for jumping to a labeled statement elsewhere in the same function.

```go
goto Label
// ...
Label:
// code to jump to
```

## Break and Continue

In loops, `break` is used to exit the loop, and `continue` is used to skip the current iteration and proceed to the next
iteration.

## Best Practices in Control Flow:

- Use `if-else` and `switch` judiciously to make the code readable.
- Prefer `for` loops over `goto` for better readability and maintainability.
- Use `defer` for cleanup actions like closing files or releasing resources.
- Avoid complex nesting of control structures to maintain readability.

Control flow is a fundamental aspect of GoLang, guiding how different blocks of code are executed and under what
conditions, enabling developers to write efficient, readable, and maintainable code.