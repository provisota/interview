# Java Runtime

## JVM
The Java Virtual Machine (JVM) is an abstract computing machine that enables a computer to run a Java program. It is a runtime environment that executes Java bytecode by converting it into machine language.

## JDK
The Java Development Kit (JDK) is a software development environment used for developing Java applications. It includes the Java Runtime Environment (JRE), an interpreter/loader (Java), a compiler (javac), an archiver (jar), a documentation generator (Javadoc), and other tools needed in Java development.

## GC
Garbage Collection (GC) in Java is a process that automatically reclaims the runtime unused memory. It frees up the memory space by destroying the objects that are no longer in use.

## Memory Allocation Model
The Java memory model specifies how the Java virtual machine works with the computer's memory (RAM). It is divided into several regions: Heap, Stack, Code, and Static. The Heap is used for dynamic memory allocation for Java objects. The Stack holds local variables and partial results, and plays a part in method invocation and return. The Code and Static areas are used for storing bytecode and static variables respectively.

## JIT
Just-In-Time (JIT) compiler is a part of the JVM that improves the performance of Java applications by compiling bytecodes to native machine code at runtime. It compiles parts of the bytecode that have similar functionality at the same time, and hence reduces the amount of time needed for compilation.

## Class Loading
In Java, class loaders are part of the Java Runtime Environment (JRE) that dynamically loads Java classes into the JVM. They are used to load classes and interfaces.

## Specific Implementations (Graal VM, HotSpot, OpenJDK, etc)
These are different implementations of the JVM. GraalVM is a high-performance runtime that provides significant improvements in application performance and efficiency. HotSpot is the JVM from Oracle Corporation and is the JVM in the OpenJDK. OpenJDK is the open-source implementation of the Java Platform, Standard Edition.

## Questions
1. How is Java code executed?
2. What are JVM and JDK?
3. How does GC work?
4. How does JIT work?
5. How is bytecode optimized at runtime?

## Answers
1. Java code is compiled into bytecode by the Java compiler. The bytecode is a platform-independent code that is executed by the JVM. The JVM interprets the bytecode and translates it into machine code which is then executed by the machine.
2. JVM is a part of the Java Runtime Environment (JRE) that executes Java bytecode. JDK is a software development environment used for developing Java applications. It includes the JRE and development tools.
3. GC works by automatically reclaiming the runtime unused memory. It frees up the memory space by destroying the objects that are no longer in use.
4. JIT compiler improves the performance of Java applications by compiling bytecodes to native machine code at runtime. It compiles parts of the bytecode that have similar functionality at the same time, and hence reduces the amount of time needed for compilation.
5. Bytecode is optimized at runtime by the JIT compiler. The JIT compiler compiles the bytecode to native machine code just before it's executed, using various optimization techniques to improve the performance of the execution.