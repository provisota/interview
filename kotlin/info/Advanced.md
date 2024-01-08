# Basic language and standard library knowledge

## Syntax
Kotlin syntax is the set of rules defining how a Kotlin program is written and interpreted. The syntax is designed to be familiar to those who know Java, but it also incorporates features from other languages.

## Primitives
Kotlin has similar primitive types to Java, but they are not treated as special cases. All types, including primitives, are objects.

## Exception Handling
Exception handling in Kotlin is similar to Java. It uses `try`, `catch`, `finally` blocks to handle exceptions. Unlike Java, Kotlin does not have checked exceptions.

## Immutability
Immutability in Kotlin is achieved by declaring variables with `val` keyword. Once initialized, their value cannot be changed.

## Nullability
Kotlin has built-in null safety. It distinguishes nullable types (e.g., `String?`) and non-nullable types (e.g., `String`), and it requires explicit handling of nullable types.

## Functions
Functions in Kotlin are declared using the `fun` keyword. Kotlin supports top-level functions, member functions, local/nested functions, and extension functions.

## Collections
Kotlin has a rich standard library that provides a set of collections similar to Java's, including `List`, `Set`, `Map`, and their mutable counterparts.

## Generics
Generics in Kotlin are a means of parameterizing classes, interfaces, and functions by the types they operate on.

## Language Evolution (What's New)
Kotlin is continuously evolving. As of the latest version, Kotlin 1.6.0, new features include stable support for JVM IR backend, improved performance and exception handling for coroutines, and more.

## Lambdas
Lambdas in Kotlin are a type of function literal that can be stored in variables, passed as arguments, or returned from functions.

## Questions
1. How to create Mutable & immutable variables?
2. What are Mutable & immutable types?
3. How nullability is handled in Kotlin?
4. How to handle exceptions in Kotlin?
5. What collection types are relevant for Kotlin?
6. What is the key difference between mutable and immutable collections?
7. How could you create range and then progression?
8. What is sequence?
9. What difference between Iterator, ListIterator and MutableIterator?
10. What transformation operations do you know?
11. What does partition function do?
12. What is new in the latest Kotlin?
13. What are Extension, Inline, Infix functions? Scoped functions?
14. What are Generics. What is Reified type?
15. Kotlin specific types (Any, Unit, Nothing)
16. What difference between HashSet and LinkedHashSet?
17. When to use mutable and immutable collections?
18. What difference between fold and reduce?
19. Properties vs fields, Lazy loading, Delegated properties
20. What is Lambda or Higher-order functions?
21. What strategy Kotlin provides for backward compatibility between versions?

## Answers
1. You can create mutable variables using `var` and immutable variables using `val`.
2. Mutable types in Kotlin are those whose state can be changed after they are created, like `MutableList`, `MutableSet`, `MutableMap`. Immutable types are those whose state cannot be changed after they are created, like `List`, `Set`, `Map`.
3. Nullability is handled in Kotlin by distinguishing nullable types (e.g., `String?`) and non-nullable types (e.g., `String`). Nullable types must be explicitly handled to avoid null pointer exceptions.
4. Exceptions in Kotlin are handled using `try`, `catch`, `finally` blocks. Kotlin does not have checked exceptions, so there is no need to declare them in a function signature.
5. Relevant collection types in Kotlin include `List`, `Set`, `Map`, and their mutable counterparts `MutableList`, `MutableSet`, `MutableMap`.
6. The key difference between mutable and immutable collections is that mutable collections can be modified after they are created, while immutable collections cannot.
7. You can create a range in Kotlin using the `..` operator (e.g., `1..10`). You can create a progression using the `step` function (e.g., `1..10 step 2`).
8. A sequence in Kotlin is a type of collection that can lazily produce values one at a time.
9. `Iterator` allows iterating over a collection, `ListIterator` extends `Iterator` and allows bidirectional iteration over a list, `MutableIterator` extends `Iterator` and allows removing elements from the underlying collection during iteration.
10. Transformation operations in Kotlin include `map`, `filter`, `reduce`, `flatMap`, and more.
11. The `partition` function splits a collection into two collections based on a predicate.
12. The latest version of Kotlin, Kotlin 1.6.0, includes stable support for JVM IR backend, improved performance and exception handling for coroutines, and more.
13. Extension functions allow you to add functions to existing classes. Inline functions are functions that are expanded at the call site. Infix functions are functions that can be called using infix notation. Scoped functions (`let`, `run`, `with`, `apply`, `also`) are functions that introduce a new scope for an object.
14. Generics are a means of parameterizing classes, interfaces, and functions by the types they operate on. A reified type is a type that is preserved at runtime, available in inline functions with reified type parameters.
15. `Any` is the root of the Kotlin class hierarchy, `Unit` is a type that represents the absence of a meaningful value, `Nothing` is a type that represents "a value that never exists".
16. `HashSet` and `LinkedHashSet` both implement the `Set` interface, but `LinkedHashSet` also maintains the insertion order.
17. You should use mutable collections when you need to modify the collection after it's created, and immutable collections when you don't need to modify the collection and want to ensure it remains constant.
18. `fold` and `reduce` are both aggregation operations, but `fold` takes an initial value and a binary operation as parameters, while `reduce` only takes a binary operation and uses the first element of the collection as the initial value.
19. Properties in Kotlin are public by default and can be accessed directly. Fields are private variables inside a class. Lazy loading is a design pattern where initialization of an object occurs only when it is necessary. Delegated properties allow delegating property getter and setter logic to another class.
20. A lambda or higher-order function in Kotlin is a function that takes functions as parameters, or returns a function.
21. Kotlin provides backward compatibility by deprecating features before removing them, providing migration tools, and maintaining strict compatibility of the Kotlin language and the standard library.