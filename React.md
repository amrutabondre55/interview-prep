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


