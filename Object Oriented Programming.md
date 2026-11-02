# Object-Oriented Programming (OOP) and Refactoring Legacy Code

## 1. Scenario Context

After joining a software development team, I started exploring an existing Java project that had been maintained for several years. The codebase contained duplicated logic, large methods, global data, and tightly connected classes. Even a small change in one method sometimes affected other parts of the application.

Maintaining this kind of code becomes difficult as the project grows. I realized that applying Object-Oriented Programming (OOP) concepts could make the code easier to understand, modify, and test. Instead of keeping all the logic in separate methods, we can organize responsibilities into classes and objects.

## 2. Core OOP Concepts for Refactoring

### 2.1 Encapsulation

Encapsulation means keeping data and the methods that operate on it together inside a class. It also controls how other classes access that data.

Before refactoring:

```java
class Employee {
    public double salary = 25000;
}
```

After refactoring:

```java
class Employee {
    private double salary;

    public Employee(double salary) {
        this.salary = salary;
    }

    public void updateSalary(double amount) {
        if (amount > 0) {
            salary = amount;
        }
    }

    public double getSalary() {
        return salary;
    }
}
```

By making salary private, we prevent other classes from modifying it directly. Validation is handled inside the class, which makes the code safer and easier to maintain.

### 2.2 Abstraction

Abstraction hides implementation details and exposes only the necessary operations.

```java
abstract class Payment {
    abstract void pay(double amount);
}

class CardPayment extends Payment {
    void pay(double amount) {
        System.out.println("Paid using card: " + amount);
    }
}

class UPIPayment extends Payment {
    void pay(double amount) {
        System.out.println("Paid using UPI: " + amount);
    }
}
```

The calling code only needs to use the `pay()` method. It does not need to know how each payment method works internally.

### 2.3 Inheritance and Polymorphism

Inheritance allows a class to reuse the properties and methods of another class. Polymorphism allows different classes to implement the same method in different ways.

```java
class Employee {
    void work() {
        System.out.println("Employee is working");
    }
}

class Developer extends Employee {
    @Override
    void work() {
        System.out.println("Developer is writing code");
    }
}

class Tester extends Employee {
    @Override
    void work() {
        System.out.println("Tester is testing software");
    }
}

public class Main {
    public static void main(String[] args) {
        Employee[] team = {
            new Developer(),
            new Tester()
        };

        for (Employee member : team) {
            member.work();
        }
    }
}
```

Both classes inherit from `Employee`, but each provides its own implementation of `work()`. We can add new employee types without changing the existing calling logic.

## 3. Benefits of Applying OOP During Refactoring

* Encapsulation protects data and keeps validation in one place.
* Abstraction hides unnecessary implementation details.
* Inheritance reduces code duplication through reuse.
* Polymorphism avoids complicated conditional statements.
* Classes separate responsibilities and make testing easier.
* Changes become easier to manage without affecting unrelated parts of the application.

OOP should be applied where it makes the code clearer. Creating unnecessary classes can also make a project complicated. The main goal is to keep each class focused on its responsibility.

## 4. References

* [Oracle Java Documentation - Classes and Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/)
* [GeeksforGeeks - Object-Oriented Programming in Java](https://www.geeksforgeeks.org/java/object-oriented-programming-oops-concept-in-java/)
* [Martin Fowler - Refactoring](https://refactoring.com/)
* [Refactoring Guru - Design Patterns](https://refactoring.guru/design-patterns)
