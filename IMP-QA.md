### ✅ Improving API Performance

**Backend Improvements:**

* **SQL Optimization & Indexing:** Speeds up database queries
* **Caching (Redis):** Stores frequent data in memory to reduce DB hits
* **Read Replicas:** Offloads read-heavy traffic from primary DB
* **Parallel Processing (Multithreading):** Handles multiple requests simultaneously

**Frontend Improvements:**

* **CDN (CloudFront):** Caches static content globally for faster load

**30-Second Summary:**

> **“We improve API performance by optimizing SQL queries with indexing, caching frequent data using Redis, using read replicas for heavy reads, and parallel processing with multithreading. On the frontend, CloudFront caches static content globally to reduce latency.”**


------

### ✅ React Hooks for Performance Improvement

Here’s a **short, interview-ready answer**:

---

### **1️⃣ useMemo**

* **Purpose:** Memoizes expensive calculations
* **Use Case:** Prevents recalculating values on every render
* **Example:** `const result = useMemo(() => expensiveCalculation(data), [data])`

---

### **2️⃣ useCallback**

* **Purpose:** Memoizes functions
* **Use Case:** Prevents re-creating functions on every render, useful for passing callbacks to child components
* **Example:** `const handleClick = useCallback(() => doSomething(), [dependencies])`

---

### **3️⃣ React.memo (Not a hook, but related)**

* **Purpose:** Memoizes functional components
* **Use Case:** Prevents unnecessary re-render of child components
* **Example:** `export default React.memo(MyComponent)`

---

### **4️⃣ useRef**

* **Purpose:** Stores mutable values that don’t trigger re-render
* **Use Case:** Persist values like DOM references or previous state for optimization

---

### **5️⃣ useTransition & useDeferredValue** (React 18+)

* **Purpose:** Optimize UI responsiveness for heavy renders
* **Use Case:** Marks non-urgent updates to avoid blocking UI
* **Example:** `const deferredValue = useDeferredValue(value)`

---

### **30-Second Interview Summary**

> **“We use `useMemo` to memoize expensive calculations, `useCallback` to memoize functions, `React.memo` for component memoization, `useRef` to avoid unnecessary re-renders, and `useTransition`/`useDeferredValue` to keep the UI responsive during heavy renders.”**

---

### ✅ Short Interview Answer – Debounce

> **“Debounce is used to limit how often a function is executed, usually to reduce frequent calls like search input or API requests.”**

**Example (React):**

```javascript
const handleSearch = debounce((value) => {
  fetchData(value);
}, 300); // waits 300ms after user stops typing
```

**One-Line Explanation:**

> The function runs only after the user stops typing for 300ms, improving performance.

