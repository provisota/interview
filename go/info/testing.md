# Testing

# Test types (i.e. unit, integration), benchmarks

### Test Types and Benchmarks in GoLang

Testing is a crucial aspect of software development in GoLang. Go provides built-in support for various types of testing and benchmarking, allowing developers to ensure code quality and performance.

#### Technical Details

1. **Unit Tests**:
   - Focus on individual units of code, typically functions or methods.
   - Go's standard library provides the `testing` package for writing unit tests.
   - Unit tests are written in the same package as the code and usually in files with a `_test.go` suffix.

2. **Integration Tests**:
   - Test the integration of different parts of the application, such as how different packages or systems work together.
   - Can be achieved in Go by writing tests that cover the interaction between different components.

3. **Table-Driven Tests**:
   - A common pattern in Go for writing tests where test cases are represented as table entries, making it easy to add new cases.

4. **Benchmarks**:
   - Used for measuring and tracking the performance of code.
   - Go's `testing` package allows writing benchmark tests, typically prefixed with `Benchmark`, which can be run using `go test -bench`.

5. **Mocking**:
   - Involves replacing parts of the system under test with mock objects that simulate the behavior of real components.

#### Best Practices

- **Write Readable and Maintainable Tests**: Focus on clarity and simplicity. Remember, tests are also part of your codebase.
- **Cover Edge Cases in Unit Tests**: Ensure that unit tests cover a broad range of input conditions, including edge cases.
- **Isolate Units in Unit Testing**: Aim for unit tests to be independent of external systems or states.
- **Use Benchmarks for Performance Regressions**: Regularly run benchmark tests to catch performance regressions.
- **Mock External Dependencies in Integration Tests**: Use mocking to isolate the parts of the system you're integrating.

#### Example: Unit Test and Benchmark

Unit Test Example:

```go
package mypackage

import "testing"

func TestSum(t *testing.T) {
    total := Sum(5, 5)
    if total != 10 {
       t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
    }
}
```

Benchmark Example:

```go
func BenchmarkSum(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Sum(5, 5)
    }
}
```

Run the tests and benchmarks with:

```bash
go test -v      # Run tests
go test -bench=. # Run benchmarks
```

#### Conclusion

Effective testing is key to building reliable and maintainable software in GoLang. By leveraging Go's comprehensive testing framework, developers can write a variety of tests from unit to integration tests, as well as benchmarks to ensure both correctness and performance. Adopting a consistent testing strategy and following best practices helps in creating robust Go applications.

# Mock, fake and stub

### Mock, Fake, and Stub in GoLang

In GoLang testing, mock, fake, and stub are common techniques used to isolate and test units of code independently. They are particularly useful in unit testing where testing a piece of code in isolation from its dependencies is essential.

#### Technical Details

1. **Mock**:
   - A mock is an object that imitates the behavior of a real object in controlled ways.
   - It's typically used to mimic the behavior of complex real objects and often includes the ability to verify that certain actions have taken place.
   - In Go, libraries like `gomock` or `testify/mock` provide mocking frameworks.

2. **Fake**:
   - A fake is a lightweight implementation of an interface that behaves like the real object but in a simplified way.
   - Unlike mocks, fakes do not usually track interactions but provide a working implementation, for example, an in-memory database.

3. **Stub**:
   - A stub is an object that provides predetermined responses to method calls.
   - Stubs are primarily used to provide inputs to the system under test and are not used to verify outputs.

#### Best Practices

- **Use the Simplest Approach**: Choose the simplest form of test double (stub, mock, or fake) that fulfills your testing needs.
- **Isolation**: Use these techniques to isolate the unit of code under test, ensuring that the tests are not affected by external dependencies.
- **Clear Intent**: Make it clear in your tests what is being tested and why. The use of mocks, fakes, or stubs should be easily understandable.
- **Avoid Over-Mocking**: Excessive use of mocks can lead to fragile tests that are hard to maintain and understand.

#### Example: Using Mock in Go

Using `gomock` to create a mock:

```go
// Assuming you have an interface MyInterface
type MyInterface interface {
    DoSomething(string) int
}

// Test function using a mock
func TestMyFunction(t *testing.T) {
    ctrl := gomock.NewController(t)
    defer ctrl.Finish()

    mockObj := NewMockMyInterface(ctrl)
    mockObj.EXPECT().DoSomething(gomock.Eq("input")).Return(123)

    // test code here that uses mockObj
}
```

In this example, `gomock` is used to create a mock object for an interface `MyInterface`.

#### Conclusion

Mocks, fakes, and stubs are powerful tools in the GoLang testing ecosystem, providing ways to effectively isolate and test code units. Choosing the right tool depends on the specific requirements of what you need to test and how. Proper use of these testing techniques leads to more reliable, maintainable, and comprehensible test suites.

# Test-Driven Development (TDD)

### Test-Driven Development (TDD) in GoLang

Test-Driven Development (TDD) is a software development approach where tests are written before the actual code. In GoLang, TDD is a popular methodology due to the language's robust testing facilities.

#### Technical Details

1. **TDD Cycle**:
   - **Write a Failing Test**: Start by writing a test that fails because the functionality it tests is not implemented yet.
   - **Write the Minimal Code**: Write just enough code to make the test pass.
   - **Refactor**: Refine the code while keeping it green (passing all tests).

2. **Testing Package**:
   - GoLang's `testing` package provides the necessary tools to implement TDD, such as writing test cases and benchmarks.

3. **Test Naming Conventions**:
   - Tests in Go are typically named `TestXxx`, where `Xxx` is the name of the function being tested.

4. **Table-Driven Tests**:
   - A common pattern in Go TDD is using table-driven tests, where test cases are stored in a table structure for efficient testing of various inputs and outputs.

#### Best Practices

- **Small and Incremental Development**: Focus on writing small and manageable tests and corresponding code increments.
- **Run Tests Frequently**: Regularly run your entire test suite to ensure new changes haven't broken existing functionality.
- **Refactoring**: Use the safety net provided by the tests to refactor and improve your code confidently.
- **Collaboration and Documentation**: Use tests as a form of documentation to describe and understand the intended functionality.

#### Example: TDD in Go

Suppose you're implementing a function `Add` to add two integers. Start with the test:

```go
// add_test.go
package adder

import "testing"

func TestAdd(t *testing.T) {
    got := Add(1, 2)
    want := 3

    if got != want {
        t.Errorf("Add(1, 2) = %d; want %d", got, want)
    }
}
```

Initially, this test will fail because `Add` is not implemented yet. Next, implement the `Add` function:

```go
// add.go
package adder

func Add(a, b int) int {
    return a + b
}
```

Run the test again, and it should pass. You can then refactor if needed and re-run the test to ensure it still passes.

#### Conclusion

TDD in GoLang encourages writing cleaner, more testable code, often leading to higher quality software. By leveraging Go's strong support for testing, developers can practice TDD effectively, leading to well-designed, robust, and maintainable codebases. TDD not only helps in ensuring correctness but also aids in defining clear requirements and improving software design.

# Behavior-Driven Development (BDD)

### Behavior-Driven Development (BDD) in GoLang

Behavior-Driven Development (BDD) is a software development approach that emphasizes collaboration among developers, QA, and non-technical or business participants. It focuses on obtaining a clear understanding of desired software behavior through discussion with stakeholders.

#### Technical Details

1. **BDD Principles**:
   - BDD combines the general techniques and principles of TDD with ideas from domain-driven design.
   - It encourages collaboration between developers, QA, and business stakeholders to define the behavior of the system in a language understood by all.

2. **Specification Language**:
   - BDD tests are often written in a human-readable language (like Gherkin), describing the behavior of the application in a logical language that stakeholders can understand.

3. **Go BDD Frameworks**:
   - In Go, frameworks like `Ginkgo` and `GoConvey` offer BDD-style testing. These frameworks allow you to write specs in a descriptive language.

#### Best Practices

- **Define Behavior Before Implementation**: Start with defining the expected behavior of the system, often through user stories or scenarios.
- **Collaboration**: Involve all stakeholders, including business analysts, QA engineers, and developers, in the definition of behavior.
- **Automate Acceptance Criteria**: Translate behavior descriptions into automated tests, ensuring that the software meets the agreed-upon criteria.

#### Example: BDD in Go with Ginkgo

Using Ginkgo, you can write BDD-style tests like this:

First, install Ginkgo:

```bash
go get -u github.com/onsi/ginkgo/ginkgo
go get -u github.com/onsi/gomega/...
```

Then, write your specs:

```go
// calculator_test.go
package calculator_test

import (
    . "github.com/onsi/ginkgo"
    . "github.com/onsi/gomega"
    "example.com/calculator"
)

var _ = Describe("Calculator", func() {

    Describe("Adding two numbers", func() {
        Context("when both numbers are positive", func() {
            It("should return the sum", func() {
                sum := calculator.Add(2, 3)
                Expect(sum).To(Equal(5))
            })
        })
    })

})
```

Run your Ginkgo tests using:

```bash
ginkgo -r
```

#### Conclusion

BDD in GoLang helps bridge the gap between business requirements and technical implementation. By using frameworks like Ginkgo and GoConvey, teams can write tests that not only serve as specifications and documentation but also as a tool to ensure the application meets business needs. BDD promotes a collaborative approach to software development, focusing on delivering software that fulfills user expectations and business objectives.

# Questions
1. What are the most common types of tests and their usecases?
2. How to test code performance?
3. How to run tests in parallel?
4. What is the difference between mock, fake and stub?
5. How to make code more testable?
6. Which third-party tooling for testing do you know/use?
7. Development technics that allow to produce testable and better design code do you know? (TDD, BDD)
8. With what testing frameworks have you worked with? Describe their pros/cons.

# Answers
1. The most common types of tests are unit tests and integration tests. Unit tests are used to test individual components of the software, while integration tests are used to test the interaction between different components.
2. Code performance can be tested using benchmarks. In Go, you can write benchmarks using the `testing` package's `B` type.
3. Tests can be run in parallel using the `t.Parallel()` function in the `testing` package.
4. Mocks, fakes, and stubs are all types of test doubles. Mocks are used to verify interactions, fakes have working implementations, and stubs provide canned responses.
5. Code can be made more testable by writing small, pure functions, avoiding global state, and using interfaces to allow for easy mocking.
6. Third-party testing tools in Go include `testify` for more assertion options and `gomock` for generating mocks.
7. Test-Driven Development (TDD) and Behavior-Driven Development (BDD) are two techniques that can help produce more testable code.
8. The standard `testing` package in Go is a powerful framework for writing tests. It's simple and lightweight, but it lacks some features provided by other frameworks like `testify`, such as setup/teardown functions and a wider range of assertions.