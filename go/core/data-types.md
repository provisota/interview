## Data Types in Go

Go, also known as Golang, has a variety of data types that are used to define the kind of data that a variable can hold. Here are the primary data types in Go:

### Basic Types

#### Boolean
`bool`: Represents a boolean value, true or false.
```go
var isActive bool = true
```

#### Numeric Types
##### Integers
- `int`, `int8`, `int16`, `int32`, `int64`
- `uint`, `uint8` (alias for byte), `uint16`, `uint32`, `uint64`, `uintptr`
```go
var a int = 10
var b int64 = 20
var c uint = 30
```
     
In Go, the default integer type is `int`. The size of `int` is platform-dependent:

- On 32-bit systems, `int` is 32 bits (4 bytes) long, equivalent to `int32`.
- On 64-bit systems, `int` is 64 bits (8 bytes) long, equivalent to `int64`.

This means that the size of `int` changes depending on the architecture of the system the code is running on. Therefore, it is important to be aware of the system architecture when using the default `int` type.     
     
##### Floating-point
Go provides two floating-point types, `float32` and `float64`, which are used to represent real numbers. These types follow the IEEE-754 standard for floating-point arithmetic.

```go
var x float32 = 3.14
var y float64 = 6.28
```

`float32`

- **Range**: Approximately 1.18e-38 to 3.4e+38.
- **Precision**: About 6 decimal digits.
- **Size**: 32 bits (4 bytes).

`float64`

- **Range**: Approximately 2.23e-308 to 1.8e+308.
- **Precision**: About 15 decimal digits.
- **Size**: 64 bits (8 bytes).

###### Structure of Floating-Point Numbers

Floating-point numbers are typically represented using three components:
1. **Sign bit**: Indicates whether the number is positive or negative.
2. **Exponent**: Encodes the magnitude of the number.
3. **Mantissa (or significand)**: Represents the precision bits of the number.

For `float32`:
- 1 bit for the sign.
- 8 bits for the exponent.
- 23 bits for the mantissa.

For `float64`:
- 1 bit for the sign.
- 11 bits for the exponent.
- 52 bits for the mantissa.

##### Complex Numbers
Go provides two complex number types, `complex64` and `complex128`, to represent complex numbers with real and imaginary parts.

`complex64`

- **Components**: Real and imaginary parts, both `float32`.
- **Size**: 64 bits (8 bytes).

`complex128`

- **Components**: Real and imaginary parts, both `float64`.
- **Size**: 128 bits (16 bytes).

```go
var z1 complex64 = 1 + 2i
var z2 complex128 = 3 + 4i
```

###### Structure of Complex Numbers

Complex numbers in Go are represented as pairs of floating-point numbers:
- The real part.
- The imaginary part.

For `complex64`:
- Real part: `float32`.
- Imaginary part: `float32`.

For `complex128`:
- Real part: `float64`.
- Imaginary part: `float64`.

###### Operations on Complex Numbers

You can perform arithmetic operations on complex numbers similar to real numbers:

```go
var a complex128 = 1 + 2i
var b complex128 = 3 + 4i

// Addition
var c = a + b // 4 + 6i

// Subtraction
var d = a - b // -2 - 2i

// Multiplication
var e = a * b // -5 + 10i

// Division
var f = a / b // 0.44 + 0.08i
```

These operations are built-in and follow the standard rules for complex arithmetic.

### Strings

#### Overview

Strings in Go are a sequence of bytes that represent text data. They are immutable, meaning once a string is created, it cannot be changed. Any modification to a string results in the creation of a new string.

#### String Declaration

Strings can be declared in two ways: using double quotes `""` for interpreted string literals and backticks `` ` ` ` for raw string literals.

##### Interpreted String Literals

Interpreted string literals are enclosed in double quotes and can contain escape sequences.

```go
var s1 string = "Hello, World!"
var s2 string = "Line 1\nLine 2"
```

##### Raw String Literals

Raw string literals are enclosed in backticks and do not process escape sequences.

```go
var s3 string = `Line 1
Line 2`
```

#### String Functions and Operations

Go provides a rich set of functions and operations to manipulate strings. These functions are found in the `strings` and `strconv` packages.

##### Length of a String

The `len` function returns the number of bytes in the string.

```go
length := len(s1) // 13
```

##### Concatenation

Strings can be concatenated using the `+` operator.

```go
s4 := "Hello, " + "World!"
```

##### Accessing Characters

You can access individual bytes of a string using indexing. Note that this returns the byte at the specified index, not the character.

```go
char := s1[0] // 72 (ASCII value of 'H')
```

##### Iterating Over Characters

To iterate over the characters (runes) in a string, use a `for` range loop.

```go
for i, c := range s1 {
    fmt.Printf("Index: %d, Character: %c\n", i, c)
}
```

##### Substrings

You can obtain a substring using slicing.

```go
substr := s1[0:5] // "Hello"
```

#### String Comparison

Strings in Go can be compared using the `==`, `!=`, `<`, `<=`, `>`, and `>=` operators.

```go
isEqual := s1 == s4 // false
isLess := s1 < s4   // true
```

#### String Functions in the `strings` Package

The `strings` package provides many useful functions for string manipulation.

##### Contains

```go
contains := strings.Contains(s1, "World") // true
```

##### HasPrefix and HasSuffix

```go
hasPrefix := strings.HasPrefix(s1, "Hello") // true
hasSuffix := strings.HasSuffix(s1, "World!") // true
```

##### Index and LastIndex

```go
index := strings.Index(s1, "World")       // 7
lastIndex := strings.LastIndex(s1, "o")   // 8
```

##### Split and Join

```go
parts := strings.Split(s1, ", ")          // ["Hello", "World!"]
joined := strings.Join(parts, ", ")       // "Hello, World!"
```

##### Replace

```go
replaced := strings.Replace(s1, "World", "Go", 1) // "Hello, Go!"
```
#
#### ToUpper and ToLower

```go
upper := strings.ToUpper(s1) // "HELLO, WORLD!"
lower := strings.ToLower(s1) // "hello, world!"
```

#### Converting Strings

The `strconv` package provides functions to convert between strings and other data types.

##### String to Int

```go
i, err := strconv.Atoi("123")
```

##### Int to String

```go
s := strconv.Itoa(123)
```

##### String to Float

```go
f, err := strconv.ParseFloat("3.14", 64)
```

##### Float to String

```go
s := strconv.FormatFloat(3.14, 'f', 2, 64)
```

#### Unicode and Runes

Go's strings are UTF-8 encoded, and you can work with Unicode characters using runes. A rune is an alias for `int32` and represents a Unicode code point.

##### Converting String to Runes

```go
runes := []rune(s1)
```

##### Converting Runes to String

```go
s := string(runes)
```

#### Example Usage

Here is an example program demonstrating various string operations:

```go
package main

import (
    "fmt"
    "strings"
    "strconv"
)

func main() {
    s1 := "Hello, World!"
    fmt.Println("Original String:", s1)

    // Length of the string
    fmt.Println("Length:", len(s1))

    // Concatenation
    s2 := s1 + " How are you?"
    fmt.Println("Concatenated String:", s2)

    // Accessing characters
    fmt.Printf("First character: %c\n", s1[0])

    // Iterating over characters
    fmt.Println("Characters:")
    for i, c := range s1 {
        fmt.Printf("Index: %d, Character: %c\n", i, c)
    }

    // Substring
    substr := s1[7:12]
    fmt.Println("Substring:", substr)

    // Contains
    fmt.Println("Contains 'World':", strings.Contains(s1, "World"))

    // Prefix and Suffix
    fmt.Println("Has Prefix 'Hello':", strings.HasPrefix(s1, "Hello"))
    fmt.Println("Has Suffix 'World!':", strings.HasSuffix(s1, "World!"))

    // Index and LastIndex
    fmt.Println("Index of 'World':", strings.Index(s1, "World"))
    fmt.Println("Last Index of 'o':", strings.LastIndex(s1, "o"))

    // Split and Join
    parts := strings.Split(s1, ", ")
    fmt.Println("Split:", parts)
    joined := strings.Join(parts, ", ")
    fmt.Println("Joined:", joined)

    // Replace
    replaced := strings.Replace(s1, "World", "Go", 1)
    fmt.Println("Replaced:", replaced)

    // ToUpper and ToLower
    fmt.Println("ToUpper:", strings.ToUpper(s1))
    fmt.Println("ToLower:", strings.ToLower(s1))

    // String to Int and Int to String
    i, _ := strconv.Atoi("123")
    fmt.Println("String to Int:", i)
    s3 := strconv.Itoa(123)
    fmt.Println("Int to String:", s3)

    // String to Float and Float to String
    f, _ := strconv.ParseFloat("3.14", 64)
    fmt.Println("String to Float:", f)
    s4 := strconv.FormatFloat(3.14, 'f', 2, 64)
    fmt.Println("Float to String:", s4)

    // Unicode and Runes
    runes := []rune(s1)
    fmt.Println("Runes:", runes)
    s5 := string(runes)
    fmt.Println("Runes to String:", s5)
}
```

This comprehensive overview provides detailed information about strings in Go, covering declaration, manipulation, and conversion.

### Composite Types

1. **Arrays**:
   - Fixed-size sequence of elements of a single type.
   ```go
   var arr [3]int = [3]int{1, 2, 3}
   ```

2. **Slices**:
   - Dynamic arrays, more flexible than arrays.
   ```go
   var slice []int = []int{1, 2, 3, 4}
   ```

3. **Maps**:
   - Key-value pairs, similar to dictionaries or hash tables.
   ```go
   var m map[string]int = map[string]int{"one": 1, "two": 2}
   ```

4. **Structs**:
   - Collection of fields, useful for creating complex data types.
   ```go
   type Person struct {
       Name string
       Age  int
   }

   var p Person = Person{Name: "Alice", Age: 30}
   ```

5. **Pointers**:
   - Variables that store memory addresses of other variables.
   ```go
   var a int = 10
   var ptr *int = &a
   ```

### Interface Types

1. **Interfaces**:
   - Define a set of method signatures.
   ```go
   type Reader interface {
       Read(p []byte) (n int, err error)
   }
   ```

2. **Empty Interface**:
   - Can hold values of any type.
   ```go
   var i interface{} = "hello"
   ```

### Function Types

- Functions are first-class citizens in Go and can be assigned to variables.
```go
func add(a int, b int) int {
    return a + b
}

var f func(int, int) int = add
```

## Q&A

### Q1: What are the main advantages of using Go’s static typing system?

**A**: 
- **Type Safety**: Prevents operations on incompatible types, reducing bugs.
- **Performance**: Allows for more efficient code compilation and execution.
- **Clarity**: Makes the code more readable and self-documenting, as types provide insight into the data being used.

### Q2: Explain the difference between an array and a slice in Go.

**A**:
- **Array**: Fixed-size sequence of elements of a single type. The size is specified at the time of declaration and cannot be changed.
- **Slice**: Dynamic array, which is more flexible than arrays. It can grow and shrink as needed. Slices are backed by arrays and provide a more convenient and powerful way to handle collections of data.

### Q3: How does Go handle string immutability?

**A**: 
- Strings in Go are immutable, meaning once a string is created, it cannot be modified. Any operation that appears to modify a string actually creates a new string.

### Q4: What is a pointer in Go, and how do you use it?

**A**: 
- A pointer is a variable that stores the memory address of another variable. Pointers are used to indirectly access and modify the value of the variable they point to.
```go
var a int = 10
var ptr *int = &a // ptr now holds the address of a
*ptr = 20 // modifies the value of a through the pointer
```

### Q5: Can you explain what an interface is in Go and give an example?

**A**: 
- An interface in Go is a type that specifies a set of method signatures. A type implements an interface by implementing its methods. Interfaces allow for polymorphism and decoupling of code.
```go
type Reader interface {
    Read(p []byte) (n int, err error)
}

type File struct {
    // File-specific fields
}

func (f *File) Read(p []byte) (n int, err error) {
    // Implementation of the Read method
    return 0, nil
}

var r Reader = &File{}
```

### Q6: How does Go handle error handling?

**A**: 
- Go uses a simple and explicit error handling model. Functions that can result in an error return an error value as the last return value. The caller is responsible for checking this value to determine if an error occurred.
```go
func divide(a, b int) (int, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

result, err := divide(10, 0)
if err != nil {
    fmt.Println("Error:", err)
} else {
    fmt.Println("Result:", result)
}
```

This overview provides a solid foundation on Go's data types and addresses common interview questions that may be encountered for a Senior Golang Software Engineer position.
