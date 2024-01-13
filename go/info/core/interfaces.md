<!-- TOC -->
* [Interfaces](#interfaces)
  * [Implicit Implementation](#implicit-implementation)
  * [Basic Interface Implementation](#basic-interface-implementation)
  * [Empty Interface](#empty-interface)
  * [Best Practices and Common Use Cases](#best-practices-and-common-use-cases)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Interfaces

Interfaces in GoLang are a powerful feature used to define behavior. Unlike some other languages, interfaces in Go are
implicit, meaning that a type implements an interface by implementing its methods, not by explicitly declaring that it
does so.

**Definition**

An interface is a type that specifies a set of method signatures. A Go type implements an interface by implementing all
the methods in the interface.

**Interface Types**

An interface type can hold any value that implements the set of methods.

**[Polymorphism](polymorphism.md)**

Interfaces enable polymorphism in Go. Functions that take interface parameters can be called with any value that
implements the interface.

**Empty Interface**

The interface type that specifies zero methods is known as the empty interface: `interface{}`. Since every type
implements zero methods, any type can be assigned to the empty interface.

## Implicit Implementation

In Go, a type implements an interface simply by having the methods that the interface requires. There's no need for
explicit declaration.

In Go, the process of verifying that a struct type satisfies an interface is done through what is often referred to as
"structural typing" or "implicit implementation." Unlike some other languages where you explicitly declare that a type
implements an interface, in Go, this is determined by whether the type has the necessary methods that the interface
requires.

Under the hood, this is how Go checks if a struct matches an interface:

**Interface Internal Representation**

In Go, an interface is internally represented as a tuple of two pointers:

- A pointer to a type descriptor, which describes the actual type stored in the interface.
- A pointer to the actual data represented by the interface.

**Method Set Verification**

When a variable of an interface type is assigned a value (for instance, an instance of a struct), Go checks whether the
struct's method set satisfies the interface. This means that for each method specified in the interface, there must be a
corresponding method with the same name and signature in the struct's method set.

**Type Descriptor and Method Table**

Each type in Go has a type descriptor, which includes information about the type's methods. This descriptor effectively
acts as a method table. When the Go runtime needs to check if a struct satisfies an interface, it looks at this method
table to ensure all methods required by the interface are present in the struct.

**Dynamic Dispatch**

When a method of an interface is called, Go uses the type descriptor to find the actual implementation of the method for
the type stored in the interface and then calls it. This is a form of dynamic dispatch.

**Compile-Time Check**

The majority of this checking happens at compile time. The Go compiler ensures that the methods required by an interface
are present in the struct. If a struct does not implement all the methods of an interface, the program will fail to
compile.

**Runtime Behavior**

While most of the verification is done at compile time, there are runtime behaviors too, especially when interfaces are
used in a more dynamic context, such as with reflection.

By using this approach, Go provides a flexible and powerful way to use interfaces, enabling polymorphism and decoupling
the definition of an interface from its implementation. This system checks conformance without needing explicit
declarations, leading to cleaner and more maintainable code.

## Basic Interface Implementation

```go
package main

import "fmt"

// Defining an interface
type Shape interface {
    Area() float64
}

// Structs implementing the Shape interface
type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return 3.14 * c.Radius * c.Radius
}

type Rectangle struct {
    Length, Width float64
}

func (r Rectangle) Area() float64 {
    return r.Length * r.Width
}

// Function that takes a Shape interface
func printArea(s Shape) {
    fmt.Println(s.Area())
}

func main() {
    c := Circle{Radius: 5}
    r := Rectangle{Length: 3, Width: 4}

    printArea(c)
    printArea(r)

    // Output:
    // 78.5
    // 12
}
```

## Empty Interface

The empty interface can hold values of any type, as every type implements at least zero methods.

```go
package main

import "fmt"

func printType(i interface{}) {
    fmt.Printf("Type: %T, Value: %v\n", i, i)
}

func main() {
    printType(42)
    printType("hello")
    printType(3.14)

    // Output:
    // Type: int, Value: 42
    // Type: string, Value: hello
    // Type: float64, Value: 3.14
}
```

## Best Practices and Common Use Cases

- **Designing Modular and Reusable Code**: Interfaces are great for creating modular, reusable code that can work with
  different types.
- **Testing**: Interfaces make it easier to mock dependencies in unit tests.
- **Decoupling**: Using interfaces can help decouple your code from specific implementations.

## Conclusion

Interfaces in GoLang are a fundamental concept that provide a way to achieve polymorphism and decouple code from
specific types. They are used extensively in GoLang's standard library and are a key part of effective GoLang
programming.