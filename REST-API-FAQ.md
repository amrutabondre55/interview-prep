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

Absolutely. Below is an **interview-focused REST API preparation set** for your selected topics. I’ve kept the answers at a **3–4 years Java/Spring Boot experience level** and used exactly your structure:

**What → Why → How → Real Project Example → Interview Answer**

---

# 1. Idempotent Methods

### Q1. What is idempotency in REST API?

### What?

Idempotency means **making the same API request multiple times produces the same final result/state as making it once**.

Commonly:

| HTTP Method | Idempotent?                  |
| ----------- | ---------------------------- |
| GET         | ✅ Yes                        |
| PUT         | ✅ Yes                        |
| DELETE      | ✅ Yes                        |
| POST        | ❌ Generally No               |
| PATCH       | ⚠️ Depends on implementation |

### Why?

It is important when a client retries a request because of a network issue.

For example, if a request times out, the client may send it again.

### How?

For example:

```http
PUT /api/v1/employees/101
```

```json
{
  "salary": 80000
}
```

Sending this request once or five times should result in:

```text
Employee 101 salary = 80000
```

### Real Project Example

In your Employee Management API:

```http
PUT /api/v1/employees/101
```

updates employee 101.

If the same PUT request is sent multiple times with the same data, the final state remains the same.

### Interview Answer

> "Idempotency means that executing the same request multiple times produces the same intended final state. GET, PUT and DELETE are generally idempotent, while POST is generally not. This is important in distributed systems because clients may retry requests due to network failures."

### 🔥 Follow-up

**Q: Is DELETE always idempotent?**

> "DELETE is considered idempotent because after the resource is deleted, repeating the same delete request doesn't change the final state. However, the HTTP response may differ—for example, the first request could return 204 and a subsequent request could return 404."

---

# 2. Path Variable

### Q2. What is `@PathVariable` in Spring Boot?

### What?

`@PathVariable` is used to extract a value directly from the URL path.

### Why?

We use it when the value identifies a **specific resource**.

### How?

```java
@GetMapping("/employees/{id}")
public ResponseEntity<EmployeeResponse> getEmployee(
        @PathVariable Long id) {

    return ResponseEntity.ok(
        employeeService.getEmployeeById(id)
    );
}
```

URL:

```text
GET /api/v1/employees/101
```

Here:

```text
101 → id
```

### Real Project Example

Suppose we want employee ID 101:

```text
GET /api/v1/employees/101
```

Controller:

```java
@GetMapping("/{id}")
public ResponseEntity<EmployeeResponse> getEmployee(
        @PathVariable Long id) {

    return ResponseEntity.ok(
        employeeService.getEmployeeById(id)
    );
}
```

### Interview Answer

> "`@PathVariable` is used to extract a value from the URL path. I use it when I want to identify a specific resource. For example, `GET /api/v1/employees/101` uses `@PathVariable` to retrieve employee 101."

### 🔥 Follow-up

**Q: Why not use RequestParam for employee ID?**

> "Both are technically possible, but a path variable is more RESTful when the value identifies a specific resource. `/employees/101` clearly represents employee 101, whereas `/employees?id=101` is more suitable when the ID is being treated as a query parameter."

---

# 3. RequestParam

### Q3. What is `@RequestParam`?

### What?

`@RequestParam` extracts parameters from the URL query string.

### Why?

It is commonly used for:

* Search
* Filtering
* Pagination
* Sorting
* Optional parameters

### How?

```java
@GetMapping("/search")
public ResponseEntity<List<EmployeeResponse>> searchEmployees(
        @RequestParam String name) {

    return ResponseEntity.ok(
        employeeService.searchEmployees(name)
    );
}
```

Request:

```text
GET /api/v1/employees/search?name=John
```

### Real Project Example

Search employees by department:

```text
GET /api/v1/employees?department=IT
```

Controller:

```java
@GetMapping
public ResponseEntity<List<EmployeeResponse>> getEmployees(
        @RequestParam(required = false) String department) {

    return ResponseEntity.ok(
        employeeService.getEmployees(department)
    );
}
```

### Interview Answer

> "`@RequestParam` is used to read query parameters from the URL. I generally use it for filtering, searching, pagination and sorting. For example, `GET /api/v1/employees?department=IT` uses `@RequestParam` to filter employees by department."

### 🔥 Follow-up

**Q: What does `required=false` mean?**

```java
@RequestParam(required = false) String department
```

> "It means the parameter is optional. If the client doesn't send `department`, Spring won't throw a missing parameter exception, and the value will be null."

---

# 4. RequestBody

### Q4. What is `@RequestBody`?

### What?

`@RequestBody` is used to read JSON or other request payload data and convert it into a Java object.

### Why?

We use it mainly for APIs where the client sends data to create or update resources.

### How?

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @RequestBody EmployeeRequest request) {

    EmployeeResponse response =
            employeeService.createEmployee(request);

    return ResponseEntity.status(HttpStatus.CREATED)
            .body(response);
}
```

Request:

```http
POST /api/v1/employees
```

```json
{
  "employeeCode": "EMP101",
  "firstName": "John",
  "lastName": "Smith",
  "email": "john@test.com",
  "department": "IT",
  "salary": 80000
}
```

### Real Project Example

React/Postman sends JSON to Spring Boot.

```text
React
 ↓
JSON Request
 ↓
@RequestBody
 ↓
EmployeeRequest DTO
 ↓
Service
 ↓
Database
```

### Interview Answer

> "`@RequestBody` is used to bind the HTTP request body, usually JSON, to a Java object. In my Employee Management API, I use it with request DTOs for POST and PUT APIs. I also combine it with `@Valid` to validate the incoming request."

### 🔥 Follow-up

**Q: Why use DTO with `@RequestBody` instead of Entity?**

> "I prefer DTOs because they prevent exposing the database entity directly, allow us to control the API contract, provide request-specific validation and reduce coupling between the API and database model."

---

# 5. PathVariable vs RequestParam vs RequestBody

### Q5. Explain the difference between these three.

### What?

They receive different types of request data.

### Why?

Choosing the correct one makes the API design clear and RESTful.

### How?

| Annotation      | Example          | Purpose                  |
| --------------- | ---------------- | ------------------------ |
| `@PathVariable` | `/employees/101` | Identify resource        |
| `@RequestParam` | `?department=IT` | Filter/search/pagination |
| `@RequestBody`  | JSON payload     | Create/update data       |

### Real Project Example

Get employee:

```text
GET /api/v1/employees/101
```

```java
@PathVariable Long id
```

Filter:

```text
GET /api/v1/employees?department=IT
```

```java
@RequestParam String department
```

Create:

```text
POST /api/v1/employees
```

```java
@RequestBody EmployeeRequest request
```

### Interview Answer

> "`@PathVariable` is used when the value is part of the resource URL, `@RequestParam` is used for query parameters such as filtering, searching and pagination, and `@RequestBody` is used to receive structured request data such as JSON for create or update operations."

---

# 6. Exception Handling

### Q6. How do you handle exceptions in Spring Boot REST APIs?

### What?

Exception handling means managing application errors and returning meaningful HTTP responses to clients.

### Why?

We don't want to expose stack traces or internal implementation details to clients.

It also keeps our Controllers clean.

### How?

I use:

```java
@RestControllerAdvice
```

and:

```java
@ExceptionHandler
```

Example:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EmployeeNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleEmployeeNotFound(
            EmployeeNotFoundException ex) {

        ErrorResponse error = new ErrorResponse(
                false,
                ex.getMessage()
        );

        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(error);
    }
}
```

Custom exception:

```java
public class EmployeeNotFoundException
        extends RuntimeException {

    public EmployeeNotFoundException(Long id) {
        super("Employee not found with id: " + id);
    }
}
```

### Real Project Example

Request:

```text
GET /api/v1/employees/999
```

If employee 999 doesn't exist:

```text
Service
 ↓
EmployeeNotFoundException
 ↓
GlobalExceptionHandler
 ↓
404 NOT FOUND
```

Response:

```json
{
  "success": false,
  "message": "Employee not found with id: 999"
}
```

### Interview Answer

> "In my Spring Boot application, I use centralized exception handling with `@RestControllerAdvice` and `@ExceptionHandler`. I create custom exceptions for business scenarios such as employee not found or duplicate employee email. The global handler converts these exceptions into consistent error responses with appropriate HTTP status codes."

### 🔥 Follow-up

**Q: Why not use try-catch in every Controller?**

> "That would duplicate code across Controllers and make them difficult to maintain. Centralized exception handling keeps business code clean and provides a consistent error response structure."

---

# 7. Exception Handling Scenario

### Q7. What happens if Employee ID doesn't exist?

### What?

We should return a meaningful `404 NOT FOUND`.

### Why?

The client requested a resource that doesn't exist.

### How?

Repository:

```java
Optional<Employee> employee =
        employeeRepository.findById(id);
```

Service:

```java
return employeeRepository.findById(id)
        .orElseThrow(() ->
            new EmployeeNotFoundException(id));
```

Global handler:

```java
@ExceptionHandler(EmployeeNotFoundException.class)
public ResponseEntity<ErrorResponse> handleNotFound(
        EmployeeNotFoundException ex) {

    return ResponseEntity
            .status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse(
                    false,
                    ex.getMessage()
            ));
}
```

### Real Project Example

```text
GET /api/v1/employees/999
```

Response:

```text
404 NOT FOUND
```

### Interview Answer

> "If the employee doesn't exist, I don't return null from the service. I throw a custom `EmployeeNotFoundException`, which is handled centrally by `@RestControllerAdvice` and converted into a 404 response."

---

# 8. Validation

### Q8. How do you validate REST API requests?

### What?

Validation ensures incoming data follows the required business and data rules.

### Why?

It prevents invalid data from reaching the Service and Database layers.

### How?

DTO:

```java
public class EmployeeRequest {

    @NotBlank
    private String firstName;

    @NotBlank
    private String lastName;

    @Email
    @NotBlank
    private String email;

    @Positive
    private BigDecimal salary;
}
```

Controller:

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @Valid @RequestBody EmployeeRequest request) {

    ...
}
```

### Real Project Example

Client sends:

```json
{
  "firstName": "",
  "email": "wrong-email",
  "salary": -100
}
```

Validation fails.

The request doesn't proceed to business logic.

### Interview Answer

> "I use Jakarta Bean Validation annotations such as `@NotBlank`, `@Email`, `@Positive` and `@Size` on request DTOs. I trigger validation using `@Valid` in the Controller and handle validation exceptions centrally using `@RestControllerAdvice`."

---

# 9. What is `@Valid`?

### What?

`@Valid` tells Spring to validate the object against its validation annotations.

### Why?

Without triggering validation, annotations such as `@NotBlank` won't automatically reject the request.

### How?

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @Valid @RequestBody EmployeeRequest request) {
    
    ...
}
```

DTO:

```java
@NotBlank
private String firstName;
```

### Real Project Example

Request:

```json
{
  "firstName": ""
}
```

Spring detects the validation failure.

### Interview Answer

> "`@Valid` triggers Bean Validation on the request object. I use it with `@RequestBody` DTOs so that invalid data is rejected before it reaches the service layer."

---

# 10. How do you return validation errors?

### What?

We should return a structured and client-friendly error response.

### Why?

The frontend should know which fields are invalid.

### How?

Example:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "email": "Invalid email",
    "firstName": "First name is required"
  }
}
```

Handle:

```java
@ExceptionHandler(MethodArgumentNotValidException.class)
```

### Real Project Example

React submits:

```json
{
  "firstName": "",
  "email": "abc"
}
```

Backend returns:

```text
400 BAD REQUEST
```

with field-level errors.

### Interview Answer

> "I handle `MethodArgumentNotValidException` globally and extract field-level validation errors. I return a structured 400 Bad Request response so that the frontend can clearly identify which fields need correction."

---

# 11. Pagination

### Q11. What is pagination in REST API?

### What?

Pagination means returning data in smaller pages instead of returning the complete dataset.

### Why?

Suppose we have:

```text
1 million employees
```

Returning all employees at once can cause:

* High memory usage
* Slow response
* Large network payload
* Database performance issues

### How?

Request:

```text
GET /api/v1/employees?page=0&size=10
```

Controller:

```java
@GetMapping
public ResponseEntity<Page<EmployeeResponse>> getEmployees(
        @PageableDefault(size = 10)
        Pageable pageable) {

    return ResponseEntity.ok(
        employeeService.getEmployees(pageable)
    );
}
```

Repository:

```java
Page<Employee> findAll(Pageable pageable);
```

### Real Project Example

```text
GET /api/v1/employees?page=0&size=10
```

means:

```text
Page = 0
Size = 10
```

The database returns only the required records.

### Interview Answer

> "I use Spring Data JPA's `Pageable` and `Page` to implement pagination. Instead of loading all employees, I retrieve a fixed number of records per page. This reduces memory usage, database load and response size."

---

# 12. Pagination + Sorting

### Q12. How do you implement sorting with pagination?

### What?

We can combine `Pageable` with `Sort`.

### Why?

The client may want results in a particular order.

### How?

Request:

```text
GET /api/v1/employees?page=0&size=10&sort=salary,desc
```

Spring:

```java
Pageable pageable =
        PageRequest.of(
                0,
                10,
                Sort.by("salary").descending()
        );
```

### Real Project Example

Client asks:

> Give me the first 10 employees with the highest salary.

Request:

```text
GET /api/v1/employees?page=0&size=10&sort=salary,desc
```

### Interview Answer

> "Spring Data allows me to combine pagination and sorting using `Pageable`. For example, I can expose `page`, `size` and `sort` parameters so clients can retrieve paginated employees ordered by salary, joining date or another allowed field."

---

# 13. What happens if client requests page size 10,000?

### What?

The client is requesting a very large page.

### Why?

Without limits, a client could cause performance problems.

### How?

I can enforce a maximum page size.

For example:

```text
Maximum = 100
```

If client sends:

```text
size=10000
```

we cap it to 100 or reject the request.

### Real Project Example

```text
GET /api/v1/employees?page=0&size=10000
```

Instead of allowing 10,000 records:

```text
Maximum allowed = 100
```

### Interview Answer

> "I would not allow unlimited page sizes. I would configure a maximum page size, for example 100, to protect the API and database from large queries. I would also validate page numbers and sorting fields."

---

# 14. Swagger / OpenAPI

### Q14. What is Swagger/OpenAPI?

### What?

**OpenAPI** is a specification for describing REST APIs.

**Swagger UI** provides an interactive web interface for viewing and testing the API documentation.

### Why?

It helps:

* Developers understand APIs
* Frontend/backend teams collaborate
* Test endpoints
* Document request/response models
* Understand parameters and status codes

### How?

In Spring Boot, we commonly use **springdoc-openapi**.

Dependency:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.9</version>
</dependency>
```

Then Spring Boot can generate OpenAPI documentation from the application's API definitions.

### Real Project Example

Your Employee API:

```text
GET    /api/v1/employees
GET    /api/v1/employees/{id}
POST   /api/v1/employees
PUT    /api/v1/employees/{id}
DELETE /api/v1/employees/{id}
```

Swagger UI allows developers to see and test these endpoints.

### Interview Answer

> "I use OpenAPI with Swagger UI to document REST APIs. It provides an interactive interface where developers can understand endpoints, request parameters, request bodies, response models and status codes, and can also test APIs during development."

---

# 15. Swagger vs Postman

### Q15. What is the difference between Swagger and Postman?

### What?

Both can be used to interact with APIs, but their primary purposes are different.

### Why?

Swagger is more focused on **API documentation and API contract**, while Postman is more focused on **API testing and collections/workflows**.

### How?

Swagger:

```text
API Documentation
       ↓
Swagger UI
       ↓
Try API
```

Postman:

```text
API Endpoint
       ↓
Request
       ↓
Headers / Body / Auth
       ↓
Response
       ↓
Tests
```

### Real Project Example

For your Employee API:

Swagger can document:

```text
POST /api/v1/employees
```

and show the request/response schema.

Postman can be used to test:

```text
POST
GET
PUT
DELETE
```

and create a collection containing multiple scenarios.

### Interview Answer

> "Swagger/OpenAPI is primarily used for API documentation and defining the API contract, while Postman is primarily used for API testing and creating reusable request collections. In a project, I can use Swagger for documentation and quick endpoint verification and Postman for detailed functional and negative testing."

---

# 🔥 16. Very Important Combined Interview Question

### Q16. Explain your Employee REST API Controller.

Suppose interviewer asks:

> **"Show me how you would design your Employee Controller."**

### What?

The Controller handles HTTP requests and maps URLs to appropriate operations.

### Why?

It should focus on the **HTTP layer** and delegate business logic to the Service.

### How?

Example:

```java
@RestController
@RequestMapping("/api/v1/employees")
public class EmployeeController {

    private final EmployeeService employeeService;

    public EmployeeController(EmployeeService employeeService) {
        this.employeeService = employeeService;
    }

    @GetMapping("/{id}")
    public ResponseEntity<EmployeeResponse> getEmployee(
            @PathVariable Long id) {

        return ResponseEntity.ok(
                employeeService.getEmployeeById(id)
        );
    }

    @GetMapping
    public ResponseEntity<Page<EmployeeResponse>> getEmployees(
            @RequestParam(required = false) String department,
            Pageable pageable) {

        return ResponseEntity.ok(
                employeeService.getEmployees(
                        department, pageable
                )
        );
    }

    @PostMapping
    public ResponseEntity<EmployeeResponse> createEmployee(
            @Valid @RequestBody EmployeeRequest request) {

        EmployeeResponse response =
                employeeService.createEmployee(request);

        return ResponseEntity
                .status(HttpStatus.CREATED)
                .body(response);
    }

    @PutMapping("/{id}")
    public ResponseEntity<EmployeeResponse> updateEmployee(
            @PathVariable Long id,
            @Valid @RequestBody EmployeeRequest request) {

        return ResponseEntity.ok(
                employeeService.updateEmployee(id, request)
        );
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteEmployee(
            @PathVariable Long id) {

        employeeService.deleteEmployee(id);

        return ResponseEntity.noContent().build();
    }
}
```

### Real Project Flow

```text
React / Postman
       ↓
GET /api/v1/employees/101
       ↓
EmployeeController
       ↓
@PathVariable → 101
       ↓
EmployeeService
       ↓
EmployeeRepository
       ↓
PostgreSQL
       ↓
Employee Entity
       ↓
EmployeeResponse DTO
       ↓
200 OK
```

### Interview Answer

> "In my Employee Management project, I use a versioned base URL such as `/api/v1/employees`. The Controller is responsible only for handling HTTP requests, request parameters, path variables, request-body validation and HTTP responses. I use `@PathVariable` for resource IDs, `@RequestParam` for filtering and pagination, and `@RequestBody` with `@Valid` for create and update requests. The Controller delegates business logic to the Service layer and returns appropriate HTTP status codes. I don't put business logic or database operations directly in the Controller."

---

# ⭐ Most Frequently Asked Follow-ups

For your **3–4 year interview**, prepare these especially well:

### Idempotency

> **"Why is PUT idempotent but POST generally isn't?"**

### PathVariable

> **"When would you use PathVariable instead of RequestParam?"**

### RequestParam

> **"How do you make RequestParam optional?"**

### RequestBody

> **"Can GET have RequestBody?"**

A safe interview answer:

> "Although HTTP doesn't universally prohibit a GET body, it is generally not recommended because clients, proxies and servers may not handle it consistently. For GET, I prefer path variables or query parameters."

### Exception Handling

> **"Why use `@RestControllerAdvice`?"**

### Validation

> **"What is the difference between `@Valid` and `@Validated`?"**

### Pagination

> **"How would you handle 10 million records?"**

### Swagger

> **"Swagger vs Postman?"**

---

# 🎯 Quick Revision Sheet

Before your interview, remember this:

```text
@PathVariable
→ Resource identification
→ /employees/101

@RequestParam
→ Filtering / Search / Pagination
→ /employees?department=IT

@RequestBody
→ JSON request data
→ POST /employees

@Valid
→ Request validation

@RestControllerAdvice
→ Global exception handling

Pageable
→ Pagination + Sorting

OpenAPI / Swagger
→ API documentation + interactive testing

GET
→ Retrieve
→ Idempotent

POST
→ Create
→ Generally NOT idempotent

PUT
→ Full update/replacement
→ Idempotent

PATCH
→ Partial update
→ Depends on implementation

DELETE
→ Delete
→ Idempotent
```

### ⭐ One strong answer for your interview

If the interviewer asks **"What REST API best practices do you follow?"**, you can combine almost everything:

> **"In my Spring Boot REST APIs, I follow resource-based and versioned URLs such as `/api/v1/employees`. I use the appropriate HTTP methods and status codes, DTOs instead of exposing entities, constructor injection, Bean Validation with `@Valid`, centralized exception handling using `@RestControllerAdvice`, and pagination and sorting for large datasets. I use `@PathVariable` for resource identification, `@RequestParam` for filtering and pagination, and `@RequestBody` for request payloads. I also document APIs using OpenAPI/Swagger, secure APIs using Spring Security where required, and write unit and integration tests for positive and negative scenarios."**
Absolutely. Below is an **interview-focused REST API preparation set** for your selected topics. I’ve kept the answers at a **3–4 years Java/Spring Boot experience level** and used exactly your structure:

**What → Why → How → Real Project Example → Interview Answer**

---

# 1. Idempotent Methods

### Q1. What is idempotency in REST API?

### What?

Idempotency means **making the same API request multiple times produces the same final result/state as making it once**.

Commonly:

| HTTP Method | Idempotent?                  |
| ----------- | ---------------------------- |
| GET         | ✅ Yes                        |
| PUT         | ✅ Yes                        |
| DELETE      | ✅ Yes                        |
| POST        | ❌ Generally No               |
| PATCH       | ⚠️ Depends on implementation |

### Why?

It is important when a client retries a request because of a network issue.

For example, if a request times out, the client may send it again.

### How?

For example:

```http
PUT /api/v1/employees/101
```

```json
{
  "salary": 80000
}
```

Sending this request once or five times should result in:

```text
Employee 101 salary = 80000
```

### Real Project Example

In your Employee Management API:

```http
PUT /api/v1/employees/101
```

updates employee 101.

If the same PUT request is sent multiple times with the same data, the final state remains the same.

### Interview Answer

> "Idempotency means that executing the same request multiple times produces the same intended final state. GET, PUT and DELETE are generally idempotent, while POST is generally not. This is important in distributed systems because clients may retry requests due to network failures."

### 🔥 Follow-up

**Q: Is DELETE always idempotent?**

> "DELETE is considered idempotent because after the resource is deleted, repeating the same delete request doesn't change the final state. However, the HTTP response may differ—for example, the first request could return 204 and a subsequent request could return 404."

---

# 2. Path Variable

### Q2. What is `@PathVariable` in Spring Boot?

### What?

`@PathVariable` is used to extract a value directly from the URL path.

### Why?

We use it when the value identifies a **specific resource**.

### How?

```java
@GetMapping("/employees/{id}")
public ResponseEntity<EmployeeResponse> getEmployee(
        @PathVariable Long id) {

    return ResponseEntity.ok(
        employeeService.getEmployeeById(id)
    );
}
```

URL:

```text
GET /api/v1/employees/101
```

Here:

```text
101 → id
```

### Real Project Example

Suppose we want employee ID 101:

```text
GET /api/v1/employees/101
```

Controller:

```java
@GetMapping("/{id}")
public ResponseEntity<EmployeeResponse> getEmployee(
        @PathVariable Long id) {

    return ResponseEntity.ok(
        employeeService.getEmployeeById(id)
    );
}
```

### Interview Answer

> "`@PathVariable` is used to extract a value from the URL path. I use it when I want to identify a specific resource. For example, `GET /api/v1/employees/101` uses `@PathVariable` to retrieve employee 101."

### 🔥 Follow-up

**Q: Why not use RequestParam for employee ID?**

> "Both are technically possible, but a path variable is more RESTful when the value identifies a specific resource. `/employees/101` clearly represents employee 101, whereas `/employees?id=101` is more suitable when the ID is being treated as a query parameter."

---

# 3. RequestParam

### Q3. What is `@RequestParam`?

### What?

`@RequestParam` extracts parameters from the URL query string.

### Why?

It is commonly used for:

* Search
* Filtering
* Pagination
* Sorting
* Optional parameters

### How?

```java
@GetMapping("/search")
public ResponseEntity<List<EmployeeResponse>> searchEmployees(
        @RequestParam String name) {

    return ResponseEntity.ok(
        employeeService.searchEmployees(name)
    );
}
```

Request:

```text
GET /api/v1/employees/search?name=John
```

### Real Project Example

Search employees by department:

```text
GET /api/v1/employees?department=IT
```

Controller:

```java
@GetMapping
public ResponseEntity<List<EmployeeResponse>> getEmployees(
        @RequestParam(required = false) String department) {

    return ResponseEntity.ok(
        employeeService.getEmployees(department)
    );
}
```

### Interview Answer

> "`@RequestParam` is used to read query parameters from the URL. I generally use it for filtering, searching, pagination and sorting. For example, `GET /api/v1/employees?department=IT` uses `@RequestParam` to filter employees by department."

### 🔥 Follow-up

**Q: What does `required=false` mean?**

```java
@RequestParam(required = false) String department
```

> "It means the parameter is optional. If the client doesn't send `department`, Spring won't throw a missing parameter exception, and the value will be null."

---

# 4. RequestBody

### Q4. What is `@RequestBody`?

### What?

`@RequestBody` is used to read JSON or other request payload data and convert it into a Java object.

### Why?

We use it mainly for APIs where the client sends data to create or update resources.

### How?

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @RequestBody EmployeeRequest request) {

    EmployeeResponse response =
            employeeService.createEmployee(request);

    return ResponseEntity.status(HttpStatus.CREATED)
            .body(response);
}
```

Request:

```http
POST /api/v1/employees
```

```json
{
  "employeeCode": "EMP101",
  "firstName": "John",
  "lastName": "Smith",
  "email": "john@test.com",
  "department": "IT",
  "salary": 80000
}
```

### Real Project Example

React/Postman sends JSON to Spring Boot.

```text
React
 ↓
JSON Request
 ↓
@RequestBody
 ↓
EmployeeRequest DTO
 ↓
Service
 ↓
Database
```

### Interview Answer

> "`@RequestBody` is used to bind the HTTP request body, usually JSON, to a Java object. In my Employee Management API, I use it with request DTOs for POST and PUT APIs. I also combine it with `@Valid` to validate the incoming request."

### 🔥 Follow-up

**Q: Why use DTO with `@RequestBody` instead of Entity?**

> "I prefer DTOs because they prevent exposing the database entity directly, allow us to control the API contract, provide request-specific validation and reduce coupling between the API and database model."

---

# 5. PathVariable vs RequestParam vs RequestBody

### Q5. Explain the difference between these three.

### What?

They receive different types of request data.

### Why?

Choosing the correct one makes the API design clear and RESTful.

### How?

| Annotation      | Example          | Purpose                  |
| --------------- | ---------------- | ------------------------ |
| `@PathVariable` | `/employees/101` | Identify resource        |
| `@RequestParam` | `?department=IT` | Filter/search/pagination |
| `@RequestBody`  | JSON payload     | Create/update data       |

### Real Project Example

Get employee:

```text
GET /api/v1/employees/101
```

```java
@PathVariable Long id
```

Filter:

```text
GET /api/v1/employees?department=IT
```

```java
@RequestParam String department
```

Create:

```text
POST /api/v1/employees
```

```java
@RequestBody EmployeeRequest request
```

### Interview Answer

> "`@PathVariable` is used when the value is part of the resource URL, `@RequestParam` is used for query parameters such as filtering, searching and pagination, and `@RequestBody` is used to receive structured request data such as JSON for create or update operations."

---

# 6. Exception Handling

### Q6. How do you handle exceptions in Spring Boot REST APIs?

### What?

Exception handling means managing application errors and returning meaningful HTTP responses to clients.

### Why?

We don't want to expose stack traces or internal implementation details to clients.

It also keeps our Controllers clean.

### How?

I use:

```java
@RestControllerAdvice
```

and:

```java
@ExceptionHandler
```

Example:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EmployeeNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleEmployeeNotFound(
            EmployeeNotFoundException ex) {

        ErrorResponse error = new ErrorResponse(
                false,
                ex.getMessage()
        );

        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(error);
    }
}
```

Custom exception:

```java
public class EmployeeNotFoundException
        extends RuntimeException {

    public EmployeeNotFoundException(Long id) {
        super("Employee not found with id: " + id);
    }
}
```

### Real Project Example

Request:

```text
GET /api/v1/employees/999
```

If employee 999 doesn't exist:

```text
Service
 ↓
EmployeeNotFoundException
 ↓
GlobalExceptionHandler
 ↓
404 NOT FOUND
```

Response:

```json
{
  "success": false,
  "message": "Employee not found with id: 999"
}
```

### Interview Answer

> "In my Spring Boot application, I use centralized exception handling with `@RestControllerAdvice` and `@ExceptionHandler`. I create custom exceptions for business scenarios such as employee not found or duplicate employee email. The global handler converts these exceptions into consistent error responses with appropriate HTTP status codes."

### 🔥 Follow-up

**Q: Why not use try-catch in every Controller?**

> "That would duplicate code across Controllers and make them difficult to maintain. Centralized exception handling keeps business code clean and provides a consistent error response structure."

---

# 7. Exception Handling Scenario

### Q7. What happens if Employee ID doesn't exist?

### What?

We should return a meaningful `404 NOT FOUND`.

### Why?

The client requested a resource that doesn't exist.

### How?

Repository:

```java
Optional<Employee> employee =
        employeeRepository.findById(id);
```

Service:

```java
return employeeRepository.findById(id)
        .orElseThrow(() ->
            new EmployeeNotFoundException(id));
```

Global handler:

```java
@ExceptionHandler(EmployeeNotFoundException.class)
public ResponseEntity<ErrorResponse> handleNotFound(
        EmployeeNotFoundException ex) {

    return ResponseEntity
            .status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse(
                    false,
                    ex.getMessage()
            ));
}
```

### Real Project Example

```text
GET /api/v1/employees/999
```

Response:

```text
404 NOT FOUND
```

### Interview Answer

> "If the employee doesn't exist, I don't return null from the service. I throw a custom `EmployeeNotFoundException`, which is handled centrally by `@RestControllerAdvice` and converted into a 404 response."

---

# 8. Validation

### Q8. How do you validate REST API requests?

### What?

Validation ensures incoming data follows the required business and data rules.

### Why?

It prevents invalid data from reaching the Service and Database layers.

### How?

DTO:

```java
public class EmployeeRequest {

    @NotBlank
    private String firstName;

    @NotBlank
    private String lastName;

    @Email
    @NotBlank
    private String email;

    @Positive
    private BigDecimal salary;
}
```

Controller:

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @Valid @RequestBody EmployeeRequest request) {

    ...
}
```

### Real Project Example

Client sends:

```json
{
  "firstName": "",
  "email": "wrong-email",
  "salary": -100
}
```

Validation fails.

The request doesn't proceed to business logic.

### Interview Answer

> "I use Jakarta Bean Validation annotations such as `@NotBlank`, `@Email`, `@Positive` and `@Size` on request DTOs. I trigger validation using `@Valid` in the Controller and handle validation exceptions centrally using `@RestControllerAdvice`."

---

# 9. What is `@Valid`?

### What?

`@Valid` tells Spring to validate the object against its validation annotations.

### Why?

Without triggering validation, annotations such as `@NotBlank` won't automatically reject the request.

### How?

```java
@PostMapping
public ResponseEntity<EmployeeResponse> createEmployee(
        @Valid @RequestBody EmployeeRequest request) {
    
    ...
}
```

DTO:

```java
@NotBlank
private String firstName;
```

### Real Project Example

Request:

```json
{
  "firstName": ""
}
```

Spring detects the validation failure.

### Interview Answer

> "`@Valid` triggers Bean Validation on the request object. I use it with `@RequestBody` DTOs so that invalid data is rejected before it reaches the service layer."

---

# 10. How do you return validation errors?

### What?

We should return a structured and client-friendly error response.

### Why?

The frontend should know which fields are invalid.

### How?

Example:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "email": "Invalid email",
    "firstName": "First name is required"
  }
}
```

Handle:

```java
@ExceptionHandler(MethodArgumentNotValidException.class)
```

### Real Project Example

React submits:

```json
{
  "firstName": "",
  "email": "abc"
}
```

Backend returns:

```text
400 BAD REQUEST
```

with field-level errors.

### Interview Answer

> "I handle `MethodArgumentNotValidException` globally and extract field-level validation errors. I return a structured 400 Bad Request response so that the frontend can clearly identify which fields need correction."

---

# 11. Pagination

### Q11. What is pagination in REST API?

### What?

Pagination means returning data in smaller pages instead of returning the complete dataset.

### Why?

Suppose we have:

```text
1 million employees
```

Returning all employees at once can cause:

* High memory usage
* Slow response
* Large network payload
* Database performance issues

### How?

Request:

```text
GET /api/v1/employees?page=0&size=10
```

Controller:

```java
@GetMapping
public ResponseEntity<Page<EmployeeResponse>> getEmployees(
        @PageableDefault(size = 10)
        Pageable pageable) {

    return ResponseEntity.ok(
        employeeService.getEmployees(pageable)
    );
}
```

Repository:

```java
Page<Employee> findAll(Pageable pageable);
```

### Real Project Example

```text
GET /api/v1/employees?page=0&size=10
```

means:

```text
Page = 0
Size = 10
```

The database returns only the required records.

### Interview Answer

> "I use Spring Data JPA's `Pageable` and `Page` to implement pagination. Instead of loading all employees, I retrieve a fixed number of records per page. This reduces memory usage, database load and response size."

---

# 12. Pagination + Sorting

### Q12. How do you implement sorting with pagination?

### What?

We can combine `Pageable` with `Sort`.

### Why?

The client may want results in a particular order.

### How?

Request:

```text
GET /api/v1/employees?page=0&size=10&sort=salary,desc
```

Spring:

```java
Pageable pageable =
        PageRequest.of(
                0,
                10,
                Sort.by("salary").descending()
        );
```

### Real Project Example

Client asks:

> Give me the first 10 employees with the highest salary.

Request:

```text
GET /api/v1/employees?page=0&size=10&sort=salary,desc
```

### Interview Answer

> "Spring Data allows me to combine pagination and sorting using `Pageable`. For example, I can expose `page`, `size` and `sort` parameters so clients can retrieve paginated employees ordered by salary, joining date or another allowed field."

---

# 13. What happens if client requests page size 10,000?

### What?

The client is requesting a very large page.

### Why?

Without limits, a client could cause performance problems.

### How?

I can enforce a maximum page size.

For example:

```text
Maximum = 100
```

If client sends:

```text
size=10000
```

we cap it to 100 or reject the request.

### Real Project Example

```text
GET /api/v1/employees?page=0&size=10000
```

Instead of allowing 10,000 records:

```text
Maximum allowed = 100
```

### Interview Answer

> "I would not allow unlimited page sizes. I would configure a maximum page size, for example 100, to protect the API and database from large queries. I would also validate page numbers and sorting fields."

---

# 14. Swagger / OpenAPI

### Q14. What is Swagger/OpenAPI?

### What?

**OpenAPI** is a specification for describing REST APIs.

**Swagger UI** provides an interactive web interface for viewing and testing the API documentation.

### Why?

It helps:

* Developers understand APIs
* Frontend/backend teams collaborate
* Test endpoints
* Document request/response models
* Understand parameters and status codes

### How?

In Spring Boot, we commonly use **springdoc-openapi**.

Dependency:

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.9</version>
</dependency>
```

Then Spring Boot can generate OpenAPI documentation from the application's API definitions.

### Real Project Example

Your Employee API:

```text
GET    /api/v1/employees
GET    /api/v1/employees/{id}
POST   /api/v1/employees
PUT    /api/v1/employees/{id}
DELETE /api/v1/employees/{id}
```

Swagger UI allows developers to see and test these endpoints.

### Interview Answer

> "I use OpenAPI with Swagger UI to document REST APIs. It provides an interactive interface where developers can understand endpoints, request parameters, request bodies, response models and status codes, and can also test APIs during development."

---

# 15. Swagger vs Postman

### Q15. What is the difference between Swagger and Postman?

### What?

Both can be used to interact with APIs, but their primary purposes are different.

### Why?

Swagger is more focused on **API documentation and API contract**, while Postman is more focused on **API testing and collections/workflows**.

### How?

Swagger:

```text
API Documentation
       ↓
Swagger UI
       ↓
Try API
```

Postman:

```text
API Endpoint
       ↓
Request
       ↓
Headers / Body / Auth
       ↓
Response
       ↓
Tests
```

### Real Project Example

For your Employee API:

Swagger can document:

```text
POST /api/v1/employees
```

and show the request/response schema.

Postman can be used to test:

```text
POST
GET
PUT
DELETE
```

and create a collection containing multiple scenarios.

### Interview Answer

> "Swagger/OpenAPI is primarily used for API documentation and defining the API contract, while Postman is primarily used for API testing and creating reusable request collections. In a project, I can use Swagger for documentation and quick endpoint verification and Postman for detailed functional and negative testing."

---

# 🔥 16. Very Important Combined Interview Question

### Q16. Explain your Employee REST API Controller.

Suppose interviewer asks:

> **"Show me how you would design your Employee Controller."**

### What?

The Controller handles HTTP requests and maps URLs to appropriate operations.

### Why?

It should focus on the **HTTP layer** and delegate business logic to the Service.

### How?

Example:

```java
@RestController
@RequestMapping("/api/v1/employees")
public class EmployeeController {

    private final EmployeeService employeeService;

    public EmployeeController(EmployeeService employeeService) {
        this.employeeService = employeeService;
    }

    @GetMapping("/{id}")
    public ResponseEntity<EmployeeResponse> getEmployee(
            @PathVariable Long id) {

        return ResponseEntity.ok(
                employeeService.getEmployeeById(id)
        );
    }

    @GetMapping
    public ResponseEntity<Page<EmployeeResponse>> getEmployees(
            @RequestParam(required = false) String department,
            Pageable pageable) {

        return ResponseEntity.ok(
                employeeService.getEmployees(
                        department, pageable
                )
        );
    }

    @PostMapping
    public ResponseEntity<EmployeeResponse> createEmployee(
            @Valid @RequestBody EmployeeRequest request) {

        EmployeeResponse response =
                employeeService.createEmployee(request);

        return ResponseEntity
                .status(HttpStatus.CREATED)
                .body(response);
    }

    @PutMapping("/{id}")
    public ResponseEntity<EmployeeResponse> updateEmployee(
            @PathVariable Long id,
            @Valid @RequestBody EmployeeRequest request) {

        return ResponseEntity.ok(
                employeeService.updateEmployee(id, request)
        );
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteEmployee(
            @PathVariable Long id) {

        employeeService.deleteEmployee(id);

        return ResponseEntity.noContent().build();
    }
}
```

### Real Project Flow

```text
React / Postman
       ↓
GET /api/v1/employees/101
       ↓
EmployeeController
       ↓
@PathVariable → 101
       ↓
EmployeeService
       ↓
EmployeeRepository
       ↓
PostgreSQL
       ↓
Employee Entity
       ↓
EmployeeResponse DTO
       ↓
200 OK
```

### Interview Answer

> "In my Employee Management project, I use a versioned base URL such as `/api/v1/employees`. The Controller is responsible only for handling HTTP requests, request parameters, path variables, request-body validation and HTTP responses. I use `@PathVariable` for resource IDs, `@RequestParam` for filtering and pagination, and `@RequestBody` with `@Valid` for create and update requests. The Controller delegates business logic to the Service layer and returns appropriate HTTP status codes. I don't put business logic or database operations directly in the Controller."

---

# ⭐ Most Frequently Asked Follow-ups

For your **3–4 year interview**, prepare these especially well:

### Idempotency

> **"Why is PUT idempotent but POST generally isn't?"**

### PathVariable

> **"When would you use PathVariable instead of RequestParam?"**

### RequestParam

> **"How do you make RequestParam optional?"**

### RequestBody

> **"Can GET have RequestBody?"**

A safe interview answer:

> "Although HTTP doesn't universally prohibit a GET body, it is generally not recommended because clients, proxies and servers may not handle it consistently. For GET, I prefer path variables or query parameters."

### Exception Handling

> **"Why use `@RestControllerAdvice`?"**

### Validation

> **"What is the difference between `@Valid` and `@Validated`?"**

### Pagination

> **"How would you handle 10 million records?"**

### Swagger

> **"Swagger vs Postman?"**

---

# 🎯 Quick Revision Sheet

Before your interview, remember this:

```text
@PathVariable
→ Resource identification
→ /employees/101

@RequestParam
→ Filtering / Search / Pagination
→ /employees?department=IT

@RequestBody
→ JSON request data
→ POST /employees

@Valid
→ Request validation

@RestControllerAdvice
→ Global exception handling

Pageable
→ Pagination + Sorting

OpenAPI / Swagger
→ API documentation + interactive testing

GET
→ Retrieve
→ Idempotent

POST
→ Create
→ Generally NOT idempotent

PUT
→ Full update/replacement
→ Idempotent

PATCH
→ Partial update
→ Depends on implementation

DELETE
→ Delete
→ Idempotent
```

### ⭐ One strong answer for your interview

If the interviewer asks **"What REST API best practices do you follow?"**, you can combine almost everything:

> **"In my Spring Boot REST APIs, I follow resource-based and versioned URLs such as `/api/v1/employees`. I use the appropriate HTTP methods and status codes, DTOs instead of exposing entities, constructor injection, Bean Validation with `@Valid`, centralized exception handling using `@RestControllerAdvice`, and pagination and sorting for large datasets. I use `@PathVariable` for resource identification, `@RequestParam` for filtering and pagination, and `@RequestBody` for request payloads. I also document APIs using OpenAPI/Swagger, secure APIs using Spring Security where required, and write unit and integration tests for positive and negative scenarios."**
