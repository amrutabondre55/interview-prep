Microservices Interview Questions and Answers – 4.5 Years Experience
For a Java Backend Developer with 4.5 years of experience, interviewers generally expect more than definitions. They want to understand:
- Microservices architecture and real-time implementation.
- Spring Boot and Spring Cloud.
- Inter-service communication.
- API Gateway and Service Discovery.
- Resilience, fault tolerance and distributed transactions.
- Docker, AWS and deployment.
- Production-level problem-solving scenarios.
I'll explain in simple English, with practical examples and interview-ready answers that are easy to speak.
1. Microservices Fundamentals
Q1. What are microservices? Why do we use them?
Interview-friendly answer:

Microservices is an architectural style where we divide a large application into multiple small, independent services.

Each service handles a specific business functionality and can be developed, deployed and maintained independently.

For example, in an e-commerce application, we can have:
- User Service – manages user information.
- Product Service – manages product details.
- Order Service – manages orders.
- Payment Service – handles payments.
- Notification Service – sends emails and SMS.
Each service can have its own database and communicates with other services using REST APIs or messaging systems like Kafka or RabbitMQ.

Advantages:
1. Independent deployment.
2. Easy scalability.
3. Better fault isolation.
4. Technology flexibility.
5. Easier maintenance for large applications.
Real-time example: If the Notification Service goes down, users can still place orders. Only notification functionality may be affected.
Q2. What is the difference between Monolithic and Microservices architecture?
Monolithic	Microservices
Single application	Multiple independent services
Usually one deployment unit	Independent deployments
Often shared database	Independent databases are preferred
Scaling the entire application	Scale individual services
Tight coupling can develop	Services are loosely coupled
Failure can impact entire application	Better fault isolation when designed properly

Interview answer:

In a monolithic application, all business functionalities are developed and deployed as a single application.

In microservices architecture, we divide functionalities into independent services. Each service can be deployed and scaled independently.

For large applications, microservices provide better flexibility and scalability, but they also introduce distributed system complexity.
Q3. How do microservices communicate with each other?
There are two major communication approaches:

1. Synchronous communication
- REST API
- HTTP
- OpenFeign
Example: Order Service calls Payment Service and waits for the response.
@FeignClient(name = "payment-service")
public interface PaymentClient {

    @PostMapping("/payments")
    String makePayment(@RequestBody PaymentRequest request);
}


2. Asynchronous communication
- Apache Kafka
- RabbitMQ
Example: After an order is created, Order Service publishes an event. Notification Service consumes that event and sends an email.

Interview answer:

We use synchronous communication when an immediate response is required, and asynchronous communication when services don't need to wait for each other.
Q4. What is API Gateway? Why do we use it?







designgurus.substack.com


Interview-friendly answer:

API Gateway acts as a single entry point for all client requests in a microservices architecture.

Instead of directly calling multiple microservices, the client sends requests to the API Gateway, which routes them to the appropriate service.

Responsibilities:
1. Request routing.
2. Authentication and authorization.
3. Rate limiting.
4. Load balancing integration.
5. Logging and monitoring.
6. SSL termination.
Example:
Client
   |
API Gateway
   |
   |---- User Service
   |---- Product Service
   |---- Order Service
   |---- Payment Service


In Spring Cloud, we can implement an API Gateway using Spring Cloud Gateway.
Q5. What is Service Discovery?
Interview-friendly answer:

Service Discovery is a mechanism that helps microservices find and communicate with each other without hardcoding their IP addresses and ports.

For example, if Order Service wants to communicate with Payment Service, it doesn't need to know the exact IP address of Payment Service.

We can use Netflix Eureka as a service registry.

How it works:
1. Each microservice registers itself with Eureka Server.
2. Eureka maintains the service instances.
3. When Order Service needs Payment Service, it discovers the available instance.
4. The request is routed to the selected instance.







medium.com


Q6. What is Load Balancing in microservices?
Load balancing distributes incoming requests across multiple instances of a service.

Example:

Suppose Payment Service has three instances:
          Order Service
                |
          Load Balancer
          /     |     \
      Instance 1 2   Instance 3


Instead of sending all requests to one instance, requests are distributed across available instances.

In Spring Cloud, we can use Spring Cloud LoadBalancer.

Benefits:
- Better performance.
- High availability.
- Reduced load on individual instances.
2. Important Advanced Microservices Questions
Q7. What happens if one microservice is down?
Very important scenario-based question
Interview-friendly answer:

If one microservice becomes unavailable, other services that depend on it may also get affected.

To prevent cascading failures, we use fault-tolerance mechanisms like:
1. Circuit Breaker: Temporarily stops calling an unhealthy service.
2. Retry: Retries failed requests for temporary failures.
3. Timeout: Prevents waiting indefinitely.
4. Fallback: Provides an alternative response.
5. Bulkhead: Isolates resources between different operations.
For example, if Notification Service is down, Order Service should still successfully create an order. We can publish an event to Kafka and process the notification later.
Q8. What is Circuit Breaker? How do you implement it?
Interview-friendly answer:

Circuit Breaker is a fault-tolerance pattern that prevents repeated calls to a failing microservice.

We commonly use Resilience4j with Spring Boot.

It has three states:







medium.com


- Closed: Requests are allowed.
- Open: Requests are blocked temporarily.
- Half-Open: A limited number of test requests are allowed.
Example:
@CircuitBreaker(
    name = "paymentService",
    fallbackMethod = "paymentFallback"
)
public String makePayment() {
    return restTemplate.getForObject(
        "http://payment-service/pay",
        String.class
    );
}

public String paymentFallback(Exception ex) {
    return "Payment service is temporarily unavailable";
}


Important: In a real payment flow, we should not return a successful payment response just because the fallback was executed. We must maintain the actual payment status.
Q9. What is the difference between Retry and Circuit Breaker?
Retry	Circuit Breaker
Calls the service again	Stops calls temporarily
Handles temporary failures	Prevents cascading failures
Useful for transient errors	Useful when service is unhealthy
Can increase load	Protects the failing service

Interview answer:

Retry attempts to execute a failed operation again, whereas Circuit Breaker stops calling a service when failures cross a configured threshold.

We can combine both using Resilience4j, with appropriate limits and timeouts.
Q10. How do you manage transactions across multiple microservices?
Frequently asked for experienced developers
Interview-friendly answer:

In microservices, each service generally manages its own database transaction.

We cannot directly use a single traditional database transaction across multiple independent services.

To manage distributed transactions, we can use the Saga Pattern.

Saga Pattern breaks a business transaction into multiple local transactions.

Example: Order Placement
1. Order Service
   Create Order

2. Payment Service
   Process Payment

3. Inventory Service
   Reduce Stock

4. Notification Service
   Send Confirmation


Suppose payment succeeds but inventory update fails.

We execute a compensating transaction, such as refunding the payment.

There are two Saga approaches:
- Choreography: Services communicate through events.
- Orchestration: A central orchestrator manages the workflow.
Q11. What is the difference between Kafka and RabbitMQ?
Apache Kafka	RabbitMQ
Distributed event streaming platform	Message broker
Stores events for configured retention	Messages are generally removed after acknowledgement
High-throughput event processing	Flexible message routing
Partition-based scalability	Queue-based processing
Useful for event streaming and analytics	Useful for task queues and messaging

Interview answer:

Kafka is suitable for high-throughput event streaming and event-driven architectures. RabbitMQ is useful for traditional message-based communication and complex routing.

The choice depends on business requirements.
Q12. How do you handle failures in asynchronous communication?
Interview-friendly answer:

In asynchronous communication, the producer sends a message without waiting for the consumer to process it.

If the consumer fails, we need to ensure that messages are not lost.

We can handle failures using:
1. Retry mechanism.
2. Dead Letter Queue (DLQ).
3. Message acknowledgement.
4. Idempotent consumers.
5. Monitoring and alerting.
For example, if Notification Service fails to process an order event, we can retry it. If it continues failing, we can move the message to a Dead Letter Queue for investigation.
3. Spring Boot Microservices Questions
Q13. What is Feign Client?
Feign Client is a declarative REST client provided through Spring Cloud OpenFeign.

It simplifies communication between microservices because we don't need to write boilerplate HTTP client code.

Example:
@FeignClient(name = "user-service")
public interface UserClient {

    @GetMapping("/users/{id}")
    User getUserById(@PathVariable Long id);
}


We can inject this interface into Order Service and call it like a normal Java method.
Q14. What is the difference between RestTemplate, WebClient and Feign Client?
RestTemplate	WebClient	Feign Client
Synchronous/blocking	Supports non-blocking reactive calls	Declarative HTTP client
Imperative API	Reactive API	Interface-based
Older approach	Modern WebFlux client	Spring Cloud integration
More manual code	Supports reactive streams	Less boilerplate

Interview answer:

RestTemplate is a synchronous HTTP client. WebClient supports both synchronous-style and asynchronous/reactive usage. Feign Client simplifies service-to-service communication using declarative interfaces.
Q15. How do you secure microservices?
Interview-friendly answer:

We secure microservices using Spring Security and OAuth 2.0 or OpenID Connect.

The client sends an access token, usually a JWT, with the request.

The API Gateway or individual microservices validate the token and check the required permissions.

We also implement:
- Role-based access control.
- HTTPS.
- Token expiration.
- Secure communication between services.
- Secrets management.
Q16. What is centralized configuration in microservices?
In microservices, maintaining configuration separately in every service can become difficult.

We use Spring Cloud Config Server to maintain centralized configuration.

For example:
Config Server
     |
     |---- Order Service
     |---- Payment Service
     |---- User Service


Each service fetches its configuration from the Config Server.

This makes configuration management easier across multiple environments.
4. Real-Time Scenario-Based Questions
These are especially important for 4.5 years of experience.
Interview question	What interviewer expects
One service is taking 10 seconds. How will you debug?	Logs, metrics, tracing, DB queries
How do you prevent duplicate payment?	Idempotency key, unique transaction reference
How do you handle 10,000 requests per second?	Horizontal scaling, load balancing, caching
How do you handle database failure?	Timeout, retry, circuit breaker
How do you maintain data consistency?	Saga, Outbox Pattern
How do you avoid duplicate Kafka messages?	Idempotent consumer, deduplication
How do you trace a request across services?	Correlation ID, distributed tracing
How do you deploy microservices?	Docker, Kubernetes, CI/CD
How do you handle API versioning?	URI/header versioning and backward compatibility
How do you improve slow APIs?	Profiling, indexing, caching, pagination

5. Important topics to prepare deeply
For your 4.5 years Java experience, prioritize these:
Priority	Topic
Must know	Microservices architecture
Must know	API Gateway
Must know	Eureka / Service Discovery
Must know	Feign Client
Must know	Circuit Breaker / Resilience4j
Must know	Saga Pattern
Must know	Kafka / RabbitMQ
Important	Distributed tracing
Important	Docker and Kubernetes
Important	OAuth2 and JWT
Important	Centralized configuration
Important	Database per service

6. Practice: Mock Interview – 4.5 Years Experience
Let's prepare as if you are attending an actual Java Backend Developer interview.

I'll ask one question at a time. You answer in your own English. I'll evaluate your answer out of 10 and provide:
1. Your score out of 10.
2. Mistakes and corrections.
3. Explanation in simple English.
4. Marathi explanation where useful.
5. An impressive interview-ready answer.
6. One follow-up scenario question.
Mock interview
Fundamentals

Question 1 of 6

4.5 years level



What are microservices, and why do we use microservices instead of monolithic architecture?

Submit my answerPreviousNext question

My recommendation: Don't just memorize definitions. Prepare each topic with one real-time example from your Order, Payment, Inventory or Pharma Inventory project. Interviewers at 4.5 years expect you to explain what you implemented, why you chose that approach, and how you handled failures.

In Spring Boot, we mainly use `@RestControllerAdvice` and `@ExceptionHandler` for global exception handling.

### 1. Which annotations are used?

| Annotation              | Purpose                                                                             |
| ----------------------- | ----------------------------------------------------------------------------------- |
| `@RestControllerAdvice` | Handles exceptions globally across REST controllers and returns response bodies.    |
| `@ControllerAdvice`     | Handles exceptions globally across controllers, commonly with view-based responses. |
| `@ExceptionHandler`     | Handles a specific exception type.                                                  |
| `@ResponseStatus`       | Defines the HTTP status code for an exception or handler.                           |

### 2. Practical example

Step 1: Create Custom Exception

```
public class EmployeeNotFoundException extends RuntimeException {

    public EmployeeNotFoundException(String message) {
        super(message);
    }
}
```

Step 2: Create Global Exception Handler

```
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(EmployeeNotFoundException.class)
    public ResponseEntity<String> handleEmployeeNotFound(
            EmployeeNotFoundException ex) {

        return new ResponseEntity<>(
                ex.getMessage(),
                HttpStatus.NOT_FOUND
        );
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGlobalException(Exception ex) {

        return new ResponseEntity<>(
                "Something went wrong",
                HttpStatus.INTERNAL_SERVER_ERROR
        );
    }
}
```

Step 3: Throw Exception from Service

```
public Employee getEmployeeById(Long id) {

    return employeeRepository.findById(id)
            .orElseThrow(() ->
                new EmployeeNotFoundException(
                    "Employee not found with ID: " + id
                )
            );
}
```

### 3. What is the execution flow?

Client Request

Controller

Service Layer

Exception is thrown

GlobalExceptionHandler

`@RestControllerAdvice` + `@ExceptionHandler`

ResponseEntity – HTTP 404 / 500

### 4. Interview-ready answer

"We use `@RestControllerAdvice` and `@ExceptionHandler` annotations for global exception handling in Spring Boot. `@RestControllerAdvice` catches exceptions across multiple controllers, and `@ExceptionHandler` handles specific exceptions. We can return appropriate HTTP status codes using ResponseEntity. This helps maintain consistent error responses throughout the application."

# Microservices – 10 Scenario-Based Interview Answers



4.5 Years Java Experience

Project-based answers



For your Tech Mahindra Senior Java Developer interview, I'll connect these answers with your Pharma Inventory and Batch Traceability System and Material Management System.

The answers are written in simple, professional English so you can speak them naturally during an interview.

## 1. What happens if one microservice is down?

Interview-friendly answer:

"In our microservices architecture, each service handles a specific business functionality. If one microservice goes down, the services depending on it may fail or experience delays.

For example, in our Pharma Inventory System, suppose the Inventory Service is unavailable. The Order Service cannot verify the available stock.

To handle this situation, we use timeout and circuit breaker mechanisms with Resilience4j. We can also use asynchronous communication through Kafka for operations that don't require an immediate response.

We log the failure, monitor the service and retry the operation when the service becomes available."

Technical keywords:

- Circuit Breaker
- Timeout
- Retry
- Fallback
- Kafka
- Health Checks

## 2. How do you prevent cascading failures?

Interview-friendly answer:

"Cascading failure happens when one service fails and its dependent services also start failing because of repeated requests.

For example, suppose Order Service continuously calls Inventory Service, but Inventory Service is slow or unavailable. This can consume Order Service threads and eventually affect the entire application.

To prevent this, we use Resilience4j Circuit Breaker, timeouts, limited retries and bulkhead patterns.

The circuit breaker temporarily stops requests to the failing service and allows the application to recover.

We also monitor service health using Spring Boot Actuator and application monitoring."

Technical keywords:

- Circuit Breaker
- Bulkhead
- Timeout
- Retry with backoff
- Spring Boot Actuator

## 3. How do you handle transactions across microservices?

Very important interview question

Interview-friendly answer:

"In microservices architecture, each service generally maintains its own database, so we cannot directly use a single database transaction across multiple services.

We use the Saga Pattern to manage distributed transactions.

For example, in our Material Management System, when a purchase order is created, multiple operations are involved:

1. Procurement Service creates the purchase order.
2. Approval Service handles manager approval.
3. Integration Service sends approved purchase order details to SAP.

If SAP integration fails after approval, we don't simply assume the entire process is successful. We maintain the transaction status and retry the integration or trigger a compensating business action if required.

Saga can be implemented using choreography or orchestration."

Technical keywords:

- Saga Pattern
- Choreography
- Orchestration
- Compensating Transaction
- Eventual Consistency
- Transaction Status

Important: Don't say that we use `@Transactional` across multiple independent microservices. It normally manages transactions within a service's transaction boundary.

## 4. How do you avoid duplicate messages in Kafka?

Interview-friendly answer:

"In an event-driven microservices architecture, Kafka may deliver the same message more than once, especially when a consumer processes a message but fails before committing its offset.

To avoid duplicate processing, we implement idempotent consumers.

For example, in our Material Management System, suppose a purchase order event is received twice. We maintain a unique transaction ID or event ID and check whether that event has already been processed.

If it is already processed, we skip the duplicate operation.

We can also use Kafka producer idempotence and appropriate offset management to improve message delivery reliability."

Technical keywords:

- Idempotent Consumer
- Unique Event ID
- Producer Idempotence
- Offset Management
- Deduplication
- Database Unique Constraint

Remember: Kafka producer idempotence prevents certain duplicate writes caused by producer retries. It does not automatically guarantee that your business operation executes only once.

## 5. What happens if Kafka consumer fails?

Interview-friendly answer:

"If a Kafka consumer fails while processing a message, the message can be processed again depending on the offset commit strategy.

For example, in our Material Management System, suppose a consumer is processing a purchase order event for SAP integration and the consumer application goes down.

After the consumer restarts, Kafka can deliver the uncommitted message again.

To handle this, we use proper offset management, retry mechanisms and Dead Letter Topics for messages that repeatedly fail.

We also make the consumer idempotent to avoid duplicate processing."

Technical keywords:

- Consumer Group
- Offset Commit
- Manual Acknowledgement
- Retry
- Dead Letter Topic (DLT)
- Idempotency

Follow-up: What is the difference between auto commit and manual commit?

- Auto commit: Kafka commits offsets automatically.
- Manual commit: Application controls when offsets are committed.

For important business processing, manual or carefully managed offset commits help avoid acknowledging messages before successful processing.

## 6. How do you handle 10,000 requests per second?

Interview-friendly answer:

"If our application receives 10,000 requests per second, first I would identify the bottleneck using application metrics, logs and database monitoring.

In our Inventory Management System, if multiple users access inventory details simultaneously, I would consider the following optimizations:

1. Horizontal scaling – run multiple instances of the service.
2. Load balancing – distribute requests across instances.
3. Caching – use Redis for frequently accessed inventory data.
4. Database optimization – add appropriate indexes and optimize SQL queries.
5. Connection pooling – configure HikariCP properly.
6. Asynchronous processing – use Kafka for background operations.
7. Monitoring – track response time, CPU, memory and error rates.

This helps improve throughput and application performance."

Technical keywords:

- Horizontal Scaling
- Load Balancer
- Redis Cache
- Database Indexing
- HikariCP
- Kafka
- Kubernetes
- Monitoring

Important follow-up: How will you identify the bottleneck?

Check:

- API response time.
- Database query execution time.
- CPU and memory utilization.
- Thread pool exhaustion.
- Database connection pool utilization.

## 7. How do you debug communication failure between services?

Interview-friendly answer:

"First, I identify which service is failing and check the application logs.

For example, suppose Order Service is unable to communicate with Inventory Service.

I follow these steps:

1. Check Order Service logs for HTTP errors or connection timeouts.
2. Verify whether Inventory Service is running.
3. Check the service URL, port and network connectivity.
4. Verify API Gateway or service discovery configuration.
5. Check authentication and authorization.
6. Check whether the target service is responding slowly.
7. Use correlation IDs to trace the request across services.

In Spring Boot, we can use Actuator for health checks and distributed tracing tools to identify where the request is failing.

After identifying the root cause, we fix it and monitor the service."

Technical keywords:

- Application Logs
- Correlation ID
- Distributed Tracing
- Spring Boot Actuator
- Eureka
- HTTP Status Codes
- Network Connectivity

## 8. What is the difference between synchronous and asynchronous communication?

Interview-friendly answer:

"In microservices, we mainly use two types of communication.

Synchronous communication: One service sends a request to another service and waits for its response.

For example, in our Pharma Inventory System, when we need to validate available stock before confirming an operation, the calling service can communicate with Inventory Service using REST API or Feign Client.

Asynchronous communication: One service sends a message or event without waiting for the consumer to finish processing it.

For example, after a purchase order is approved, we can publish an event to Kafka. Another service consumes that event and performs SAP integration or notification processing.

We use synchronous communication when an immediate response is required and asynchronous communication for background processing and loosely coupled services."

| Synchronous                | Asynchronous                |
| -------------------------- | --------------------------- |
| REST API / Feign           | Kafka / RabbitMQ            |
| Waits for response         | Doesn't wait for processing |
| Tighter runtime dependency | Looser coupling             |
| Immediate response         | Eventual processing         |
| Timeout handling important | Retry and DLQ important     |

## 9. How do you maintain data consistency across microservices?

Interview-friendly answer:

"In microservices architecture, every service generally manages its own database. So maintaining data consistency across services is important.

We use eventual consistency and the Saga Pattern to maintain consistency.

For example, in our Material Management System, after a purchase order is approved, we need to update the relevant business status and send the information to SAP.

We can publish an event after the local database transaction is successfully committed. The consuming service processes that event and updates its own data.

If processing fails, we use retry mechanisms and maintain transaction status. We also use idempotency to avoid duplicate updates.

For reliable event publishing, we can use the Transactional Outbox Pattern."

Technical keywords:

- Eventual Consistency
- Saga Pattern
- Transactional Outbox
- Kafka
- Idempotency
- Retry Mechanism
- Compensating Transactions

Important distinction:

- Saga handles a business transaction spanning multiple services.
- Outbox helps ensure that database changes and event publishing remain consistent.

## 10. How do you secure microservices?

Interview-friendly answer:

"We secure microservices using Spring Security and OAuth 2.0 or JWT-based authentication.

For example, in our Pharma Inventory System, different users such as Admin, Warehouse and Quality teams have different permissions.

When a user sends a request, the access token is validated. Based on the user's role and permissions, the application allows or denies access to the requested functionality.

We can implement authentication at API Gateway and authorization within individual microservices.

We also use HTTPS, secure secrets management, token expiration and role-based access control."

Technical keywords:

- Spring Security
- JWT
- OAuth 2.0
- Authentication
- Authorization
- RBAC
- HTTPS
- API Gateway
- AWS Secrets Manager

# 11. Most important keywords to remember

| Scenario                 | Keywords to mention                |
| ------------------------ | ---------------------------------- |
| Service down             | Circuit Breaker, Timeout, Fallback |
| Cascading failure        | Bulkhead, Retry, Resilience4j      |
| Distributed transaction  | Saga, Compensation                 |
| Duplicate Kafka messages | Idempotency, Event ID              |
| Consumer failure         | Offset, Retry, DLT                 |
| High traffic             | Load Balancing, Caching, Scaling   |
| Communication failure    | Logs, Correlation ID, Tracing      |
| Service communication    | REST, Feign, Kafka                 |
| Data consistency         | Eventual Consistency, Outbox       |
| Security                 | JWT, OAuth2, Spring Security       |

# 12. How to answer like a senior developer

Follow this structure for every scenario-based question:

1. Problem: Explain the situation.
2. Approach: Explain how you handle it.
3. Technology: Mention Spring Boot / Kafka / Resilience4j etc.
4. Project example: Connect it to your business workflow.
5. Result: Explain what benefit it provides.

Important interview advice

One thing to be careful about: your actual project experience includes RabbitMQ-based asynchronous processing and SAP OData integration. Don't claim you implemented Kafka, Saga or Resilience4j in production if you only studied them. You can say, "I understand this approach, and I would implement it using..."

This makes your answers technically strong and credible.

My recommendation: Practise questions 1, 2, 3, 4, 5 and 9 especially well. These test whether you understand real microservices problems rather than just definitions.
### 5. Interview follow-up question

What is the difference between `@ControllerAdvice` and `@RestControllerAdvice`?

Try answering this in your own words. I'll evaluate your answer out of 10.
