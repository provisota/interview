<!-- TOC -->
* [Reflection](#reflection)
  * [Best Practices](#best-practices)
  * [Example](#example)
  * [Conclusion](#conclusion)
<!-- TOC -->

# Reflection

Reflection in GoLang is a powerful feature that allows programs to inspect, and manipulate objects at runtime. It's
primarily provided by the `reflect` package. While powerful, it should be used judiciously, as improper use can lead to
complex, hard-to-read code and performance issues.

**`reflect` Package** - The `reflect` package in GoLang provides functionality to dynamically interact with objects
at runtime. It allows you to inspect types and values and call methods and functions dynamically.

**Types and Kinds**:

- In reflection, every value is represented as an `interface{}` type. The `reflect.TypeOf()` function returns the
  reflection `Type` that represents the dynamic type of the interface value.
- The `Kind` of a `reflect.Type` describes the underlying type of a Go value, like `Int`, `String`, `Slice`, etc.

**Value Inspection and Modification** - The `reflect.ValueOf()` function returns a `reflect.Value` which is a
runtime representation of a Go value. It can be used to inspect and modify the value.

**Struct Field Tag Reflection** - Struct field tags can be accessed using reflection, which is common for
decoding/encoding libraries.

## Best Practices

- **Use Sparingly**: Due to the complexity and performance cost, use reflection only when absolutely necessary.
- **Error Handling**: Always check for potential errors or panics, such as calling methods on nil pointers or trying to
  set unexportable fields.
- **Performance Awareness**: Reflection operations are relatively slow. Be aware of this in performance-critical code.

## Example

```go
package main

import (
    "fmt"
    "reflect"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    p := Person{"Alice", 30}
    reflectPerson(p)
}

func reflectPerson(i interface{}) {
    t := reflect.TypeOf(i)
    v := reflect.ValueOf(i)

    fmt.Printf("Type: %v\n", t)

    for i := 0; i < t.NumField(); i++ {
        field := t.Field(i)
        value := v.Field(i)
        fmt.Printf("%d. Field: %v, Value: %v, Tag: '%v'\n", i, field.Name, value, field.Tag.Get("json"))
    }
}
```

In this example, reflection is used to inspect a `Person` struct, including its fields, values, and struct tags.

## Conclusion

Reflection in GoLang offers the ability to write highly dynamic and flexible code, but it comes with trade-offs in terms
of performance and code maintainability. It's a powerful tool in the Go programmer's toolbox, especially useful in
serialization, deserialization, and in scenarios where types are not known until runtime. However, it should be used
carefully and sparingly to maintain code quality and performance.