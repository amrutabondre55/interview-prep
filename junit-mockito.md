| Annotation     | Purpose          |
| -------------- | ---------------- |
| `@Test`        | Test method      |
| `@Mock`        | Fake dependency  |
| `@InjectMocks` | Class under test |
| `@ExtendWith`  | Enable Mockito   |
| `@BeforeEach`  | Setup            |

--------------------------
Here’s a **small, interview-friendly mini project for JUnit + Mockito**, plus **5 common interview Q&A**, explained **step-by-step** and **easy to speak**.

---

# ✅ Mini Project: Employee Service (JUnit + Mockito)

### 📌 Scenario

> We want to **fetch employee details**.
> Service depends on Repository (DB).
> In unit testing, **we mock the repository**.

---

## 1️⃣ Employee Entity

```java
// Simple POJO class
public class Employee {

    private int id;
    private String name;

    // Constructor to initialize values
    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Getter for id
    public int getId() {
        return id;
    }

    // Getter for name
    public String getName() {
        return name;
    }
}
```

---

## 2️⃣ Repository Layer (Dependency)

```java
// Repository interface (DB layer)
public interface EmployeeRepository {

    // Method to fetch employee by id
    Employee findById(int id);
}
```

---

## 3️⃣ Service Layer (Business Logic)

```java
// Service class
public class EmployeeService {

    // Dependency
    private EmployeeRepository employeeRepository;

    // Constructor injection
    public EmployeeService(EmployeeRepository employeeRepository) {
        this.employeeRepository = employeeRepository;
    }

    // Business method
    public String getEmployeeName(int id) {

        // Call repository
        Employee employee = employeeRepository.findById(id);

        // Business validation
        if (employee == null) {
            return "Employee Not Found";
        }

        return employee.getName();
    }
}
```

---

## 4️⃣ JUnit + Mockito Test Class ⭐ (Most Important)

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.Mockito.when;

import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

// Test class
public class EmployeeServiceTest {

    // Mocking repository
    @Mock
    private EmployeeRepository employeeRepository;

    // Injecting mock into service
    @InjectMocks
    private EmployeeService employeeService;

    // Constructor to initialize mocks
    public EmployeeServiceTest() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testEmployeeFound() {

        // Mock behavior
        when(employeeRepository.findById(1))
                .thenReturn(new Employee(1, "Amruta"));

        // Call service method
        String result = employeeService.getEmployeeName(1);

        // Verify result
        assertEquals("Amruta", result);
    }

    @Test
    public void testEmployeeNotFound() {

        // Mock behavior for null
        when(employeeRepository.findById(2))
                .thenReturn(null);

        // Call service method
        String result = employeeService.getEmployeeName(2);

        // Verify result
        assertEquals("Employee Not Found", result);
    }
}
```

---

## 🔁 What Is Happening (Interview Flow)

1️⃣ JUnit runs test
2️⃣ Mockito creates mock repository
3️⃣ Service uses mocked repository
4️⃣ No real DB call
5️⃣ Only business logic is tested

---

# 🎯 How to Explain This Project in Interview (30 seconds)

> **“I wrote unit tests for the service layer using JUnit and Mockito.
> I mocked the repository to avoid database calls and tested only business logic.
> Mockito helps simulate repository behavior, and JUnit validates the output.”**

---

# ⭐ 5 Important JUnit + Mockito Interview Q&A

---

## 1️⃣ What is JUnit?

> **“JUnit is a unit testing framework used to test individual methods or classes in Java.”**

---

## 2️⃣ What is Mockito?

> **“Mockito is a mocking framework used to create fake objects for dependencies during unit testing.”**

---

## 3️⃣ Why use Mockito with JUnit?

> **“To isolate the unit under test by mocking external dependencies like DB or APIs.”**

---

## 4️⃣ Difference between @Mock and @InjectMocks?

> **@Mock** → Creates fake object
> **@InjectMocks** → Injects mocks into class under test

---

## 5️⃣ What is stubbing in Mockito?

> **“Defining mock behavior using `when().thenReturn()` is called stubbing.”**

Example:

```java
when(repo.findById(1)).thenReturn(employee);
```

---

## 🏁 One-Line Interview Summary (Very Strong)

> **“JUnit tests the business logic, and Mockito mocks dependencies to avoid real external calls.”**

---

