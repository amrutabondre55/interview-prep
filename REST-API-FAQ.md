Absolutely. Below is a **3–4 years experienced Java/Spring Boot interview-ready REST API Q&A set**. I’ll use the exact format you asked for:

**What → Why → How → Real Project Example → Interview Answer**

---

# 1. What is REST API?

### What?

REST stands for **Representational State Transfer**. REST API is an architectural style used to allow applications to communicate over HTTP.

### Why?

We use REST APIs because they are:

* Lightweight
* Scalable
* Stateless
* Easy to integrate with React, Angular, mobile apps, etc.

### How?

A client sends an HTTP request:

```text
GET /api/v1/employees/101
```

The server processes it and returns a representation, usually JSON.

### Real Project Example

In an Employee Management System:

```text
GET /api/v1/employees/101
```

returns:

```json
{
  "id": 101,
  "employeeCode": "EMP101",
  "firstName": "John",
  "department": "IT"
}
```

### Interview Answer

> "REST API is an architectural style for building web services using HTTP. In my project, I used REST APIs to communicate between the React frontend and Spring Boot backend. I followed REST principles such as stateless communication, resource-based URLs, HTTP methods, DTOs and proper HTTP status codes."

---

# 2. What are REST principles?

### What?

Important REST principles include:

1. Client-Server
2. Statelessness
3. Cacheability
4. Uniform Interface
5. Layered System
6. Code on Demand — optional

### Why?

These principles make APIs scalable, maintainable and loosely coupled.

### How?

For example, statelessness means the server doesn't maintain client session state between requests.

```text
Request 1 → contains required information
Request 2 → contains required information
```

### Real Project Example

For:

```text
GET /api/v1/employees/101
```

the server doesn't depend on a previous request from that client.

### Interview Answer

> "REST follows principles such as client-server architecture, statelessness, cacheability, uniform interface and layered architecture. In my project, I mainly follow stateless communication, resource-based URLs and standard HTTP methods."

---

# 3. GET vs POST vs PUT vs PATCH vs DELETE

### What?

| Method | Purpose                 |
| ------ | ----------------------- |
| GET    | Retrieve                |
| POST   | Create                  |
| PUT    | Full update/replacement |
| PATCH  | Partial update          |
| DELETE | Delete                  |

### Why?

HTTP methods communicate the intention of the operation clearly.

### How?

```text
GET    /employees/101
POST   /employees
PUT    /employees/101
PATCH  /employees/101
DELETE /employees/101
```

### Real Project Example

To create an employee:

```http
POST /api/v1/employees
```

To update salary only:

```http
PATCH /api/v1/employees/101
```

### Interview Answer

> "I use GET for retrieving resources, POST for creating resources, PUT for complete replacement, PATCH for partial updates and DELETE for removing resources."

---

# 4. PUT vs PATCH

### What?

**PUT** generally represents a complete update/replacement.

**PATCH** represents a partial update.

### Why?

It tells the API exactly what kind of update the client is requesting.

### How?

PUT:

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "email": "john@test.com",
  "department": "IT",
  "salary": 80000,
  "status": "ACTIVE"
}
```

PATCH:

```json
{
  "salary": 90000
}
```

### Real Project Example

If an employee changes department:

```http
PATCH /api/v1/employees/101
```

```json
{
  "department": "Finance"
}
```

### Interview Answer

> "PUT is generally used when I want to replace or fully update a resource, whereas PATCH is used for partial updates. For example, if I only want to change an employee's salary, PATCH is more appropriate."

---

# 5. Explain HTTP Status Codes

### What?

HTTP status codes tell the client the result of the request.

### Why?

They provide standardized communication between client and server.

### How?

Common codes:

```text
200 → OK
201 → Created
204 → No Content
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
409 → Conflict
500 → Internal Server Error
```

### Real Project Example

Employee created:

```text
POST /employees
→ 201 CREATED
```

Employee not found:

```text
GET /employees/999
→ 404 NOT FOUND
```

Duplicate email:

```text
POST /employees
→ 409 CONFLICT
```

### Interview Answer

> "I use appropriate HTTP status codes based on the operation. For example, I return 201 for successful creation, 200 for successful retrieval or update, 204 for successful deletion, 400 for validation errors, 404 when the resource doesn't exist and 409 for conflicts such as duplicate employee email."

---

# 6. `@PathVariable` vs `@RequestParam` vs `@RequestBody`

### What?

They extract different types of information from HTTP requests.

### Why?

They allow us to map request data to Java method parameters.

### How?

Path variable:

```java
@GetMapping("/{id}")
public Employee getEmployee(@PathVariable Long id)
```

URL:

```text
/employees/101
```

Request parameter:

```java
@GetMapping("/search")
public Employee search(@RequestParam String name)
```

URL:

```text
/employees/search?name=John
```

Request body:

```java
@PostMapping
public Employee create(@RequestBody EmployeeRequest request)
```

### Real Project Example

```text
GET /api/v1/employees/101
```

uses `@PathVariable`.

```text
GET /api/v1/employees/search?name=John
```

uses `@RequestParam`.

```text
POST /api/v1/employees
```

uses `@RequestBody`.

### Interview Answer

> "`@PathVariable` is used for identifying a resource in the URL, `@RequestParam` is generally used for filtering, searching or pagination parameters, and `@RequestBody` is used to receive JSON request data."

---

# 7. Why use `/api/v1/employees`?

### What?

This is **API versioning**.

### Why?

It allows us to introduce breaking changes without immediately affecting existing clients.

### How?

Version 1:

```text
/api/v1/employees
```

Later:

```text
/api/v2/employees
```

### Real Project Example

Suppose V1 returns:

```json
{
  "firstName": "John",
  "lastName": "Smith"
}
```

But V2 changes the response structure.

Existing React clients can continue using V1 while newer clients use V2.

### Interview Answer

> "I use URL-based API versioning such as `/api/v1/employees`. It allows us to introduce backward-incompatible changes in V2 without breaking clients that still depend on V1."

---

# 8. Why use DTO instead of Entity?

### What?

DTO means **Data Transfer Object**.

It is used to transfer data between client and application layers.

### Why?

We don't want to expose our database Entity directly.

Benefits:

* Security
* Loose coupling
* API contract control
* Validation
* Easier evolution

### How?

```text
Request JSON
     ↓
EmployeeRequest DTO
     ↓
Service
     ↓
Employee Entity
```

Response:

```text
Employee Entity
     ↓
EmployeeResponse DTO
     ↓
JSON
```

### Real Project Example

Database Entity might contain:

```text
id
employeeCode
firstName
lastName
email
salary
internalAuditId
createdBy
```

But API doesn't necessarily need to expose every field.

### Interview Answer

> "I don't expose JPA entities directly from REST APIs. I use request and response DTOs to control the API contract, prevent accidental exposure of internal fields, separate database structure from API structure and make the application easier to maintain."

---

# 9. Explain Complete REST API Request Flow

### What?

It is the journey of an HTTP request through the Spring Boot application.

### Why?

Layered architecture separates responsibilities.

### How?

```text
Client
 ↓
Controller
 ↓
DTO + Validation
 ↓
Service
 ↓
Repository
 ↓
JPA
 ↓
Hibernate
 ↓
Database
```

Response:

```text
Database
 ↓
Entity
 ↓
Mapper
 ↓
Response DTO
 ↓
Controller
 ↓
JSON
```

### Real Project Example

```text
GET /api/v1/employees/101
```

Controller:

```java
employeeService.getEmployeeById(101);
```

Service:

```java
employeeRepository.findById(101);
```

### Interview Answer

> "In my project, the request first reaches the Controller. The Controller validates and converts the request into a DTO and delegates to the Service. The Service performs business logic and calls the Repository. Spring Data JPA uses Hibernate to interact with PostgreSQL. The result is mapped from Entity to Response DTO and returned as JSON."

---

# 10. How do you handle exceptions globally?

### What?

We use:

```java
@RestControllerAdvice
```

with:

```java
@ExceptionHandler
```

### Why?

Instead of writing try-catch blocks in every Controller, we centralize exception handling.

### How?

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EmployeeNotFoundException.class)
    public ResponseEntity<?> handleNotFound(...) {
        ...
    }
}
```

### Real Project Example

Service:

```java
throw new EmployeeNotFoundException(id);
```

Global handler converts it to:

```text
404 NOT FOUND
```

### Interview Answer

> "I use `@RestControllerAdvice` for centralized exception handling. I define specific handlers using `@ExceptionHandler` for custom exceptions, validation exceptions and unexpected exceptions. This keeps Controllers clean and provides a consistent error response."

---

# 11. How do you validate REST API requests?

### What?

Spring Boot supports Bean Validation.

Examples:

```java
@NotBlank
@NotNull
@Email
@Positive
@Size
@PastOrPresent
```

### Why?

To prevent invalid data from entering our business logic or database.

### How?

DTO:

```java
@NotBlank
private String firstName;

@Email
private String email;
```

Controller:

```java
public ResponseEntity<?> create(
        @Valid @RequestBody EmployeeRequest request)
```

### Real Project Example

If:

```json
{
  "email": "abc"
}
```

is sent, validation fails before service processing.

### Interview Answer

> "I perform request validation at the DTO level using Bean Validation annotations and trigger validation using `@Valid` in the Controller. Validation failures are handled centrally using `@RestControllerAdvice` and returned with HTTP 400."

---

# 12. How do you implement pagination and sorting?

### What?

Pagination retrieves data in smaller chunks instead of loading everything.

### Why?

Suppose the database has:

```text
10 million employees
```

Returning all 10 million records is inefficient.

### How?

Spring Data:

```java
Pageable pageable =
    PageRequest.of(
        page,
        size,
        Sort.by("salary").descending()
    );
```

Repository:

```java
Page<Employee> findAll(Pageable pageable);
```

### Real Project Example

```text
GET /api/v1/employees?page=0&size=10&sortBy=salary&direction=desc
```

### Interview Answer

> "I use Spring Data's `Pageable` and `Page` for pagination and sorting. This prevents loading large datasets into memory and improves API performance. For example, I can retrieve 10 employees per page sorted by salary."

---

# 13. How do you implement Search?

### What?

Search allows clients to retrieve resources based on criteria.

### Why?

Clients don't always need all records.

### How?

Repository:

```java
Page<Employee>
findByFirstNameContainingIgnoreCase(
    String firstName,
    Pageable pageable
);
```

Controller:

```java
@GetMapping("/search")
```

### Real Project Example

```text
GET /api/v1/employees/search?name=John
```

### Interview Answer

> "I implement search using request parameters and Spring Data JPA derived queries or custom JPQL queries when required. I also combine search with pagination to avoid returning a large result set."

---

# 14. What is Idempotency?

### What?

An operation is idempotent if making the same request multiple times produces the same intended final state.

### Why?

It is important when clients retry requests because of network failures.

### How?

Generally:

```text
GET     → Idempotent
PUT     → Idempotent
DELETE  → Idempotent
POST    → Not necessarily idempotent
PATCH   → Depends on implementation
```

### Real Project Example

```http
PUT /employees/101
```

with:

```json
{
  "salary": 80000
}
```

Sending it multiple times should leave the employee with salary 80000.

### Interview Answer

> "Idempotency means repeated execution of the same request produces the same intended final state. GET, PUT and DELETE are generally considered idempotent, whereas POST is generally not. This is particularly important for retry mechanisms and distributed systems."

---

# 15. How do you handle duplicate records?

### What?

We need to prevent duplicate business data.

### Why?

For example, two employees shouldn't have the same unique email.

### How?

Application-level check:

```java
employeeRepository.existsByEmail(email)
```

and database-level constraint:

```sql
UNIQUE(email)
```

### Real Project Example

```text
POST /employees
email = john@test.com
```

If it already exists:

```text
409 CONFLICT
```

### Interview Answer

> "I prefer defense in depth. I can check for duplicates at the service level to provide a meaningful error message, but I also enforce a unique database constraint because application-level checks alone can have race conditions under concurrent requests."

That's a **very good 3–4 year interview answer**.

---

# 16. How do you secure REST APIs?

### What?

We use authentication and authorization mechanisms such as:

```text
Spring Security
JWT
OAuth2
```

### Why?

To prevent unauthorized users from accessing APIs.

### How?

Typical flow:

```text
Login
 ↓
Validate credentials
 ↓
Generate JWT
 ↓
Client stores token
 ↓
Client sends:
Authorization: Bearer <token>
 ↓
Spring Security validates token
 ↓
Controller
```

### Real Project Example

```text
GET /api/v1/employees
Authorization: Bearer eyJ...
```

### Interview Answer

> "In a production REST API, I use Spring Security with JWT-based authentication. The client first authenticates and receives a token. For subsequent requests it sends the token in the Authorization header. Spring Security validates the token and checks the user's roles or authorities before allowing access."

---

# 17. Authentication vs Authorization

### What?

**Authentication** = Who are you?

**Authorization** = What are you allowed to do?

### Why?

Security requires both identity verification and permission checking.

### How?

Example:

```text
Authentication:
username/password → JWT

Authorization:
ROLE_ADMIN → DELETE employee
ROLE_USER → GET employee
```

### Real Project Example

```text
GET /employees
→ USER allowed

DELETE /employees/101
→ ADMIN only
```

### Interview Answer

> "Authentication verifies the identity of the user, while authorization determines what that authenticated user is allowed to access. For example, an authenticated employee may be allowed to view employee information, while only an admin may delete an employee."

---

# 18. How do you improve REST API performance?

### What?

API performance means reducing response time and resource consumption.

### Why?

Slow APIs impact user experience and system scalability.

### How?

I would check:

```text
Database indexes
Pagination
Query optimization
N+1 queries
Caching
Connection pool
Lazy/Eager loading
Payload size
Logging/monitoring
```

### Real Project Example

Suppose:

```text
GET /employees
```

takes 5 seconds.

I would check:

```text
API logs
 ↓
SQL logs
 ↓
Database query
 ↓
Execution plan
```

Then optimize the bottleneck.

### Interview Answer

> "For API performance, I first identify the bottleneck rather than blindly optimizing. I check application metrics, database queries and logs. Then I can use pagination, proper indexes, query optimization, avoid N+1 queries, appropriate fetching strategies, connection-pool tuning and caching where appropriate."

---

# 19. How do you test REST APIs?

### What?

We use tools such as:

```text
JUnit 5
Mockito
MockMvc
Postman
```

### Why?

To verify functionality and prevent regressions.

### How?

Service test:

```java
@Mock
EmployeeRepository repository;
```

Controller test:

```java
@WebMvcTest(EmployeeController.class)
```

and:

```java
MockMvc
```

### Real Project Example

Test:

```text
GET /api/v1/employees/101
```

Verify:

```text
200 OK
employee ID = 101
```

Test not found:

```text
GET /api/v1/employees/999
```

Verify:

```text
404 NOT FOUND
```

### Interview Answer

> "I use JUnit 5 and Mockito for unit testing service-layer business logic and MockMvc with `@WebMvcTest` for Controller-layer testing. I also use Postman for manual API verification. I cover positive, negative, validation and exception scenarios."

---

# 20. How would you design REST API for millions of employees?

### What?

We need to design for scalability and high traffic.

### Why?

A simple CRUD implementation may not work efficiently at very large scale.

### How?

I would consider:

```text
Pagination
Database indexing
Query optimization
Caching
Connection pooling
Load balancing
Stateless services
Horizontal scaling
Read replicas
Asynchronous processing where appropriate
Monitoring
Rate limiting
```

### Real Project Example

Instead of:

```text
GET /employees
```

returning millions of records:

```text
GET /employees?page=0&size=20
```

Database indexes:

```text
employee_code
email
department
```

### Interview Answer

> "For millions of employees, I would avoid loading the entire dataset. I would use pagination, proper indexing and optimized queries. At the infrastructure level, I would keep the API stateless so it can scale horizontally behind a load balancer. Depending on traffic, I would also consider caching, database read replicas, connection-pool tuning, rate limiting and monitoring."

---

# ⭐ Bonus: 5 Scenario Questions

These are **very important for 3–4 years experience**.

## 21. What if the database is down?

### Interview Answer

> "I would handle database failures through proper exception handling, connection timeouts and monitoring. The API should not expose internal database details to the client. Depending on the operation, we can return an appropriate 5xx response and log the technical exception internally. For production systems, health checks and alerts should detect the database outage."

---

## 22. Two users update the same employee. What happens?

### Interview Answer

> "This is a concurrency problem. I would consider optimistic locking using JPA's `@Version` for normal business applications. Hibernate can detect that the record was modified by another transaction and prevent an outdated update from silently overwriting newer data."

Example:

```java
@Version
private Long version;
```

---

## 23. What if your API takes 5 seconds?

### Interview Answer

> "First, I would identify where the latency is coming from instead of assuming the Controller is the problem. I would check API metrics, application logs, database query execution time, external service calls and thread or connection-pool utilization. If the database query is slow, I would optimize the query and indexes. If the issue is an external service, I would consider timeout, retry and circuit-breaker strategies where appropriate."

---

## 24. Why use Service and ServiceImpl separately?

### Interview Answer

> "I separate the Service interface from its implementation to keep the business contract separate from implementation details. It supports loose coupling and makes it easier to provide another implementation if required. It also aligns with dependency inversion and improves testability."

Architecture:

```text
Controller
    ↓
EmployeeService
    ↓
EmployeeServiceImpl
    ↓
EmployeeRepository
```

---

## 25. Why constructor injection?

### Interview Answer

> "I prefer constructor injection because dependencies are explicit, required dependencies can be made immutable using final fields, and the class becomes easier to unit test. It also avoids hidden dependencies associated with field injection."

Example:

```java
private final EmployeeService employeeService;

public EmployeeController(
        EmployeeService employeeService) {

    this.employeeService = employeeService;
}
```

---

# 🎯 Your 3–4 Year Interview Priority

If you have limited preparation time, learn these **first**:

| Priority | Question                        |
| -------- | ------------------------------- |
| 🔥🔥🔥   | DTO vs Entity                   |
| 🔥🔥🔥   | PUT vs PATCH                    |
| 🔥🔥🔥   | HTTP status codes               |
| 🔥🔥🔥   | Global exception handling       |
| 🔥🔥🔥   | Request flow                    |
| 🔥🔥🔥   | Validation                      |
| 🔥🔥🔥   | Pagination                      |
| 🔥🔥🔥   | Constructor injection           |
| 🔥🔥🔥   | Authentication vs Authorization |
| 🔥🔥🔥   | JWT                             |
| 🔥🔥     | Idempotency                     |
| 🔥🔥     | API versioning                  |
| 🔥🔥     | Performance optimization        |
| 🔥🔥     | JPA/Hibernate flow              |
| 🔥🔥     | Concurrent updates              |
| 🔥       | API testing                     |

### One answer pattern to remember

For almost every technical question, structure your answer like this:

> **What:** Define the concept in one or two lines.
> **Why:** Explain why you use it in a real application.
> **How:** Explain the implementation/flow.
> **Real Project:** Give your Employee Management example.
> **Interview Answer:** Give a concise 30–60 second answer.

This structure will make your answers sound much more like a **3–4 year experienced developer** rather than someone giving textbook definitions.

