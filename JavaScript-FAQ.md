Absolutely! Let’s go **question by question**, with **clear explanations + answers + examples**, in a way you can **say directly in an interview**. I’ll cover the **top 30 advanced JS questions** for **3+ years experience**. I’ll keep it **structured, easy to memorize, and with examples**.

---

# **Top 30 Advanced JavaScript Questions Explained**

---

### **1. Difference between `var`, `let`, and `const`**

**Answer (Interview style):**
“`var` is function-scoped, can be redeclared, and is hoisted. `let` is block-scoped, cannot be redeclared in the same scope, and is hoisted but not initialized. `const` is block-scoped, cannot be reassigned, and must be initialized at declaration.”

**Example:**

```javascript
var a = 1; // function-scoped
let b = 2; // block-scoped
const c = 3; // block-scoped and constant
b = 4; // ✅ allowed
// c = 5; // ❌ error
```

---

### **2. Explain `this` in JavaScript**

**Answer:**
“`this` refers to the execution context. In a global function, it points to `window` (browser). In an object method, it points to the object. Arrow functions inherit `this` from their enclosing scope.”

```javascript
const obj = { name: "Amruta", greet() { console.log(this.name); } };
obj.greet(); // Amruta

const arrow = () => console.log(this.name);
arrow(); // undefined
```

---

### **3. Difference between `==` and `===`**

**Answer:**
“`==` compares values with type coercion, while `===` compares both value and type without coercion. Always prefer `===` to avoid unexpected results.”

```javascript
5 == '5';  // true
5 === '5'; // false
```

---

### **4. What is a closure?**

**Answer:**
“A closure is a function that remembers variables from its outer scope even after the outer function finishes executing.”

```javascript
function outer() {
  let count = 0;
  return function() { count++; return count; };
}
const increment = outer();
increment(); // 1
increment(); // 2
```

---

### **5. `null` vs `undefined`**

**Answer:**
“`undefined` means a variable has been declared but not assigned. `null` is an explicit assignment representing ‘no value’.”

```javascript
let a;
console.log(a); // undefined
let b = null;
console.log(b); // null
```

---

### **6. Event Loop**

**Answer:**
“JavaScript is single-threaded. The Event Loop handles asynchronous code. Synchronous code executes first, async code like `setTimeout` goes to the task queue and runs after the stack is empty.”

```javascript
console.log("Start");
setTimeout(() => console.log("Async"), 0);
console.log("End");
// Output: Start → End → Async
```

---

### **7. Synchronous vs Asynchronous**

**Answer:**
“Synchronous code runs line by line. Asynchronous code runs in the background and executes later, allowing non-blocking behavior.”

```javascript
console.log("1");
setTimeout(() => console.log("2"), 1000);
console.log("3"); // Output: 1 → 3 → 2
```

---

### **8. Promises & async/await**

**Answer:**
“A Promise represents a value that may be available now or in the future. `async/await` allows writing asynchronous code in a synchronous style.”

```javascript
async function fetchData() {
  try {
    const res = await fetch("https://api.example.com");
    const data = await res.json();
    console.log(data);
  } catch(e) {
    console.error(e);
  }
}
```

---

### **9. `call`, `apply`, `bind`**

**Answer:**

* `call`: invokes function with `this` and individual arguments
* `apply`: like call, but arguments as array
* `bind`: returns a new function with bound `this`

```javascript
function greet(age) { console.log(`${this.name} is ${age}`); }
const p = { name: "Amruta" };
greet.call(p, 25);   // Amruta is 25
greet.apply(p, [25]); // Amruta is 25
const bound = greet.bind(p, 25);
bound();               // Amruta is 25
```

---

### **10. Hoisting**

**Answer:**
“Variables and function declarations are hoisted to the top. `var` is initialized with `undefined`, `let` and `const` are hoisted but not initialized.”

```javascript
console.log(a); // undefined
var a = 5;
```

---

### **11. `for...in` vs `for...of`**

**Answer:**

* `for...in` → iterates over object keys
* `for...of` → iterates over iterable values (array, string)

```javascript
const arr = [10,20,30];
for (let index in arr) console.log(index); // 0,1,2
for (let value of arr) console.log(value); // 10,20,30
```

---

### **12. Data types & Reference vs Value**

**Answer:**

* Primitive: string, number, boolean, null, undefined, symbol, bigint → passed by value
* Reference: object, array, function → passed by reference

---

### **13. Event Delegation**

**Answer:**
“Instead of adding listeners to many child elements, we attach one listener to the parent and use event bubbling.”

```javascript
document.getElementById("list").addEventListener("click", e => {
  if(e.target.tagName === "LI") console.log(e.target.textContent);
});
```

---

### **14. Prototype & Inheritance**

**Answer:**
“JavaScript uses prototypal inheritance. Objects inherit from `prototype`.”

```javascript
function Person(name) { this.name=name; }
Person.prototype.greet = function() { console.log(`Hi, I'm ${this.name}`); };
const p = new Person("Amruta");
p.greet(); // Hi, I'm Amruta
```

---

### **15. Debounce vs Throttle**

**Answer:**

* **Debounce** → wait until action stops
* **Throttle** → limit frequency of execution

```javascript
// Debounce
const debounce = (fn, delay) => { let timer; return (...args) => { clearTimeout(timer); timer = setTimeout(() => fn(...args), delay); } };

// Throttle
const throttle = (fn, limit) => { let inThrottle; return (...args) => { if(!inThrottle){ fn(...args); inThrottle=true; setTimeout(() => inThrottle=false, limit); fn(...args); } } };
```

---

### **16. Shallow vs Deep Copy**

**Answer:**

* Shallow → copies top-level, nested objects are references
* Deep → copies everything

```javascript
let obj = { a:1, b:{c:2} };
let shallow = {...obj};
let deep = JSON.parse(JSON.stringify(obj));
```

---

### **17. `async` vs `defer` in scripts**

**Answer:**

* `async` → loads script asynchronously, executes immediately
* `defer` → loads script asynchronously, executes after HTML parsing

---

### **18. `let` vs `const` in loops**

**Answer:**
“`let` creates a new binding per iteration. `const` cannot be reassigned.”

```javascript
for (let i=0; i<3; i++) console.log(i); // 0 1 2
```

---

### **19. Callbacks, Promises, Async/Await**

**Answer:**

* Callback → function passed as arg
* Promise → object representing future value
* Async/Await → syntactic sugar for Promises

---

### **20. Arrow function & `this`**

**Answer:**
“Arrow functions inherit `this` from the parent scope.”

```javascript
const obj = { a:10, arrow:()=>console.log(this.a) };
obj.arrow(); // undefined
```

---

### **21. Memory leak in JS**

**Answer:**

* Unreferenced objects in closures
* Timers not cleared
* Global variables

---

### **22. `map`, `forEach`, `filter`, `reduce`**

```javascript
[1,2,3].map(x=>x*2);    // [2,4,6]
[1,2,3].filter(x=>x>1); // [2,3]
[1,2,3].reduce((a,b)=>a+b,0); // 6
```

---

### **23. `Object.freeze` vs `Object.seal`**

* Freeze → cannot modify or add properties
* Seal → cannot add, but can modify existing

---

### **24. `==` vs `===` vs `Object.is`**

* `Object.is` correctly handles `NaN` and `-0`

```javascript
Object.is(NaN, NaN); // true
```

---

### **25. `preventDefault` vs `stopPropagation`**

* `preventDefault` → stops default browser action
* `stopPropagation` → stops event bubbling

---

### **26. `new` keyword**

**Answer:**
Creates new object, sets prototype, binds `this`, returns object.

---

### **27. JS Module system**

* ES6 → `import/export`
* CommonJS → `require/module.exports`

---

### **28. `slice` vs `splice`**

```javascript
let arr=[1,2,3,4];
arr.slice(1,3); // [2,3] does not mutate
arr.splice(1,2); // [2,3] mutates original
```

---

### **29. Symbols**

```javascript
let sym = Symbol('id');
console.log(typeof sym); // symbol
```

---

### **30. Tricky: setTimeout in a loop**

```javascript
for(var i=0;i<3;i++){ setTimeout(()=>console.log(i),1000); }
// Output: 3,3,3
// Using let instead of var: 0,1,2
```

**Answer:** Because `var` is function-scoped; `let` creates block-scoped variable per iteration.

---

I can also **create a clean “1-page interview-ready PDF”** with **all 30 Q&A + code snippets** so you can revise in **under 1 hour** before any full-stack interview.

Do you want me to prepare that PDF-style cheat sheet?
