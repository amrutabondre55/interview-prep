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

### 5. Interview follow-up question

What is the difference between `@ControllerAdvice` and `@RestControllerAdvice`?

Try answering this in your own words. I'll evaluate your answer out of 10.
