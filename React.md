Perfect 👍
Here are **TOP 25 React Interview Questions & Answers** tailored for **3 years experience** — **clear, crisp, interview-ready**, with **real-project context** where possible.

---

# ✅ Top 25 React Interview Q&A (3 Years Experience)

---

## 1️⃣ What is React?

**Answer:**
React is a JavaScript library for building user interfaces using reusable, component-based architecture. It uses Virtual DOM for efficient UI updates.

---

## 2️⃣ What is Virtual DOM?

**Answer:**
Virtual DOM is an in-memory representation of the real DOM. React compares the previous and current Virtual DOM and updates only the changed parts in the real DOM.

---

## 3️⃣ Difference between Props and State?

| Props                  | State                    |
| ---------------------- | ------------------------ |
| Passed from parent     | Managed within component |
| Read-only              | Mutable                  |
| Used for configuration | Used for dynamic data    |

---

## 4️⃣ Functional vs Class Components?

**Answer:**
Functional components are simpler, use hooks for state and lifecycle, and are preferred over class components for better readability and performance.

---

## 5️⃣ What are Hooks?

**Answer:**
Hooks allow functional components to use state and lifecycle features without writing class components.

---

## 6️⃣ Explain `useState`

**Answer:**
`useState` is used to manage local component state and triggers re-render when the state changes.

---

## 7️⃣ Explain `useEffect`

**Answer:**
`useEffect` handles side effects like API calls, subscriptions, and timers. The dependency array controls when it executes.

---

## 8️⃣ What is dependency array in `useEffect`?

**Answer:**
It determines when the effect runs. Empty array runs once, no array runs on every render, values inside run when they change.

---

## 9️⃣ What is `useMemo`?

**Answer:**
`useMemo` memoizes expensive computations to avoid recalculating them on every render.

---

## 🔟 Difference between `useMemo` and `useCallback`?

**Answer:**
`useMemo` memoizes values, while `useCallback` memoizes functions.

---

## 1️⃣1️⃣ What is React.memo?

**Answer:**
React.memo prevents unnecessary re-renders of a component by memoizing it based on props.

---

## 1️⃣2️⃣ How do you optimize React performance?

**Answer:**
Using React.memo, useCallback, useMemo, lazy loading, code splitting, and avoiding unnecessary state updates.

---

## 1️⃣3️⃣ What is controlled vs uncontrolled component?

**Answer:**
Controlled components manage input value using state. Uncontrolled components use refs to access DOM values.

---

## 1️⃣4️⃣ What is lifting state up?

**Answer:**
Moving shared state to the nearest common parent so multiple components can access and update it.

---

## 1️⃣5️⃣ What is Context API?

**Answer:**
Context API is used to pass data globally without prop drilling, commonly used for auth and theme management.

---

## 1️⃣6️⃣ What is Redux and why use it?

**Answer:**
Redux is a predictable state management library used when application state becomes complex and shared across many components.

---

## 1️⃣7️⃣ Difference between Context API and Redux?

**Answer:**
Context is for simple global state, Redux is better for complex state with middleware, debugging, and scalability.

---

## 1️⃣8️⃣ How do you handle API calls in React?

**Answer:**
Using `fetch` or `axios` inside `useEffect` with loading and error states.

---

## 1️⃣9️⃣ What is debouncing?

**Answer:**
Debouncing limits function execution until the user stops triggering an event, commonly used in search inputs.

---

## 2️⃣0️⃣ What is React Router?

**Answer:**
React Router enables navigation between different components in a single-page application without page reload.

---

## 2️⃣1️⃣ What are keys in React?

**Answer:**
Keys help React identify list items uniquely and improve rendering performance.

---

## 2️⃣2️⃣ What is lazy loading?

**Answer:**
Lazy loading loads components only when required, improving initial load performance.

---

## 2️⃣3️⃣ How do you handle authentication in React?

**Answer:**
Using JWT tokens, protected routes, role-based rendering, and secure API calls.

---

## 2️⃣4️⃣ What is Error Boundary?

**Answer:**
Error Boundaries catch JavaScript errors in child components and display fallback UI instead of crashing the app.

An Error Boundary is a React component that catches JavaScript errors in its child component tree and displays a fallback UI instead of crashing the entire application.

In simple words:
👉 It prevents the whole app from breaking when a component throws an error.

An Error Boundary is a React component that catches JavaScript errors in its child component tree and displays a fallback UI instead of crashing the entire application.

In simple words:
👉 It prevents the whole app from breaking when a component throws an error.
✅ Why do we need Error Boundaries?

Without Error Boundary:
One UI error → entire app crashes

With Error Boundary:
Error is caught
Fallback UI is shown
App continues running

Example use cases:
Dashboard widgets
Third-party components
Large UI sections

How Error Boundary works internally?
React provides lifecycle methods:
static getDerivedStateFromError()
componentDidCatch()

✅ How to explain in interview (short & crisp)
“Error Boundaries are React components used to catch runtime errors in child components and show a fallback UI instead of crashing the whole application. They improve application stability and user experience.”

✅ Real Project Example (Say this 🔥)
“In our hospital IT dashboard, we wrapped critical widgets like charts and tables with Error Boundaries so that if one widget failed, the rest of the dashboard continued to work.”
---


How to Handle Errors in Hooks (React)

Important rule (say this first):
Hooks cannot use Error Boundaries directly.
Errors must be handled manually inside hooks or wrapped by an Error Boundary at component level.

## 2️⃣5️⃣ How do you test React components?

**Answer:**
Using Jest and React Testing Library to test rendering, user interactions, and component behavior.

---

Perfect 👍
Here’s a **clear, confident, interview-ready answer** you can speak naturally when asked
**“Class Component vs Functional Component in React”**.

---

## 🧠 **Short & Strong Interview Answer (Best to Say First)**

> “Class components are ES6 classes that use lifecycle methods and `this` keyword, whereas functional components are simple JavaScript functions that use React Hooks to manage state and side effects. Since React 16.8, functional components are preferred due to cleaner code, better readability, and easier reuse.”

---

## 🔹 **Explain Class Component (Brief)**

> “A class component extends `React.Component`, uses `this.state` for state management, and lifecycle methods like `componentDidMount` and `componentDidUpdate`.”

Example (mention, don’t write unless asked):

* Uses `this`
* More boilerplate
* Harder to reuse logic

---

## 🔹 **Explain Functional Component (Brief)**

> “A functional component is a plain JavaScript function. With hooks like `useState` and `useEffect`, it can handle state and lifecycle behavior without classes.”

Why better:

* Less code
* Easier to test
* Better performance optimizations
* Hooks enable logic reuse

---

## 🔥 **Comparison Table (Say only key points)**

| Class Component   | Functional Component |
| ----------------- | -------------------- |
| Uses `class`      | Uses function        |
| Uses `this`       | No `this`            |
| Lifecycle methods | Hooks (`useEffect`)  |
| More boilerplate  | Clean & concise      |
| Legacy approach   | Modern & recommended |

---

## 🎯 **Lifecycle Mapping (INTERVIEW GOLD)**

> “In functional components, `useEffect` replaces lifecycle methods.”

| Class                | Functional                |
| -------------------- | ------------------------- |
| componentDidMount    | `useEffect(() => {}, [])` |
| componentDidUpdate   | `useEffect(() => {})`     |
| componentWillUnmount | cleanup in `useEffect`    |

---

## 💼 **Real Project Line (Very Important)**

> “In my recent projects, I primarily used functional components with hooks because they reduce complexity and make the code easier to maintain.”

---

## 🧠 **If Interviewer Asks: Which One Do You Prefer?**

> “I prefer functional components with hooks because they provide cleaner code, better separation of logic, and align with modern React best practices.”

---

## 🎯 **One-Line Closing Statement**

> “Today, functional components are the standard in React development, and class components are mostly used in legacy codebases.”

---
Got you 👍
Here’s a **super-crisp, interview-ready answer** you can **say exactly as it is**.

---

## 🎤 Interview Answer: `var` vs `let` vs `const`

> In JavaScript, `var`, `let`, and `const` are used to declare variables.
> `var` is function-scoped and can be re-declared and re-assigned, which may cause bugs, so it’s generally avoided.
> `let` and `const` are block-scoped. `let` is used when the value needs to change, while `const` is used when the reference should not change.
> `const` prevents reassignment but allows mutation of objects.
> Best practice is to use `const` by default, `let` when reassignment is needed, and avoid `var`.

---

## ⚡ One-Line Version (If Interviewer Is in Hurry)

> `var` is function-scoped and unsafe, `let` is block-scoped and mutable, and `const` is block-scoped with fixed reference.

---

## ⭐ Bonus Line (Adds Impact)

> `let` and `const` also avoid issues like hoisting bugs by using the temporal dead zone.

---

Perfect 👍 this is a **very common JS interview question**.
Here’s an **interview-ready answer** you can say confidently.

---

## 🎤 Interview Answer: Arrow Function vs Normal Function

> Arrow functions are a shorter syntax for writing functions and they do not have their own `this`.
> Normal functions have their own `this` depending on how they are called.
> Arrow functions are best for callbacks, while normal functions are better for object methods and constructors.

---

## 🔥 Key Differences (Interview Must-Know)

| Feature               | Arrow Function      | Normal Function |
| --------------------- | ------------------- | --------------- |
| Syntax                | Short & concise     | Longer          |
| `this`                | Lexically inherited | Own `this`      |
| `arguments`           | ❌ Not available     | ✅ Available     |
| Constructor           | ❌ Cannot be used    | ✅ Can be used   |
| `call / apply / bind` | ❌ No effect         | ✅ Works         |
| Hoisting              | ❌ Not hoisted       | ✅ Hoisted       |

---

## 🧠 `this` Difference (MOST IMPORTANT)

### Normal Function

```js
function show() {
  console.log(this);
}
```

### Arrow Function

```js
const show = () => {
  console.log(this);
};
```

### Interview Explanation:

> Arrow functions take `this` from the surrounding scope, so they don’t change context.

---

## ❓ Why Arrow Functions Are Preferred in React?

### ✅ Answer

> Because arrow functions do not create their own `this`, avoiding binding issues in callbacks.

---

## ⚠️ When NOT to Use Arrow Functions?

### ✅ Strong Answer

> Arrow functions should not be used as object methods or constructors because they don’t have their own `this`.

---

## 🧠 Real-Life Example

```js
const user = {
  name: "Alex",
  sayHi: () => {
    console.log(this.name); // undefined
  }
};
```

❌ Wrong

```js
const user = {
  name: "Alex",
  sayHi() {
    console.log(this.name); // Alex
  }
};
```

✅ Correct

---

## 🎯 One-Line Power Answer

> Arrow functions inherit `this` from their parent scope, while normal functions have their own `this`.

---

Perfect 👍 this is a **VERY common React interview question**.
Here’s a **clean, interview-ready answer** you can say confidently.

---

## 🎤 Interview Answer: `useMemo` vs `useCallback`

> `useMemo` is used to memoize the **result of a calculation**, while `useCallback` is used to memoize a **function reference**.
> Both are performance optimization hooks and prevent unnecessary re-renders.

---

## 🔥 Key Difference (Say This Clearly)

| Feature          | useMemo                | useCallback               |
| ---------------- | ---------------------- | ------------------------- |
| What it returns  | Memoized **value**     | Memoized **function**     |
| Used for         | Expensive calculations | Stable function reference |
| Re-computed when | Dependencies change    | Dependencies change       |

---

## 🧠 Simple Example (Interview Friendly)

### 🔹 `useMemo`

```js
const total = useMemo(() => {
  return calculateTotal(items);
}, [items]);
```

🗣️ Say:

> Here, the calculation runs only when items change.

---

### 🔹 `useCallback`

```js
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

🗣️ Say:

> The function reference remains the same between renders.

---

## ❓ Why use `useCallback` with `React.memo`?

### ✅ Answer

> Without useCallback, a new function is created on every render, causing child components to re-render unnecessarily.

---

## ⚠️ Common Interview Trap

❓ *Can useMemo replace useCallback?*

### ✅ Perfect Answer

> Technically yes, but useCallback is clearer and more readable for memoizing functions.

---

## ❓ When NOT to use them?

### ✅ Strong Answer

> Overusing them can increase complexity and memory usage. They should be used only for expensive operations or performance issues.

---

## 🎯 One-Line Power Answer (If Time Is Short)

> `useMemo` memoizes values, `useCallback` memoizes functions.

---

## ⭐ Bonus Line (Impress Interviewer)

> Both hooks help optimize performance but should be used based on profiling, not assumptions.

---





