# Java Backend Developer Interview Preparation — Tomorrow

We’ll prepare all the important interview questions from your Java Backend Developer JD in simple English, with ready-to-speak interview answers, practical examples, and scenario-based questions.

Your main focus will be Core Java, Spring, Spring Boot, SQL, REST APIs, React, Maven, Git, CI/CD, AWS, Docker, and Kubernetes.

Preparation strategy: Don’t just memorize definitions. Learn answers you can explain confidently in an interview.

## 1. Tomorrow’s preparation roadmap

1 hour

Core Java — highest priority

OOP, collections, HashMap internal working, Java 8, Streams, exceptions, multithreading, `equals()` and `hashCode()`.

1 hour

Spring and Spring Boot

IoC, dependency injection, annotations, project architecture, REST APIs, validation, exception handling, JPA, and N+1 queries.

45 min

SQL and REST API scenarios

Joins, indexes, transactions, slow queries, HTTP methods, status codes, pagination, and production errors.

30 min

React and JavaScript

Props vs state, hooks, Axios, API integration, pagination, and virtualization.

45 min

AWS, Docker, Kubernetes, Maven, Git and CI/CD

Deployment flow, production support, logs, containers, and build pipelines.

30 min

Project and HR questions

Self-introduction, project architecture, responsibilities, production issue handling, and follow-up questions.

## 2. Core Java — interview-ready answers

### Q1. Tell me about OOP concepts in Java.

Interview answer:

“Java supports four main object-oriented programming concepts: encapsulation, inheritance, polymorphism, and abstraction.

- Encapsulation: Wrapping data and methods into a class and controlling access using access modifiers.
- Inheritance: Reusing the properties and methods of a parent class in a child class.
- Polymorphism: One method name can have different implementations, such as overloading and overriding.
- Abstraction: Hiding implementation details and exposing only essential functionality using interfaces and abstract classes.

In my projects, I use these concepts to create reusable, maintainable, and loosely coupled code.”

### Q2. What is the difference between overloading and overriding?

| Method overloading                                      | Method overriding                                |
| ------------------------------------------------------- | ------------------------------------------------ |
| Same method name, different parameters                  | Same method signature in a subclass              |
| Usually in the same class                               | Requires inheritance or interface implementation |
| Compile-time polymorphism                               | Runtime polymorphism                             |
| Return type alone cannot distinguish overloaded methods | Return type must be compatible                   |

Example:

```
// Overloading
int add(int a, int b) {
    return a + b;
}

int add(int a, int b, int c) {
    return a + b + c;
}
```

Interview answer: “Overloading means having methods with the same name but different parameter lists. Overriding means providing a new implementation of an inherited method.”

### Q3. What is the difference between an interface and an abstract class?

Interview answer:

“An interface defines a contract that implementing classes must follow. An abstract class can provide both abstract methods and common implementation. A class can implement multiple interfaces but can extend only one class. I use interfaces when I need flexibility and loose coupling, and abstract classes when related classes need to share common state or behavior.”

### Q4. What is the difference between `==` and `equals()`?

Interview answer:

“`==` compares primitive values or checks whether two object references point to the same object. The `equals()` method compares objects according to their equality implementation. For example, two different String objects can contain the same text, so `equals()` can return true while `==` returns false.”

```
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
```

### Q5. Explain `equals()` and `hashCode()`.

Interview answer:

“`equals()` determines whether two objects are logically equal, while `hashCode()` returns an integer used by hash-based collections. If two objects are equal according to `equals()`, they must have the same hash code. This contract is important when using HashMap and HashSet.”

Advanced follow-up: If you override `equals()`, you should generally override `hashCode()` as well. Otherwise, logically equal objects may behave unexpectedly in hash-based collections.

### Q6. Explain HashMap internal working.

Interview answer:

“HashMap stores data as key-value pairs. When we insert a key, Java calculates its hash code and uses it to determine a bucket. HashMap uses the key's hash and equality checks to locate the correct entry. If multiple keys map to the same bucket, a collision occurs. Java handles collisions using a linked structure and can convert a sufficiently populated bucket into a balanced tree under the applicable conditions.

HashMap allows one null key and multiple null values. It is not thread-safe.”

Example:

```
Map<String, Integer> employees = new HashMap<>();

employees.put("Amruta", 101);
employees.put("Rahul", 102);
employees.put("Amruta", 103);

System.out.println(employees.size());       // 2
System.out.println(employees.get("Amruta")); // 103
```

Why? Keys must be unique. Inserting `"Amruta"` again replaces its previous value; it does not create a third entry.

### Q7. Difference between ArrayList and LinkedList?

Interview answer:

“ArrayList uses a resizable array, so accessing an element by index is generally fast. LinkedList uses linked nodes, so accessing an element by index requires traversal. LinkedList can insert or remove elements efficiently when the relevant node is already known, but finding that position can take time. I generally prefer ArrayList for read-heavy operations and choose LinkedList only when its specific behavior is beneficial.”

### Q8. Difference between HashMap, Hashtable, and ConcurrentHashMap?

Interview answer:

“HashMap is not thread-safe and allows a null key and null values. Hashtable is a legacy synchronized map and does not allow null keys or values. ConcurrentHashMap is designed for concurrent access and generally provides better scalability than synchronizing an entire map. It does not allow null keys or values.”

### Q9. What are the differences between checked and unchecked exceptions?

Interview answer:

“Checked exceptions are checked by the compiler, so they must be caught or declared. Examples include `IOException` and `SQLException`. Unchecked exceptions are subclasses of `RuntimeException`, such as `NullPointerException` and `IllegalArgumentException`. I use appropriate exception handling and meaningful error responses to make applications easier to troubleshoot.”

### Q10. What is the difference between `final`, `finally`, and `finalize()`?

Interview answer:

“`final` is a keyword used to prevent reassignment, overriding, or inheritance depending on where it is applied. `finally` is a block generally used for cleanup after a try-catch statement. `finalize()` was a legacy garbage-collection-related method and is deprecated for removal; it should not be used for resource cleanup.”

### Q11. What are Java 8 features?

Interview answer:

“Important Java 8 features include lambda expressions, functional interfaces, the Stream API, method references, the Optional class, and default and static methods in interfaces. These features help reduce boilerplate code and support functional-style programming.”

```
List<Integer> numbers = Arrays.asList(10, 20, 30, 40);

numbers.stream()
       .filter(n -> n > 20)
       .forEach(System.out::println);
```

Output:

```
30
40
```

### Q12. What is a functional interface?

Interview answer:

“A functional interface is an interface with exactly one abstract method. It can be used with lambda expressions. Examples include `Runnable`, `Predicate`, `Function`, and `Consumer`. An interface can have multiple default and static methods and still be a functional interface.”

```
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

Calculator c = (a, b) -> a + b;
System.out.println(c.add(10, 20)); // 30
```

### Q13. Explain intermediate and terminal operations in Streams.

Interview answer:

“Intermediate operations transform a stream and are generally lazy. Examples include `filter()`, `map()`, and `sorted()`. Terminal operations produce a result or side effect and trigger processing, such as `collect()`, `forEach()`, and `count()`.”

```
long count = numbers.stream()
        .filter(n -> n > 20)
        .count();
```

Here, `filter()` is intermediate and `count()` is terminal.

### Q14. What is Optional in Java?

Interview answer:

“Optional is a container that may or may not contain a non-null value. It helps express potentially missing results and can reduce accidental null handling. I use methods such as `orElse()`, `orElseGet()`, `map()`, and `orElseThrow()` appropriately. I avoid using Optional as a replacement for every null check.”

### Q15. Difference between Thread and Runnable?

Interview answer:

“Thread represents a thread of execution, whereas Runnable represents a task that can be executed by a thread. Implementing Runnable separates the task from the thread and allows the class to extend another class. In real applications, I generally prefer an ExecutorService or a framework-managed task executor instead of creating many threads manually.”

### Q16. How do you handle multithreading issues?

Interview answer:

“I first identify whether the issue is a race condition, deadlock, thread starvation, or excessive contention. I use thread-safe data structures, synchronization, locks, or atomic classes when appropriate. For asynchronous tasks, I prefer managed thread pools and monitor thread usage, exceptions, and task execution time.”

### Q17. What is the difference between `synchronized` and `volatile`?

Interview answer:

“`volatile` provides visibility of a variable's latest value across threads, but it does not make compound operations such as incrementing atomic. `synchronized` provides mutual exclusion and memory-visibility guarantees for a critical section. I choose between them based on whether I need visibility alone or coordinated access to shared state.”

### Q18. What is an immutable class?

Interview answer:

“An immutable class is a class whose state cannot change after its object is created. To create one, I make the class final where appropriate, fields private and final, initialize them through the constructor, provide no setters, and make defensive copies of mutable objects. String is a common example of an immutable class.”

### Q19. What is the difference between Comparable and Comparator?

Interview answer:

“Comparable defines a class's natural ordering through `compareTo()`. Comparator defines an external or custom ordering through `compare()`. For example, I can sort employees by employee ID using Comparable and sort them by salary or name using different Comparator implementations.”

### Q20. What is garbage collection in Java?

Interview answer:

“Garbage collection automatically reclaims heap memory occupied by objects that are no longer reachable. Developers generally do not manually free Java objects. If memory usage keeps increasing, I inspect heap usage, garbage-collection logs, and heap dumps to identify retained objects or memory leaks.”

## 3. Spring Boot — most important interview questions

### Q1. What is Spring Boot?

Interview answer:

“Spring Boot is a framework built on top of the Spring Framework. It simplifies application development through auto-configuration, starter dependencies, and embedded servers. We can build standalone applications and REST APIs with less configuration. In my project, I use Spring Boot to develop backend APIs that communicate with the database and React frontend.”

### Q2. Explain Spring Boot project architecture.

Interview answer:

“I follow a layered architecture to separate responsibilities and make the application maintainable.”

Controller Layer

Receives HTTP requests and returns responses

Service Layer

Business logic and validation rules

Repository Layer

Database access through Spring Data JPA

Database

MySQL or PostgreSQL

“I also use entity and DTO classes, configuration, validation, logging, and global exception handling where appropriate.”

### Q3. What are IoC and Dependency Injection?

Interview answer:

“IoC, or Inversion of Control, means that Spring manages the creation and lifecycle of application beans. Dependency Injection is the mechanism through which Spring supplies required dependencies to a class. I prefer constructor injection because it makes dependencies explicit and simplifies unit testing.”

```
@Service
public class EmployeeService {

    private final EmployeeRepository repository;

    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }
}
```

### Q4. Explain important Spring annotations.

| Annotation               | Purpose                                                           |
| ------------------------ | ----------------------------------------------------------------- |
| `@SpringBootApplication` | Main application configuration and startup                        |
| `@RestController`        | Defines a REST controller                                         |
| `@Service`               | Marks the service layer                                           |
| `@Repository`            | Marks the persistence layer                                       |
| `@Autowired`             | Requests dependency injection; constructor injection is preferred |
| `@GetMapping`            | Handles HTTP GET requests                                         |
| `@PostMapping`           | Handles HTTP POST requests                                        |
| `@PutMapping`            | Handles HTTP PUT requests                                         |
| `@DeleteMapping`         | Handles HTTP DELETE requests                                      |
| `@RequestBody`           | Reads the request body                                            |
| `@PathVariable`          | Reads a value from the URL path                                   |
| `@RequestParam`          | Reads a query parameter                                           |
| `@Transactional`         | Defines a transaction boundary                                    |

### Q5. How do you create a REST API in Spring Boot?

Interview answer:

“I define the endpoint in the controller, implement the business logic in the service layer, and use a repository to interact with the database. I validate incoming requests, return suitable HTTP status codes, and handle exceptions consistently.”

Example endpoint:

```
@RestController
@RequestMapping("/api/employees")
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    @GetMapping("/{id}")
    public Employee getEmployee(@PathVariable Long id) {
        return service.getEmployeeById(id);
    }
}
```

This is a simplified example; a production API would generally return DTOs and handle not-found errors explicitly.

### Q6. What is the difference between `@Controller` and `@RestController`?

Interview answer:

“`@Controller` is commonly used for MVC controllers that return views. `@RestController` combines `@Controller` and `@ResponseBody`, so returned objects are written to the HTTP response body, typically as JSON.”

### Q7. How do you handle exceptions globally?

Interview answer:

“I use `@RestControllerAdvice` with `@ExceptionHandler` methods to handle exceptions centrally. For example, if an employee is not found, I return HTTP 404. For validation failures, I return HTTP 400. Unexpected errors are logged with a correlation or request ID and return a generic HTTP 500 response without exposing internal details.”

```
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(
        EmployeeNotFoundException.class
    )
    public ResponseEntity<String> handleNotFound(
            EmployeeNotFoundException ex) {

        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(ex.getMessage());
    }
}
```

### Q8. What is JPA? What is Hibernate?

Interview answer:

“JPA is a Java specification for object-relational mapping, while Hibernate is a popular implementation of JPA. Spring Data JPA provides repository abstractions that reduce boilerplate code for database operations. I use entity classes to map Java objects to database tables and repositories to perform CRUD operations.”

### Q9. What is the N+1 query problem?

Interview answer:

“The N+1 problem occurs when one query retrieves a list of records and additional queries execute for related data for each record. For example, one query loads 100 orders, and 100 more queries load customer details.

I investigate SQL logs and query counts, then consider fetch joins, entity graphs, DTO projections, or batch fetching. I choose the solution based on the actual access pattern and avoid fetching unnecessary data.”

### Q10. How do you optimize a slow Spring Boot API?

Interview answer:

“First, I reproduce the issue and measure response time. Then I check application logs, distributed traces, database query execution plans, and external service latency. I look for N+1 queries, missing indexes, unnecessary data retrieval, repeated processing, and inefficient network calls. After optimizing, I run load tests and compare latency and resource usage to confirm the improvement.”

### Q11. How do you handle an HTTP 500 error in production?

Interview answer:

“When a production API returns HTTP 500, I first identify the affected endpoint, time, frequency, and scope. I check application logs and stack traces using the request or correlation ID, then investigate database failures, null values, configuration problems, and downstream service errors. I reproduce the issue if possible, apply a tested fix, deploy through the approved pipeline, and monitor the API afterward.”

### Q12. How does pagination work in Spring Boot?

Interview answer:

“Pagination retrieves data in smaller pages instead of loading all records at once. In Spring Data JPA, I use `Pageable` and `PageRequest` to specify the page number and page size. The API returns the requested records and pagination metadata such as total pages and total elements.”

```
Pageable pageable = PageRequest.of(0, 20);
Page<Employee> page = repository.findAll(pageable);
```

Here, `0` means the first page and `20` is the page size.

### Q13. What is the difference between `@Component`, `@Service`, and `@Repository`?

Interview answer:

“All three are Spring component stereotypes and can be registered as beans through component scanning. `@Component` is generic, `@Service` communicates business-layer responsibility, and `@Repository` communicates persistence-layer responsibility and participates in persistence exception translation.”

## 4. REST API and HTTP questions

### Q1. Explain GET, POST, PUT, PATCH, and DELETE.

| Method | Purpose                                   | Example                 |
| ------ | ----------------------------------------- | ----------------------- |
| GET    | Retrieve data                             | Get employee by ID      |
| POST   | Create a resource or trigger an operation | Create employee         |
| PUT    | Replace a resource representation         | Update employee details |
| PATCH  | Partially update a resource               | Update employee email   |
| DELETE | Remove a resource                         | Delete employee         |

Interview answer: “I select HTTP methods according to the operation's meaning. GET should be safe, and PUT and DELETE are defined as idempotent. POST is not inherently idempotent, though an API can implement idempotency using a key.”

### Q2. Explain common HTTP status codes.

- `200 OK` — request succeeded.
- `201 Created` — resource created.
- `204 No Content` — successful request with no response body.
- `400 Bad Request` — invalid request.
- `401 Unauthorized` — authentication is missing or invalid.
- `403 Forbidden` — caller lacks permission.
- `404 Not Found` — resource does not exist.
- `409 Conflict` — conflict with current resource state.
- `500 Internal Server Error` — unexpected server-side failure.
- `503 Service Unavailable` — service temporarily unavailable.

### Q3. What is the difference between authentication and authorization?

Interview answer:

“Authentication verifies who the user is. Authorization checks what the authenticated user is allowed to do. For example, login verifies the user, while a role or permission check determines whether that user can access an administrative endpoint.”

### Q4. What is a stateless REST API?

Interview answer:

“A stateless API does not depend on server-side session context retained from a previous request to understand the current request. Each request contains the information needed to process it, such as authentication credentials. Statelessness makes scaling easier, although applications may still use databases, caches, and other shared storage.”

### Q5. How do you secure REST APIs?

Interview answer:

“I use Spring Security for authentication and authorization, validate incoming requests, enforce HTTPS, and apply least-privilege access. Depending on the application, I use OAuth 2.0 or OpenID Connect, securely validate tokens, protect sensitive configuration, and avoid exposing secrets or internal exception details in API responses.”

## 5. SQL and database interview answers

### Q1. What is the difference between INNER JOIN and LEFT JOIN?

Interview answer:

“INNER JOIN returns only records with matching values in both tables. LEFT JOIN returns every record from the left table and matching records from the right table; when there is no match, the right-side columns contain NULL.”

```
SELECT e.employee_name, d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

This returns all employees, including employees who do not have a matching department.

### Q2. What is an index?

Interview answer:

“An index is a database structure that helps retrieve rows more efficiently. It can improve SELECT queries that filter or join on indexed columns, but it consumes storage and can increase the cost of INSERT, UPDATE, and DELETE operations. I use query execution plans to decide whether an index is beneficial.”

### Q3. How do you optimize a slow SQL query?

Interview answer:

“I inspect the query execution plan, identify full table scans or expensive joins, check indexes, and retrieve only the required columns. I also check join conditions, filtering, data volume, and whether pagination is needed. Finally, I compare execution time before and after the change using representative data.”

### Q4. What is a database transaction? Explain ACID.

Interview answer:

“A transaction groups database operations into a logical unit. ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties help maintain data correctness when operations succeed, fail, or execute concurrently.”

### Q5. What is the difference between SQL and NoSQL?

Interview answer:

“SQL databases generally store structured data in relational tables and support SQL queries and relationships. NoSQL databases support models such as document, key-value, and wide-column storage. I select the database based on data structure, consistency needs, access patterns, relationships, and scalability requirements.”

### Q6. How do you find duplicate records?

```
SELECT email, COUNT(*) AS total
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

Interview answer: “I group records by the field that should be unique and use `HAVING COUNT(*) > 1` to identify duplicates. If uniqueness is a business requirement, I also consider enforcing it with a database constraint.”

## 6. React.js and JavaScript interview answers

### Q1. What is the difference between props and state?

Interview answer:

“Props are used to pass data from a parent component to a child component, and the child should treat them as read-only. State stores data managed by a component, and it can be updated using a state setter such as `setState` or the `useState` setter. When state changes, React can re-render the component.”

### Q2. What is `useState`?

Interview answer:

“`useState` is a React Hook used to store and update component state. It returns the current value and a setter function. When the setter updates the state, React schedules a re-render.”

```
const [count, setCount] = useState(0);

<button onClick={() => setCount(c => c + 1)}>
  Increment
</button>
```

### Q3. What is `useEffect`?

Interview answer:

“`useEffect` is used to synchronize a component with external
Now I understand your actual JD. This is a Java Backend Developer role focused on Java, Quarkus, Spring Boot, Microservices, Hibernate/JPA, SQL, Docker, and Kubernetes. We should prioritize these topics instead of spending too much time on React.

# 1. Your customized interview preparation plan

Priority 1 — Core Java 8/11/17+

OOP, immutable classes, Collections, HashMap internal working, Java 8 Streams, Optional, functional interfaces, exceptions, multithreading, and design patterns.

Must prepare

Priority 2 — Quarkus + Spring Boot + Microservices

Quarkus vs Spring Boot, dependency injection, CDI, REST endpoints, configuration, bean lifecycle, service-to-service communication, and fault tolerance.

Important

Priority 3 — Hibernate, JPA and SQL

Entity relationships, lazy/eager loading, N+1 problem, transactions, indexes, joins, query optimization, and pagination.

Priority 4 — Microservices, Kafka and REST APIs

HTTP methods, status codes, synchronous vs asynchronous communication, Kafka producer/consumer, retries, idempotency, and service failures.

Priority 5 — Docker, Kubernetes, Git and CI/CD

Dockerfile, image vs container, Pod, Deployment, Service, configuration, build pipelines, Git commands, and deployment troubleshooting.

## 2. Additional Quarkus questions you must prepare

### Q1. What is Quarkus?

Interview answer:

“Quarkus is a Java framework designed for cloud-native applications and microservices. It supports fast startup and efficient memory usage, particularly when using build-time optimizations and native compilation. It supports technologies such as CDI, REST APIs, Hibernate ORM with Panache, and configuration management. We can use it to develop scalable backend services.”

### Q2. What is the difference between Quarkus and Spring Boot?

| Quarkus                                                                | Spring Boot                                               |
| ---------------------------------------------------------------------- | --------------------------------------------------------- |
| Focuses strongly on build-time optimization and cloud-native workloads | Provides a broad application development ecosystem        |
| Uses CDI-based dependency injection through ArC                        | Uses the Spring IoC container                             |
| Supports native compilation through GraalVM/Mandrel                    | Also supports native compilation                          |
| Commonly uses extensions for framework capabilities                    | Commonly uses starter dependencies and auto-configuration |

Interview answer:

“Both frameworks are used to develop Java backend applications and microservices. Quarkus emphasizes build-time optimization and efficient startup, while Spring Boot offers a mature and extensive Spring ecosystem. The choice depends on application requirements, existing architecture, team expertise, and deployment constraints.”

### Q3. What is CDI in Quarkus?

Interview answer:

“CDI stands for Contexts and Dependency Injection. In Quarkus, its ArC implementation manages beans and injects dependencies. It helps reduce tight coupling between classes and makes applications easier to test and maintain.”

```
@ApplicationScoped
public class EmployeeService {

    public String getMessage() {
        return "Employee service is running";
    }
}
```

### Q4. How do you create a REST API in Quarkus?

Interview answer:

“I use Jakarta REST annotations to define endpoints, inject the service layer, validate incoming requests, and return appropriate HTTP responses. I keep business logic in the service class instead of putting it directly into the resource class.”

```
@Path("/employees")
@Produces(MediaType.APPLICATION_JSON)
public class EmployeeResource {

    @Inject
    EmployeeService employeeService;

    @GET
    public String getEmployees() {
        return employeeService.getMessage();
    }
}
```

This is a simplified example of a Quarkus REST resource.

## 3. Scenario-based questions from your JD

Prepare these answers especially well because the responsibilities specifically mention debugging and performance optimization.

1. Your API takes 5 seconds to respond. How will you troubleshoot it?
2. How do you resolve the N+1 query problem in Hibernate?
3. What happens when one microservice is unavailable?
4. How do you prevent duplicate message processing in Kafka?
5. How do you manage transactions when multiple database operations are involved?
6. How do you containerize a Java application using Docker?
7. A Kubernetes Pod keeps restarting. How do you investigate it?
8. How do you write unit tests using JUnit and Mockito?
9. How do you handle exceptions consistently across REST APIs?
10. How do you investigate a production issue without affecting users?

## 4. Let's start your mock interview

We'll proceed one question at a time. You answer in your own English, and I'll correct your answer, give you a score out of 10, and provide a polished answer you can speak in the interview.

Question 1

Core Java · Advanced

What is an immutable class in Java? How do you create one, and why is String immutable?

Try to answer in 3–6 sentences, as if you were speaking to the interviewer.

Immutable class in Java means once you create a class, we cannot change. And class as a private class name, we cannot access the another program. And immutable means once you create, we cannot change. Create class is like write a class as a private. String is immutable because once you create string, once you object create, we cannot be change. It is not modifying.

Submit my answer
