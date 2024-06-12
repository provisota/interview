<!-- TOC -->
* [Encapsulation](#encapsulation)
  * [Technical Details of Encapsulation in GoLang](#technical-details-of-encapsulation-in-golang)
  * [Example of Encapsulation](#example-of-encapsulation)
  * [Best Practices for Encapsulation in GoLang](#best-practices-for-encapsulation-in-golang)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Encapsulation

Encapsulation is a fundamental concept in object-oriented programming (OOP) and involves bundling data with the methods
that operate on that data. It restricts direct access to some of an object's components, which is a means of preventing
unintended interference and misuse of the methods and data. In GoLang, which is not a purely object-oriented language,
encapsulation is achieved through the use of packages and visibility rules.

## Technical Details of Encapsulation in GoLang

**Package-based Encapsulation**:

- GoLang uses packages as a means of grouping related code. Each package acts as a namespace.
- Encapsulation in Go is managed at the package level. This means that whether a function or a variable is exported (
  available outside the package) or not is controlled by its naming.

**Exported vs Unexported Identifiers**:

- In Go, identifiers (names of variables, types, functions, etc.) that start with a capital letter are exported (visible
  and accessible outside the package).
- Identifiers that start with a lowercase letter are unexported (only accessible within the package).

**Structs for Holding Data and Methods**:

- Although Go does not have classes, it uses structs to group together data. Methods can be associated with these
  structs, effectively creating encapsulated objects.

**Pointer Receivers vs Value Receivers**:

- Methods in Go can have either pointer receivers or value receivers, which determines whether they can modify the
  struct's data or just read it.

## Example of Encapsulation

Here's a simple example demonstrating encapsulation in GoLang:

```go
package main

import (
    "fmt"
    "strings"
)

// A struct with both exported and unexported fields
type Person struct {
    Name   string // Exported
    age    int    // Unexported
}

// Constructor function for Person
func NewPerson(name string, age int) *Person {
    return &Person{name, age}
}

// Exported method
func (p *Person) Greet() string {
    return "Hello, " + p.Name
}

// Unexported method
func (p *Person) isAdult() bool {
    return p.age >= 18
}

func main() {
    person := NewPerson("John Doe", 30)
    fmt.Println(person.Greet()) // Accessible

    // fmt.Println(person.isAdult()) // Not accessible, as isAdult is unexported
    // fmt.Println(person.age)       // Not accessible, as 'age' is unexported
}
```

In this example, the `Person` struct has an unexported field `age` and an unexported method `isAdult`. These are
encapsulated within the package and not accessible from outside the package. The `Name` field and `Greet` method are
exported and can be accessed from other packages.

## Best Practices for Encapsulation in GoLang

- Use unexported identifiers to hide the internal implementation details of a package.
- Provide exported functions or methods to allow controlled access to the data.
- Use structs to create types that bundle data and methods together.
- When designing a package, think carefully about which parts of its API should be exported and which should remain
  unexported.

## Conclusion

Encapsulation in GoLang, while different from classical object-oriented languages, is a powerful feature for structuring
programs in a modular and maintainable way. By carefully controlling what is exported from a package, developers can
create well-defined APIs and hide implementation details, leading to cleaner and safer code.