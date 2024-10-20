# Stratigy Design Pattern

> **Definition**: Strategy Pattern defines a family of algorithms, encapsulates each algorithm, and makes the algorithms interchangeable within that family.

[Back to README](../README.md)

### Daigram

```mermaid
classDiagram
    class Animal {
    <<interface>>
        + eat()
    }

    class Cow {
       + eat()
    }

    class Lion {
       + eat()
    }

    class Ziraffe {
      + eat()
    }

    Animal <|-- Mobile
    Animal <|-- Laptop
    Animal <|-- Tablet
```

Here in the above daigram,
