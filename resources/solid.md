# Solid Principals

> This will help in writing code in a more organized manner.

[Back to README](../README.md)

**S** - Single Responsibility Principle

**O** - Open/Closed Principle

**L** - Liskov Substitution Principle

**I** - Interface Segregation Principle

**D** - Dependency Inversion Principle

### Advantages of SOLID Principles

1. **Easy to understand**: It makes the code more readable and understandable.
2. **Avoid Duplicate Code**: It helps to avoid duplicate code.
3. **Easy to maintain**: It makes the code more maintainable.
4. **Easy to test**: It makes the code more testable.
5. **Reduce Complexity**: It reduces the complexity of the code.
6. **Flexible Software**: It makes the software more flexible.
7. **Scalable**: It makes the software more scalable.

## Single Responsibility Principle

> A class should have one, and only one, reason to change.

```java
import lombok.Data;

@Data
public class Marker {
    String name;
    String color;
    int year;
    int price;
}

@Data
public class Invoice {
    private Marker marker;
    private int quantity;

    public int calculateTotal() {
        return marker.getPrice() * quantity;
    }

    public void printInvoice() {
        // print invoice
    }

    public void saveToDB() {
        // save to DB
    }
}
```

**Is it following single responsibility principal?**

It is not following the single responsibility principle because the Invoice class is doing more than one thing. It is calculating the total, printing the invoice, and saving to the database.

### How to fix it?

Arrange classes in a way, that each class should have only one responsibility.

Breaking the Invoice class into below.

```java
import lombok.Data;

@Data
public class Invoice {
    private Marker marker;
    private int quantity;

    public int calculateTotal() {
        return marker.getPrice() * quantity;
    }
}


@Data
public class InvoiceDao {
    private invoice invoice;

    public void saveToDB() {
        // save to DB
    }
}

@Data
public class InvoicePrinter {
    private invoice invoice;

    public void printInvoice() {
        // print invoice
    }
}
```

Now, the Invoice class is only responsible for calculating the total, InvoiceDao class is responsible for saving to the database, and InvoicePrinter class is responsible for printing the invoice.
**Now, each class has only one responsibility.**

## Open/Closed Principle

> A class should be open for extension but closed for modification.

In our previous example, we have a InvoiceDao class that is responsible for saving the invoice to the database. Now, we want to save the invoice to the file system as well. We can extend the InvoiceDao class to save the invoice to the file system.

```java
@Data
public class InvoiceDao {
    private invoice invoice;

    public void saveToDB() {
        // save to DB
    }

    public void saveToFile() {
        // save to file
    }
}
```

Now, this doesn't follow **Open/Closed Principal** cause we are modifying the existing class. To fix this, we can create a new class that extends the InvoiceDao class and add the saveToFile method.

```java
public interface InvoiceDao {
    void save();
}

public class DBInvoiceDao implements InvoiceDao {
    private invoice invoice;

    @Override
    public void save() {
        // save to DB
    }
}

public class FileInvoiceDao implements InvoiceDao {
    private invoice invoice;

    @Override
    public void save() {
        // save to file
    }
}
```

## Liskov Substitution Principle

> Class B extends/implements class A, then class B should be able to replace class A without affecting the functionality of the program.

> Subclass should extend the capabilities of parent class not reduce it.

```java
interface Bike {
    void turnOnEngine();
    void accelerate();
}

class MotorCycle implements Bike {

    boolean IsEngineOn;
    int speed;

    @Override
    public void turnOnEngine() {
        this.IsEngineOn = true;
    }

    @Override
    public void accelerate() {
        this.sleep += 10;
    }
}

class Bicycle implements Bike {
    @Override
    public void turnOnEngine() {
        throw new AssertionError("Bicycle does not have an engine");
    }

    @Override
    public void accelerate() {
        // accelerate
    }
}
```

In the above example, the Bicycle class is not following the Liskov Substitution Principle because the Bicycle class is throwing an exception when the turnOnEngine method is called. The Bicycle class should not have the turnOnEngine method. Subclass (Bicycle) should extend the capabilities of the parent class (Bike) not reduce it.

## Interface Segregation Principle

> A client should never be forced to implement an interface that it doesn't use or clients shouldn't be forced to depend on methods they do not use.

```java
interface ResturantEmployee {
    void serveCustomers();
    void cookFood();
}

class Waiter implements ResturantEmployee {

    @Override
    public void serveCustomers() {
        System.out.println("serving the customer");
    }

    @Override
    public void cookFood() {
        // not its job
    }
}
```

In the above example, the Waiter class is not following the Interface Segregation Principle because the Waiter class is forced to implement the cookFood method which is not its job. The Waiter class should not have the cookFood or washDishes method.

To fix this, we can create a new interface for the Waiter class, slice the interfaces into such smaller parts that no chield class should override unwanted methos.

```java
interface Waiter {
    void serveCustomers();
    void takeOrers();
}

interface Chef {
    void cookFood();
    void decideMenu();
}

class WaiterImpl implements Waiter {
    @Override
    public void serveCustomers() {
        System.out.println("serving the customer");
    }

    @Override
    public void takeOrers() {
        System.out.println("taking orders");
    }
}

class ChefImpl implements Chef {
    @Override
    public void cookFood() {
        System.out.println("cooking food");
    }

    @Override
    public void decideMenu() {
        System.out.println("deciding menu");
    }
}
```

## Dependency Inversion Principle

> High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. i.e. A Class should depend on interface not on concrete class.

```java
class WiredKeyboard {
    public void type() {
        System.out.println("typing");
    }
}

class WiredMouse {
    public void click() {
        System.out.println("clicking");
    }
}

class MacBook {
    private final WiredKeyboard keyboard;
    private final WiredMouse mouse;

    public MackBook(WiredKeyboard keyboard, WiredMouse mouse) {
        this.keyboard = keyboard;
        this.mouse = mouse;
    }
}
```

In the above example, the MacBook class is depending on the WiredKeyboard and WiredMouse classes
(Concreet classes). Which is voilating the **Dependency Inversion Principal** and if in future we want to use WirelessKeyboard and WirelessMouse, we have to change the MacBook class. hence it should depend on interface not on concrete class.

To fix this, we can create an interface for the Keyboard and Mouse classes and make the MacBook class depend on the interface.

```java
interface Keyboard {
    void type();
}

interface Mouse {
    void click();
}

class WiredKeyboard implements Keyboard {
    @Override
    public void type() {
        System.out.println("typing");
    }
}

class WiredMouse implements Mouse {
    @Override
    public void click() {
        System.out.println("clicking");
    }
}

class MacBook {
    private final Keyboard keyboard;
    private final Mouse mouse;

    public MackBook(Keyboard keyboard, Mouse mouse) {
        this.keyboard = keyboard;
        this.mouse = mouse;
    }
}
```

---

[Back to README](../README.md)
