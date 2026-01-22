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

If you want, I can also provide:

* **Java + Spring Boot REST interview answers**
* **2-minute REST explanation**
* **Real project REST API example**
* **Tricky REST interview questions**

Just tell me 👍
