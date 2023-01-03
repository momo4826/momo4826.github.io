---
layout: post
title: Notes for people with no prior Java experience
date: 2023-01-03
categories: [Java]
tags: [Java]
---
Java is an **object-oriented** language with strict requirements:

1. Every Java file must contain a class declaration
   * This is not completely true, e.g. we can also declare “interfaces” in .java files that may contain code
2. All code lives inside a class*, even helper functions(all functions in Java are methods), global constants, etc.
3. To run a Java program, you typically define a main method using `public static void main(String[] args)`
4. Other syntax: 
   * All statements in Java must end in a semi-colon. 
   * We delimit the beginning and end of segments of code with `{ }`;



Java is **statically typed**:

* All variables, parameters, and methods must have a declared type.
* That type can never change.
* Expressions also have a type, e.g. `larger(5, 10) + 3` has type `int`.
* The **compiler** checks that all the types in your program are compatible **before the program ever runs**
  * e.g. `String x = larger(5, 10) + 3` will fail to compile.
  * The compiler ensures type consistency. If types are inconsistent, the program will not compile.
  * This is unlike a language like Python, where type checks are performed DURING execution.

**Differences between dynamic typing and static typing**:
1. Dynamically-typed languages perform type checking at runtime, while statically typed languages perform type checking at compile time. 
2. Statically-typed languages require you to declare the data types of your variables before you use them, while dynamically-typed languages do not.

<figure align="center">
    <img src = "/assets/images/computer%20science/static_typing_1.png">
    <figcaption>figure from <a href="https://www.youtube.com/watch?v=SixO3uPNAdk">CS61A</a>
    </figcaption>
</figure>


**Client Programs and Main Methods**. A Java program without a main method cannot be run directly using the java command. However, its methods can still be invoked using the main method of another class.

**Class Declaration**. Java classes can contain methods and/or variables. We say that such methods and variables are “members” of the class. **Members can be instance members or static members**. Static members are declared with the static keyword. Instance members are any members without the static keyword.

**Static vs. Instance methods**. The distinction between static and instance methods is incredibly important. Instance methods are actions that can only be taken by an instance of the class (i.e. a specific object), whereas static methods are taken by the class itself. An instance method is invoked using a reference to a specific instance, e.g. `d.bark()`, whereas static methods should be invoked using the class name, e.g. `Math.sqrt()`. Know when to use each.

**The `this` keyword**. Inside a method, we can use the this keyword to refer to the current instance. This is **equivalent to `self` in Python**.

# Comparison of Java and Python/C:

| Java                                            | Python                          | C                                                                                                              |
|-------------------------------------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------|
| high level                                      | high level                      | middle level, because binding of the gaps takes place between machine level language and high-level languages. |
| Compiled programming Language                   | Interpreted programming language | Compiled Language                                                                                              |
| Platform-unaffected | Platform independent            | Platform-specific                                                                                              |
| Object-oriented programming                     | Object-oriented programming     | Procedural Programming                                                                                         |
| Syntax rules are strictly followed. | It isn't necessary to use semicolon.                                | Syntax rules are strictly followed.                                                                            |
| statements are grouped by braces | statements are grouped by indentation | statements are grouped by braces|
| static typing                                   | dynamic typing                  | static typing                                                                                                  |
| fast                                            | slower                          | faster                                                                                                         |
| it uses automatic memory allocation.            | -------------------             | Memory allocation can be done by malloc in C                                                                   |
| It doesn’t offer control over garbage collection | -------------------             | It offers control over garbage collection, like `free()`                                                       |
| It doesn't support pointers                     | It doesn't support pointers     | It supports pointers                                                                                           |





# References
1. [CS61B slides1](https://docs.google.com/presentation/d/1cMb1ojgb5_g5GMPCKLwOrCZeB-tYd86eOy6ALrrt7zQ/edit#slide=id.g15f8eac95b_0_5)






