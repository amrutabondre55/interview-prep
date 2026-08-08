## SOLID Principles

**SOLID** is a set of five principles that help us write code that is **easy to maintain, extend, test, and change**.

```text
S → Single Responsibility Principle
O → Open/Closed Principle
L → Liskov Substitution Principle
I → Interface Segregation Principle
D → Dependency Inversion Principle
```

---

## 1. S — Single Responsibility Principle

### What?

> **A class should have one responsibility and one reason to change.**

### Bad example

```java
class OrderService {

    public void createOrder() {
        // create order
    }

    public void sendEmail() {
        // send email
    }

    public void generateInvoice() {
        // generate invoice
    }
}
```

This class is doing three different jobs.

### Better

```java
class OrderService {

    public void createOrder() {
        // create order
    }
}
```

```java
class EmailService {

    public void sendEmail() {
        // send email
    }
}
```

```java
class InvoiceService {

    public void generateInvoice() {
        // generate invoice
    }
}
```

### Interview answer

> **“Single Responsibility means a class should have one responsibility and one reason to change. For example, in a Spring Boot application, I wouldn't put order creation, email sending, and invoice generation into one service. I would separate those responsibilities into different services.”**

---

# 2. O — Open/Closed Principle

### What?

> **A class should be open for extension but closed for modification.**

Meaning: when a new requirement comes, we should preferably **add new code rather than constantly modifying existing tested code**.

### Bad example

```java
class PaymentService {

    public void pay(String type) {

        if (type.equals("UPI")) {
            // UPI payment

        } else if (type.equals("CARD")) {
            // Card payment

        } else if (type.equals("NETBANKING")) {
            // Net banking
        }
    }
}
```

Every new payment method requires modifying this class.

### Better

```java
interface Payment {

    void pay();
}
```

```java
class UpiPayment implements Payment {

    public void pay() {
        System.out.println("UPI payment");
    }
}
```

```java
class CardPayment implements Payment {

    public void pay() {
        System.out.println("Card payment");
    }
}
```

Now if I need `WalletPayment`, I add another implementation:

```java
class WalletPayment implements Payment {

    public void pay() {
        System.out.println("Wallet payment");
    }
}
```

I don't have to modify the existing payment implementations.

### Interview answer

> **“Open/Closed means our code should be open for extension but closed for modification. For example, instead of adding more if-else conditions every time we introduce a new payment type, I can define a Payment interface and create separate implementations. This makes the system easier to extend without changing existing code.”**

---

# 3. L — Liskov Substitution Principle

This one is often confusing.

### What?

> **A child class should be usable wherever its parent class is expected without breaking the application's behavior.**

Classic example:

```java
class Bird {

    void fly() {
        System.out.println("Flying");
    }
}
```

Then:

```java
class Penguin extends Bird {

    @Override
    void fly() {
        throw new UnsupportedOperationException();
    }
}
```

Problem:

```java
Bird bird = new Penguin();

bird.fly(); // 💥
```

The child doesn't properly behave like the parent.

### Better design

```java
interface Bird {
}
```

```java
interface FlyingBird extends Bird {

    void fly();
}
```

```java
class Eagle implements FlyingBird {

    public void fly() {
        System.out.println("Flying");
    }
}
```

```java
class Penguin implements Bird {
}
```

Now Penguin isn't forced to implement something it can't support.

### Interview answer

> **“Liskov Substitution means a child class should be safely substitutable for its parent without changing the expected behavior. If a subclass needs to throw exceptions or violate the parent's expected behavior, the inheritance design is probably wrong.”**

---

# 4. I — Interface Segregation Principle

### What?

> **A class should not be forced to implement methods that it doesn't need.**

### Bad

```java
interface Employee {

    void work();

    void eat();

    void sleep();
}
```

Imagine we have:

```java
class Robot implements Employee {

    public void work() {
    }

    public void eat() {
        // Robot doesn't eat!
    }

    public void sleep() {
        // Robot doesn't sleep!
    }
}
```

Not a good design.

### Better

Split the interfaces:

```java
interface Workable {
    void work();
}
```

```java
interface Eatable {
    void eat();
}
```

```java
interface Sleepable {
    void sleep();
}
```

Now:

```java
class Robot implements Workable {

    public void work() {
        System.out.println("Robot working");
    }
}
```

And:

```java
class Human implements Workable, Eatable, Sleepable {

    public void work() {
    }

    public void eat() {
    }

    public void sleep() {
    }
}
```

### Interview answer

> **“Interface Segregation means we should prefer small, focused interfaces instead of one large interface. A class should only depend on methods that it actually needs.”**

---

# 5. D — Dependency Inversion Principle

⭐⭐ **Very important for Spring Boot interviews.**

### What?

> **High-level classes should depend on abstractions, not directly on low-level implementations.**

### Bad

```java
class OrderService {

    private MySQLRepository repository =
            new MySQLRepository();

    public void saveOrder() {
        repository.save();
    }
}
```

Now `OrderService` is tightly coupled to MySQLRepository.

If tomorrow I want MongoDB:

```text
OrderService
     ↓
MySQLRepository
```

I have to modify `OrderService`.

### Better

Create an interface:

```java
interface OrderRepository {

    void save();
}
```

Implementation:

```java
class MySQLRepository implements OrderRepository {

    public void save() {
        System.out.println("Saving to MySQL");
    }
}
```

Service depends on the interface:

```java
class OrderService {

    private final OrderRepository repository;

    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }

    public void saveOrder() {
        repository.save();
    }
}
```

Now:

```text
                 OrderRepository
                       ↑
              ┌────────┴────────┐
              │                 │
       MySQLRepository    MongoRepository
```

`OrderService` doesn't care which database implementation is being used.

### This is where Spring Boot comes in

Spring's dependency injection makes this pattern very easy:

```java
@Service
public class OrderService {

    private final OrderRepository repository;

    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
```

Spring injects the appropriate implementation.

### Interview answer

> **“Dependency Inversion means high-level business logic should depend on abstractions rather than concrete implementations. In Spring Boot, we commonly achieve this using interfaces and dependency injection. For example, my OrderService can depend on an OrderRepository interface instead of directly creating a MySQLRepository. This gives loose coupling and makes the code easier to test and change.”**

---

# ⭐ How I'd answer "Explain SOLID" in an interview

> **“SOLID is a set of five design principles that help us build maintainable and loosely coupled software. S stands for Single Responsibility, meaning one class should have one responsibility. O is Open/Closed, meaning we should extend functionality without unnecessarily modifying existing code. L is Liskov Substitution, meaning child classes should be substitutable for their parent without breaking behavior. I is Interface Segregation, meaning we should use small, focused interfaces rather than forcing classes to implement unnecessary methods. And D is Dependency Inversion, meaning high-level modules should depend on abstractions rather than concrete implementations.**
>
> **In my Spring Boot applications, I apply these principles using separate services, interfaces, dependency injection, and strategy-based implementations. This helps keep the code loosely coupled, testable, and easier to extend.”**

### Easy way to remember

```text
S → One job
O → Extend, don't keep modifying
L → Child should behave like parent
I → Small interfaces
D → Depend on interface, not implementation
```


Hmm. Okay. For Single Responsibility, in my Spring Boot project, my OrderService handles only order business logic, email and invoice are separate services. So each class has1 reason to change. For Open/Closed, instead of if-else for payments, we'd use a Payment interface with UpiPayment, CardPayment, etc. Adding WalletPayment doesn't modify existing code. For Liskov Substitution, every payment implementation follows the same contract, so the service can swap them without breaking behavior. For Interface Segregation, I split interfaces so a robot only implements Workable, not unnecessary methods. And for Dependency Inversion, my OrderService depends on an OrderRepository interface, and Spring injects the concrete implementation. So, in short, SRP, one job per class; OCP extend not modify; LSP, child behaves like parent contract. ISP small focused interfaces. DIP, depend on abstractions


