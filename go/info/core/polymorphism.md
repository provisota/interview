<!-- TOC -->
* [Polymorphism](#polymorphism)
  * [Best Practices](#best-practices)
  * [Example](#example)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Polymorphism

Polymorphism in GoLang is primarily achieved through interfaces, which allow variables to hold values of different types
as long as those types implement the same set of methods. This concept is key to writing flexible and reusable code in
Go.

**Interface-Based Polymorphism**

In GoLang, polymorphism is not based on inheritance (as in traditional OOP languages) but on interfaces. A type is
considered to implement an interface if it possesses all the methods the interface requires.

**Dynamic Type Resolution**

When a variable of an interface type stores a value, that value can be of any type that implements the interface. The
actual type of the value can vary, giving rise to polymorphism.

**Type Assertions**:

Type assertions are a way to retrieve the dynamic value from an interface variable. They are used to extract and inspect
the underlying concrete type.

**Empty Interface (`interface{}`)**:

The empty interface can hold values of any type, as all types implement at least zero methods. It offers a form of
polymorphism but should be used with care.

## Best Practices

- **Define Minimal Interfaces**: Smaller interfaces are generally better in Go. They are easier to implement and
  combine.
- **Prefer Composition Over Inheritance**: GoLang encourages composition over inheritance. Use embedded structs to
  compose behaviors.
- **Interface Naming Conventions**: By convention, one-method interfaces are named by the method name plus an `-er`
  suffix, like `Reader`, `Writer`, `Formatter`, etc.

## Example

```go
package main

import "fmt"

// Animal interface
type Animal interface {
    Speak() string
}

// Dog struct
type Dog struct{}

func (d Dog) Speak() string {
    return "Woof!"
}

// Cat struct
type Cat struct{}

func (c Cat) Speak() string {
    return "Meow"
}

func main() {
    animals := []Animal{Dog{}, Cat{}}
    for _, animal := range animals {
        fmt.Println(animal.Speak())
    }

    // Output:
    // Woof!
    // Meow
}
```

In this example, `Dog` and `Cat` both implement the `Animal` interface. This allows them to be used interchangeably
where `Animal` is expected, demonstrating polymorphism.

## Conclusion

Polymorphism in GoLang, achieved through interfaces, is a powerful way to create flexible and reusable code. It allows
functions and methods to be written in a more general way, handling different types without needing to know the exact
types at compile time. Proper use of interfaces and understanding of polymorphism are key to mastering GoLang's approach
to object-oriented programming.