# Basic language and standard library knowledge

## Syntax
Java syntax is the set of rules defining how a Java program is written and interpreted. The syntax is mostly derived from C and C++. Java is case-sensitive, class-based, and compiled language.

## Primitives
Primitive types in Java are the basic types that are built-in to the language. They include `byte`, `short`, `int`, `long`, `float`, `double`, `char`, and `boolean`.

## OOP
Object-Oriented Programming (OOP) in Java is a programming paradigm that uses "objects" – data structures consisting of data fields and methods together with their interactions – to design applications and computer programs.

## Collections
Java Collections Framework provides a set of interfaces and classes such as `ArrayList`, `HashSet`, `HashMap`, etc. to store and manipulate a group of objects.

## Streams
Java Streams API is used to perform computation on a sequence of elements in a functional manner. It supports different types of iterations, parallel execution, and can be used with lambda expressions.

## Language Evolution (What's New)
Java is continuously evolving. As of the latest version, Java 17, new features include sealed classes, pattern matching for switch expressions, and more.

## Questions
1. What is new in the latest Java?
2. How do primitive types differ from classes?
3. What access level modifiers exist in Java?
4. What can you tell about the interfaces?
5. What most important collections exist in Java and their use cases?
6. How to filter and convert a list of objects into another using Stream API?
7. What will happen if we put a key object in a HashMap which is already there?
8. What is the contract between equals() and hashCode()?
9. Please describe key collections and use cases?
10. What is a method reference in Java?
11. What is a "Functional Interface"?
12. What Is the Difference Between Intermediate and Terminal Operations?
13. What is a spliterator in Stream API?
14. How do record classes work in Java?

## Answers
1. The latest version of Java, Java 17, includes features like sealed classes, pattern matching for switch expressions, and more.
2. Primitive types are basic types built into the language, they are not objects and have no methods. Classes, on the other hand, are complex types that can have fields and methods.
3. Java has four access level modifiers: `private`, `public`, `protected`, and package-private (no keyword).
4. Interfaces in Java are a blueprint for classes. They can contain method signatures, static methods, default methods, and static final variables.
5. Important collections in Java include `ArrayList`, `LinkedList`, `HashSet`, `LinkedHashSet`, `HashMap`, `TreeMap`, and `LinkedHashMap`.
6. You can use the `filter` and `map` methods in the Stream API to filter and convert a list of objects.
7. If you put a key object in a HashMap which is already there, it will replace the old value with the new one.
8. The contract between `equals()` and `hashCode()` is that if two objects are equal according to the `equals()` method, they must have the same `hashCode()`.
9. Key collections in Java include `ArrayList` for a resizable array, `LinkedList` for a doubly-linked list, `HashSet` for a set with no duplicates, and `HashMap` for a key-value pair collection.
10. A method reference in Java is a simplified form of a lambda expression. They are used to refer to methods by their names.
11. A Functional Interface in Java is an interface with just one abstract method. They can be used as a type for lambda expressions.
12. Intermediate operations in Java Stream API are operations that transform a stream into another stream, like `filter` and `map`. Terminal operations produce a result or a side-effect, like `collect`, `forEach`, `reduce`.
13. A spliterator in Java is an iterator for elements of a `Collection`. It can traverse elements individually (`tryAdvance()`) and sequentially (`forEachRemaining()`).
14. Record classes in Java are a special kind of class that is a transparent carrier for a fixed set of values, known as the record components. They provide a compact syntax for declaring classes which are supposed to be data carriers.