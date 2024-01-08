# Testing

## Test Types - Unit
Unit testing is a type of testing where individual units or components of a software are tested. The purpose is to validate that each unit of the software performs as designed.

## Integration
Integration testing is a level of software testing where individual units are combined and tested as a group. The purpose of this level of testing is to expose faults in the interaction between integrated units.

## Mocks
Mocks are objects that simulate the behavior of real objects. They are used in unit testing to create a controlled environment where the behavior of dependent objects can be controlled and monitored.

## Fakes
Fakes are objects that have working implementations, but not same as production one. They usually take some shortcut and have simplified version of production code.

## Stubs (Purpose)
Stubs are used in unit testing to provide canned answers to calls made during the test. They are used to test the behavior of a unit under test without involving its dependencies.

## Techniques to Write Testable Code
Techniques to write testable code include writing small, single-purpose functions, using dependency injection, and designing software in a modular way.

## TDD
Test-Driven Development (TDD) is a software development process where the developer writes a test before writing enough production code to fulfill that test.

## BDD
Behavior-Driven Development (BDD) is a software development process that encourages collaboration among developers, QA and non-technical or business participants in a software project.

## Questions
1. Which types of tests do you know and which problems they solve?
2. What are key differences between them?
3. Which patterns/technics allow you to isolate dependencies in your tests?
4. What is a difference between mock and fake?
5. How do you isolate third-party service dependencies (e.g. REST/grpc/email/etc services) in your tests?
6. Which development processes that allow to write testable code do you know?
7. What is the purpose of TDD?
8. Explain the TDD flow?
9. What is the purpose of BDD?
10. Explain BDD flow?

## Answers
1. The types of tests include unit tests, integration tests, functional tests, system tests, acceptance tests, etc. They solve different problems like validating individual units of code, testing the interaction between different units, validating the system as a whole, etc.
2. The key differences between these tests lie in their scope, what they test, and at what level of the system they operate. For example, unit tests are focused on individual units of code, while integration tests are focused on the interaction between units.
3. Techniques to isolate dependencies in tests include using mocks, stubs, and fakes, and using dependency injection to inject test doubles.
4. A mock is an object that we can set expectations on, while a fake is an object that has a working implementation, but not the same as the production one.
5. You can isolate third-party service dependencies in your tests by using test doubles such as mocks or fakes. These can simulate the behavior of the third-party service.
6. Development processes that allow to write testable code include Test-Driven Development (TDD), Behavior-Driven Development (BDD), and writing clean, modular, and loosely-coupled code.
7. The purpose of TDD is to make the code clearer, simpler, and bug-free.
8. The TDD flow involves first writing a failing test, then writing the minimal amount of code to make the test pass, and then refactoring the code while keeping the tests green.
9. The purpose of BDD is to improve communication between developers, QA, and non-technical or business participants, and to create software that matters.
10. The BDD flow involves first writing a failing acceptance test, then writing a failing unit test, then writing the code to make the unit test pass, and then refactoring the code. This is repeated until the acceptance test passes.