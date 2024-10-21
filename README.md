# Low-Level Design Notes

Author: [Prafull Saxena](https://www.linkedin.com/in/prafullsaxena)

## Basics

Before going further into the notes, let's understand some basic concepts of Low-Level Design (LLD).

[Relationships in UML](./resources/uml.md)

## Index

1. [SOLID Principles](./resources/solid.md)
   - **Single Responsibility Principle**: A class should have one, and only one, reason to change.
   - **Open/Closed Principle**: A class should be open for extension but closed for modification.
   - **Liskov Substitution Principle**: Subtypes must be substitutable for their base types without altering the correctness of the program.
   - **Interface Segregation Principle**: Clients should not be forced to depend on interfaces they do not use.
   - **Dependency Inversion Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. [Strategy Pattern](./resources/strategy-pattern.md)
   - **Definition**: Strategy Pattern defines a family of algorithms, encapsulates each algorithm, and makes the algorithms interchangeable within that family.
   - **Advantages**: It allows the client to choose the algorithm at runtime.
3. [Observer Pattern](./resources/observer-pattern.md)
   - **Definition**: Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
   - **Advantages**: It supports the principle of loose coupling between objects.
4. [Decorator Pattern](./resources/decorator-pattern.md)
   - **Definition**: Decorator Pattern attaches additional responsibilities to an object dynamically. It provides a flexible alternative to subclassing for extending functionality.
   - **Advantages**: It allows adding new functionality to an object without altering its structure.

## About

This repository contains my notes on Low-Level Design (LLD) principles and patterns. The notes are written in Markdown format for easy readability and sharing.

I have made these notes from various sources like books, articles, and videos. below are some credtis to original authors:

- [Refactoring Guru](https://refactoring.guru/)
- [lldcoding](https://lldcoding.com/)
- [Shrayansh Jain | Low Level Design (LLD) from Basics to Advanced](https://www.udemy.com/course/lld-from-basics-to-advanced/?couponCode=LEARNNOWPLANS)

Feel free to explore and learn from these notes. Contributions and suggestions are welcome!

Please leve a ⭐ if you find this repository helpful.
