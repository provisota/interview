<!-- TOC -->
* [Scope](#scope)
  * [Block Scope](#block-scope)
  * [Function Scope](#function-scope)
  * [Package Scope](#package-scope)
  * [Capitalization and Exporting](#capitalization-and-exporting)
  * [Shadowing](#shadowing)
  * [Global Scope](#global-scope)
  * [Rules and Best Practices](#rules-and-best-practices)
<!-- TOC -->

# Scope

In GoLang, scope refers to the region of the program where a defined variable or identifier is accessible. Understanding
scope is crucial for managing the lifetime and accessibility of variables, as well as avoiding name conflicts. GoLang's
scope rules are straightforward and are based on the location of variable and function declarations.

## Block Scope

The most common scope within GoLang.

Variables declared inside a block `{}` are accessible only within that block.

Examples include variables declared inside function bodies, loops, `if` statements, and other curly-braced `{}` code
blocks.

```go
package main

import "fmt"

func main() {
    // Start of a block
    {
        a := 5 // 'a' is only accessible within this block
        fmt.Println(a)
    }
    // End of the block
    // fmt.Println(a) // This would result in an error as 'a' is not accessible here
}
```

## Function Scope

Variables declared in a function are accessible anywhere within the function, but not outside it.

This includes function parameters and any variables declared within the function body.

```go
package main

import "fmt"

func myFunction() {
    b := 10 // 'b' has function scope
    fmt.Println(b)
}

func main() {
    myFunction()
    // fmt.Println(b) // Error: 'b' is not accessible outside myFunction
}
```

## Package Scope

When a variable or function is declared outside of any function, it is accessible from any file within the same package.

This allows different files of the same package to share variables and functions.

```go
// File: main.go
package main

import "fmt"

var c = 20 // 'c' has package scope

func main() {
    fmt.Println(c) // Accessible here
    anotherFunction()
}

// File: another.go in the same package
package main

import "fmt"

func anotherFunction() {
    fmt.Println(c) // Accessible here as well
}
```

## Capitalization and Exporting

In GoLang, the visibility of a variable or function outside its package is determined by the case of the first letter of
its name.

```go
// File: mypackage.go
package mypackage

var internalVar = "internal" // lowercase, not exported, package scope
var ExternalVar = "external" // uppercase, exported, package scope
```

```go
// File: main.go
package main

import (
    "fmt"
    "mypackage"
)

func main() {
    // fmt.Println(mypackage.internalVar) // Error: not accessible
    fmt.Println(mypackage.ExternalVar) // Accessible
}
```

## Shadowing

GoLang allows variable shadowing. If a variable in a smaller (inner) scope has the same name as a variable in a larger (
outer) scope, the inner variable "shadows" the outer variable within its scope.

```go
package main

import "fmt"

var x = 10 // package scope

func main() {
    fmt.Println(x) // Prints 10
    x := 5         // New 'x' variable, shadows the package-level 'x'
    fmt.Println(x) // Prints 5
    // The package-level 'x' is still 10
}
```

## Global Scope

GoLang does not have a global scope in the same way that some other languages do.

The closest concept to a global scope in GoLang is the package-level scope where a variable is accessible across all
files of the same package.

## Rules and Best Practices

- **Capitalization Matters**: In GoLang, the visibility of a variable or function outside its package is determined by
  the case of the first letter of its name. If it starts with a capital letter, it is exported (visible outside the
  package); if it starts with a lowercase letter, it is not exported (visible only within the package).

- **Short Variable Declarations**: GoLang supports short variable declarations (`:=`) which are often used inside
  functions. These variables have a local scope to the block they are declared in.

- **Shadowing**: GoLang allows variable shadowing. If a variable in a smaller (inner) scope has the same name as a
  variable in a larger (outer) scope, the inner variable "shadows" the outer variable within its scope.

- **Lifetime of Variables**: The lifetime of a variable in GoLang is determined by its scope. Variables with block or
  function scope are destroyed once the block or function execution is completed. Package-level variables remain for the
  lifetime of the program.

Understanding scope in GoLang is fundamental to writing efficient and error-free code. It helps in managing variable
lifetimes, preventing name conflicts, and designing clean and modular code structures.