Here are **15 commonly asked REST API interview questions with clear, interview-ready answers**. I’ve kept them **simple, crisp, and easy to remember** — perfect for Java / Spring Boot interviews.

---

## 1️⃣ What is REST API?

**Answer:**
REST (Representational State Transfer) is an architectural style used to build **stateless, scalable web services** that communicate over HTTP using standard methods like GET, POST, PUT, DELETE.

---

## 2️⃣ What are the main principles of REST?

**Answer:**

1. Client–Server
2. Stateless
3. Cacheable
4. Uniform Interface
5. Layered System

---

## 3️⃣ What is a resource in REST?

**Answer:**
A resource is any **data entity** exposed by the API and identified using a **URI**.
Example:

```
/users/101
```

---

## 4️⃣ Difference between REST and SOAP?

**Answer:**

| REST        | SOAP                    |
| ----------- | ----------------------- |
| Lightweight | Heavy                   |
| Uses HTTP   | Uses XML-based protocol |
| JSON/XML    | Only XML                |
| Faster      | Slower                  |

---

## 5️⃣ What are HTTP methods used in REST?

**Answer:**

* **GET** → Fetch data
* **POST** → Create data
* **PUT** → Update entire resource
* **PATCH** → Partial update
* **DELETE** → Remove resource

---

## 6️⃣ Difference between PUT and PATCH?

**Answer:**

* **PUT** replaces the **entire resource**
* **PATCH** updates **only specific fields**

---

## 7️⃣ What is statelessness in REST?

**Answer:**
Each request contains all required information.
The server **does not store client session data**.

---

## 8️⃣ What is HTTP status code?

**Answer:**
Status codes indicate the **result of an API request**.

Common examples:

* 200 – OK
* 201 – Created
* 400 – Bad Request
* 401 – Unauthorized
* 404 – Not Found
* 500 – Internal Server Error

---

## 9️⃣ What is idempotency?

**Answer:**
An operation is idempotent if **multiple identical requests give the same result**.

Examples:

* GET ✔️
* PUT ✔️
* DELETE ✔️
* POST ❌

---

## 🔟 What is API versioning?

**Answer:**
Used to manage changes without breaking existing clients.

Example:

```
/api/v1/users
/api/v2/users
```

---

## 1️⃣1️⃣ What is Content-Type and Accept header?

**Answer:**

* **Content-Type** → format of request body sent by client
* **Accept** → format expected in response

Example:

```
application/json
```

---

## 1️⃣2️⃣ What is JWT in REST API?

**Answer:**
JWT (JSON Web Token) is a **stateless authentication mechanism** where a token is sent in every request:

```
Authorization: Bearer <token>
```

---

## 1️⃣3️⃣ What is CORS?

**Answer:**
CORS allows a frontend hosted on one domain to access APIs from another domain by setting HTTP headers.

---

## 1️⃣4️⃣ Difference between 401 and 403?

**Answer:**

* **401 Unauthorized** → User not authenticated
* **403 Forbidden** → User authenticated but not authorized

---

## 1️⃣5️⃣ How do you secure REST APIs?

**Answer:**

* JWT / OAuth2
* HTTPS
* Input validation
* Rate limiting
* Role-based access control

---

### ✅ Bonus Tip for Interview

If asked **“Have you used REST APIs in your project?”**, always mention:

* HTTP methods
* Status codes
* JWT
* Validation
* Exception handling

---

Here are **5 very common microservices interview questions** with **simple, clear answers** that match your **3+ years Java Full Stack profile** and your **pharma project context**.

---

## ✅ 1) What are Microservices?

**Answer (Simple English):**

> Microservices is an architecture where a large application is broken into **small, independent services**.
> Each service focuses on **one business capability**, has its **own database**, and communicates with other services using **REST APIs or messaging**.

**Example:**

> In our pharma system, Inventory, Batch, and Reporting can be separate microservices.

---

## ✅ 2) How do microservices communicate with each other?

**Answer:**

> Microservices communicate mainly using **REST APIs** over HTTP.
> In some cases, **asynchronous communication** using message queues like Kafka or RabbitMQ is used.

**In my project:**

> Our services communicated using **REST APIs**, and API Gateway was used to route requests.

---

## ✅ 3) What are the advantages of microservices?

**Answer:**

> The main advantages are:

* Independent deployment
* Better scalability
* Fault isolation
* Faster development by multiple teams

**Example:**

> If Reporting service fails, Inventory service still works.

---

## ✅ 4) How is security handled in microservices?

**Answer:**

> Security is handled using **JWT or OAuth**, where a token is generated after login and passed with every API request.
> API Gateway validates the token before forwarding the request to services.

**In my project:**

> We used **role-based access control** and token-based authentication.

---

## ✅ 5) What challenges did you face with microservices and how did you handle them?

**Answer:**

> Some common challenges are:

* Service communication failures
* Data consistency
* Debugging issues

**How we handled:**

> We used proper **logging**, **exception handling**, **timeouts**, and followed clear API contracts.

---

## 🎯 Bonus One-Liner (Very Impressive)

> “Microservices help us scale and deploy features independently, but they require good API design, monitoring, and communication handling.”

Got it — here’s a **clear, interview-ready explanation of REST communication** 👇

---

## 🔗 What is REST Communication?

**REST (Representational State Transfer) communication** is a way for a **client and server to talk to each other over HTTP** using standard rules.

In simple words:
👉 *Frontend or client sends an HTTP request → Backend processes it → Sends back a response (usually JSON).*

---

## 🧠 How REST Communication Works (Flow)

1. **Client** (Browser / Mobile App / Postman) sends a request
2. **Request contains**

   * URL (endpoint)
   * HTTP method (GET, POST, PUT, DELETE)
   * Headers
   * Body (optional)
3. **Server** processes the request
4. **Server sends a response**

   * Status code (200, 201, 400, 404, 500)
   * Data (mostly JSON)

---

## 🌐 HTTP Methods Used in REST

| Method | Purpose             | Interview Line      |
| ------ | ------------------- | ------------------- |
| GET    | Read data           | Fetch resource      |
| POST   | Create data         | Create new resource |
| PUT    | Update full data    | Replace resource    |
| PATCH  | Update partial data | Modify resource     |
| DELETE | Remove data         | Delete resource     |

---

## 📦 Example REST Communication

### Request

```
GET /api/employees/101
```

### Response

```json
{
  "id": 101,
  "name": "Amruta",
  "role": "Full Stack Developer"
}
```

---

## 🔑 Key Principles of REST (Very Important)

1. **Stateless**

   * Server does not store client session
   * Each request is independent

2. **Client–Server Architecture**

   * Frontend and backend are separate

3. **Uniform Interface**

   * Same rules for all APIs
   * Uses HTTP methods & status codes

4. **Resource-Based**

   * Everything is a resource (user, order, product)

---

## 📊 Common HTTP Status Codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 404  | Not Found             |
| 500  | Internal Server Error |

---

## 🎯 How to Say in Interview (Perfect Answer)

> “REST communication is a stateless client-server communication that uses HTTP methods like GET, POST, PUT, and DELETE to exchange data, usually in JSON format. Each request contains all the required information, and the server responds with proper status codes and data.”

---

## What is Configuration Management?

**Answer:**
Configuration Management is the process of managing, storing, and controlling application settings separately from the code so that the same application can run in different environments (dev, test, prod) without code changes.

👉 In short: change behavior without changing code.

“Configuration management is the practice of externalizing application settings so that the same codebase can be deployed across multiple environments by changing only configuration values. In Spring Boot, this is achieved using properties files, profiles, and tools like Spring Cloud Config.”

“In production, we change the database and API keys using configuration files without touching the application code.”

---


