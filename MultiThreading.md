
Sure! Let's break it down with a Java example to explain the concept of **processes** and how **multiple threads** can run within a single process.

### **What is a Process?**

A **process** is an instance of a program that is in execution. Each process has its own memory space and resources, like file handles and memory, independent of other processes. When you run a Java program, the Java Virtual Machine (JVM) itself runs as a process, and the code inside that JVM can create multiple threads within that process.

### **Example: Running Multiple Threads in a Single Process**

Let’s create a simple Java program that demonstrates a single process (the JVM) running multiple threads.

#### **Code Example**:

```java
class MyTask implements Runnable {
    private String taskName;

    public MyTask(String taskName) {
        this.taskName = taskName;
    }

    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(taskName + " - iteration " + i);
            try {
                Thread.sleep(1000);  // Simulate some work with a 1-second delay
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ProcessAndThreadsDemo {
    public static void main(String[] args) {
        // Creating two threads that will run within the same process
        Thread thread1 = new Thread(new MyTask("Thread 1"));
        Thread thread2 = new Thread(new MyTask("Thread 2"));

        // Starting the threads
        thread1.start();
        thread2.start();

        // Main thread work (This is the process's main thread)
        for (int i = 0; i < 5; i++) {
            System.out.println("Main thread - iteration " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

#### **Explanation**:

- **Main Process**: When you run the `ProcessAndThreadsDemo` program, the JVM starts as a process. This process contains all the code and resources required by your program.

- **Main Thread**: The code inside the `main()` method is the primary thread (also known as the "main thread") of this process.

- **Multiple Threads**: Inside the same process, we create two additional threads: `thread1` and `thread2`. Both are running concurrently and performing some task (printing a message and sleeping for 1 second). These threads share the same memory space as the main thread because they are part of the same process.

- **Thread Sleep**: The `Thread.sleep(1000)` method pauses each thread for 1 second, simulating some "work" being done by each thread.

- **Concurrency**: Even though all three threads are running concurrently, they are still part of the same process. They share the process's resources like memory, but they execute independently of each other.

### **Output Example**:

```
Main thread - iteration 0
Thread 1 - iteration 0
Thread 2 - iteration 0
Main thread - iteration 1
Thread 1 - iteration 1
Thread 2 - iteration 1
Main thread - iteration 2
Thread 1 - iteration 2
Thread 2 - iteration 2
...
```

Here you can see all three threads executing concurrently. The "Main thread" and the two additional threads (`Thread 1` and `Thread 2`) are working simultaneously, within the same process (the JVM).

### **Key Points**:

- **Process**: The JVM represents the process that runs this program.
- **Threads**: Inside the JVM process, multiple threads (`thread1`, `thread2`, and the main thread) are running concurrently.
- **Shared Memory**: All threads in the same process share memory and resources, which is why multithreading needs to be managed carefully to avoid issues like race conditions.

This example illustrates how a process (the JVM) can run multiple threads, each performing different tasks but sharing the same process resources.


Let’s go through each concept step by step with simple definitions, examples, and best practices to help you prepare for your multithreading interview in Java.

---

### **1. What is a Thread?**
- A **thread** is a lightweight sub-process, the smallest unit of processing. It is a separate path of execution within a program that allows multiple tasks to run concurrently.

### **2. What is a Process?**
- A **process** is an instance of a program in execution. Each process runs independently and has its own memory space. A process can contain multiple threads.

### **3. Difference Between Thread and Process**:
- **Process**:
    - Independent memory space.
    - More expensive to create and manage.
    - Runs separately from other processes.

- **Thread**:
    - Shares memory within the process.
    - Cheaper and faster to create.
    - Multiple threads can run concurrently in the same process.

---

### **4. Creating Threads in Java**

#### **A. Using `Thread` Class**

You can create a thread by extending the `Thread` class.

**Example**:
```java
class MyThread extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread 1 - Count: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();  // Starts the thread
    }
}
```

#### **B. Using `Runnable` Interface**

You can also create threads by implementing the `Runnable` interface.

**Example**:
```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Runnable 1 - Count: " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();  // Starts the thread
    }
}
```

---

### **5. Thread Lifecycle**

A thread in Java goes through the following lifecycle states:

1. **New**: The thread is created but not yet started.
2. **Runnable**: The thread is ready to run after calling `start()`, but it may not be running yet.
3. **Running**: The thread is actively executing its task.
4. **Blocked/Waiting**: The thread is inactive, waiting for resources or for a condition to be met.
5. **Terminated**: The thread has finished execution.

#### **Thread Lifecycle Diagram**:
```
        +-----------+  
        |   New     |  
        +-----+-----+  
              |  
          start()  
              v  
        +-----------+  
        | Runnable  |  
        +-----+-----+  
              |  
           Running  
              v  
+---------+  +---+  +------------+  
| Blocked |<-+    ->| Terminated |  
+---------+         +------------+
```

---

### **6. Thread Safety**

- **Thread safety** ensures that shared resources (variables, collections, etc.) are accessed correctly by multiple threads to avoid data inconsistency or corruption.
- **“Thread safety** means that a piece of code or resource behaves correctly when accessed by multiple threads at the same time, without causing data inconsistency or unexpected results.”

In simple words:
👉 When multiple threads access shared data, it should not corrupt the data.
#### **Ways to Achieve Thread Safety**:
1. **Synchronized Methods/Blocks**: Ensures only one thread can access the block/method at a time.
2. **Locks (`ReentrantLock`)**: Provides more control over synchronization.
3. **Atomic Variables (`AtomicInteger`)**: Provides thread-safe operations on variables without locking.

**Example of Synchronized Block**:
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

---

### **7. When to Make a Class, Method, or Block Thread-Safe**
- **Class**: If the class contains shared data accessed by multiple threads.
- **Method**: If the method modifies shared data and can be called by multiple threads.
- **Block**: If only a small section of code modifies shared data, synchronize only that block for better performance.

---

### **8. Thread Communication**

Threads communicate by using methods like `wait()`, `notify()`, and `notifyAll()`.

**Example**:
```java
class SharedResource {
    public synchronized void produce() throws InterruptedException {
        wait();  // Wait for notification
        System.out.println("Resumed production!");
    }

    public synchronized void consume() {
        notify();  // Notify waiting threads
        System.out.println("Consuming...");
    }
}

public class Main {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        new Thread(() -> {
            try {
                resource.produce();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();

        new Thread(() -> {
            resource.consume();
        }).start();
    }
}
```

---

### **9. Java Programs That Use Threads Internally**
- **Garbage Collection**: Runs in a separate thread.
- **Swing UI**: Uses the Event Dispatch Thread (EDT).
- **Scheduled Executors**: Use threads to schedule tasks.

---

### **10. Daemon Threads**

- **Daemon Threads**: These are background threads that run behind the scenes and are terminated by the JVM when all user threads (non-daemon threads) finish execution.

**Example**:
```java
class MyDaemonThread extends Thread {
    public void run() {
        while (true) {
            System.out.println("Daemon thread running...");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyDaemonThread daemonThread = new MyDaemonThread();
        daemonThread.setDaemon(true);  // Set thread as daemon
        daemonThread.start();

        System.out.println("Main thread finished.");
    }
}
```

---

### **11. Giving a Name to a Thread**
You can name threads to help with debugging and management.

**Example**:
```java
Thread t = new Thread(() -> System.out.println("Thread running"));
t.setName("MyThread");
t.start();
System.out.println("Thread name: " + t.getName());
```

---

### **12. Thread Priority**

Threads have priority levels ranging from 1 (lowest) to 10 (highest). The JVM uses these priority levels to decide the order of thread execution.

**Example**:
```java
class MyThread extends Thread {
    public void run() {
        System.out.println(Thread.currentThread().getName() + " is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setPriority(Thread.MIN_PRIORITY);  // Set priority to 1
        t2.setPriority(Thread.MAX_PRIORITY);  // Set priority to 10

        t1.start();
        t2.start();
    }
}
```

---

### **Summary**
- **Thread**: A unit of execution within a process.
- **Process**: An instance of a program with its own memory space.
- **Thread Lifecycle**: Understand the various states a thread can be in.
- **Thread Safety**: Use synchronization, locks, or atomic variables to manage thread safety.
- **Daemon Threads**: Background threads that terminate when all user threads finish.
- **Thread Communication**: Use `wait()`, `notify()`, and `notifyAll()` for thread coordination.
- **Thread Naming and Priority**: Use to manage and debug threads effectively.

With these concepts and examples, you should be well-prepared for multithreading interview questions!

Perfect! Let’s go **step by step**, question by question. I’ll provide **the question, a concise answer, and exactly how you can say it in an interview**.

---

## **1️⃣ What is a thread and what are the different stages in its life cycle?**

**Answer:**

> “A **thread** is a lightweight unit of execution within a program. Every Java program has a main thread, and we can create additional threads for concurrent execution.
> The thread life cycle has these stages:
>
> 1. **New (Created)** – Thread object is created.
> 2. **Runnable** – Ready to run; waiting for CPU.
> 3. **Running** – Thread is executing.
> 4. **Waiting/Blocked** – Thread waits for resource or condition.
> 5. **Terminated/Dead** – Thread execution is completed.”

**Interview Tip:**

> “You can imagine it as a worker in a factory: created, waiting for a task, performing the task, paused if needed, and finally done.”

---

## **2️⃣ What is the difference between process and thread?**

**Answer:**

| Feature       | Process                            | Thread                                           |
| ------------- | ---------------------------------- | ------------------------------------------------ |
| Memory        | Own memory space                   | Shares memory with other threads in same process |
| Creation      | Heavyweight                        | Lightweight                                      |
| Communication | Inter-process communication needed | Directly via shared memory                       |
| Overhead      | High                               | Low                                              |

**Interview Tip:**

> “A process is like a separate program running on your computer, while a thread is like a worker inside a process sharing resources with other threads.”

---

## **3️⃣ What are the different types of thread priorities available in Java?**

**Answer:**

> “Java threads have **priorities from 1 to 10**:
>
> * `Thread.MIN_PRIORITY = 1`
> * `Thread.NORM_PRIORITY = 5`
> * `Thread.MAX_PRIORITY = 10`
>   Higher priority threads are more likely to get CPU time, but scheduling is not guaranteed.”

**Interview Tip:**

> “It’s like telling a scheduler which tasks are more important, but JVM decides actual execution.”

---

## **4️⃣ What is context switching in Java?**

**Answer:**

> “**Context switching** happens when the CPU switches from one thread or process to another.
> It saves the current thread’s state and loads the next thread’s state.
> Frequent context switching can reduce performance.”

**Interview Tip:**

> “Think of it as a CPU multitasking between workers; switching too often slows things down.”

---

## **5️⃣ What is the difference between user threads and daemon threads?**

**Answer:**

| Feature      | User Thread                          | Daemon Thread                           |
| ------------ | ------------------------------------ | --------------------------------------- |
| Purpose      | Performs application tasks           | Background service tasks                |
| JVM behavior | JVM waits for user threads to finish | JVM exits if only daemon threads remain |
| Example      | Main application threads             | Garbage collector, background logger    |

**Interview Tip:**

> “User threads keep the program alive; daemon threads run in background and don’t prevent JVM exit.”

---

## **6️⃣ What is synchronization?**

**Answer:**

> “**Synchronization** is used to control access to shared resources by multiple threads.
> It ensures only one thread at a time can execute a synchronized block or method, preventing race conditions.”

**Interview Tip:**

> “Imagine only one person can withdraw money from an ATM at a time — that’s synchronization.”

---

## **7️⃣ What is deadlock?**

**Answer:**

> “A **deadlock** occurs when two or more threads wait for each other’s locks indefinitely, so none can proceed.
> It usually happens when multiple threads acquire multiple locks in different orders.”

**Interview Tip:**

> “It’s like two people each holding one chopstick and waiting for the other — neither can eat.”

---

## **8️⃣ What is the use of the `wait()` and `notify()` methods?**

**Answer:**

> “`wait()` makes a thread **release the lock and wait** for a condition, `notify()` **wakes one waiting thread**, and `notifyAll()` wakes all waiting threads.
> They are used for **inter-thread communication** inside synchronized blocks.”

**Interview Tip:**

> “If a thread is waiting for a resource, `wait()` pauses it until another thread signals with `notify()`.”

---

## **9️⃣ What is the difference between thread and process in Java?**

**Answer:** *(Similar to Q2, but more concise)*

> “A **process** is independent with its own memory; a **thread** is lightweight and shares memory with other threads in the same process. Threads are used for **parallel execution inside a process**.”

---

## **🔟 What is the difference between `synchronized` and `volatile` in Java?**

**Answer:**

| Feature     | Synchronized                  | Volatile            |
| ----------- | ----------------------------- | ------------------- |
| Purpose     | Mutual exclusion + visibility | Visibility only     |
| Lock        | Yes, acquires lock            | No lock             |
| Usage       | Methods or blocks             | Variables only      |
| Performance | Slower due to locking         | Faster, no blocking |

**Interview Tip:**

> “Use `synchronized` when you need **both atomicity and visibility**, and `volatile` when you only need **visibility across threads**.”

---

## **11️⃣ What is the purpose of `sleep()` method in Java?**

**Answer:**

> “`sleep()` pauses the thread for a specified time without releasing the lock.
> Useful to **simulate delay or wait between executions**.”

**Interview Tip:**

> “Think of it as a worker taking a short break without letting others interfere with its current task.”

---

## **12️⃣ What is the difference between `wait()` and `sleep()`?**

| Feature                  | wait()                          | sleep()               |
| ------------------------ | ------------------------------- | --------------------- |
| Class                    | Object                          | Thread                |
| Lock                     | Releases lock                   | Does not release lock |
| Purpose                  | Wait for condition/notification | Pause thread for time |
| Must be in synchronized? | ✅                               | ❌                     |

**Interview Tip:**

> “`wait()` is for inter-thread communication, `sleep()` is just a timed pause.”

---

## **13️⃣ What is the difference between `notify()` and `notifyAll()`?**

| Feature     | notify()                       | notifyAll()                         |
| ----------- | ------------------------------ | ----------------------------------- |
| Wakes       | One waiting thread             | All waiting threads                 |
| Use         | Faster if one thread is enough | Use if multiple threads can proceed |
| Requirement | Inside synchronized block      | Inside synchronized block           |

**Interview Tip:**

> “Use `notify()` when only one thread can proceed, `notifyAll()` when all waiting threads may continue.”

Absolutely! Here’s a **top 15 multi-threading interview question list** with **concise answers and exactly how you can say it confidently in an interview**. I’ve structured it to be **easy to remember and senior-level**.

---

# **Top 15 Multi-threading Questions in Java**

---

### **1️⃣ What is a thread in Java?**

**Answer:**

> “A thread is a lightweight unit of execution in a program. Every Java program has a main thread by default, and we can create additional threads to perform tasks concurrently.”

**Interview tip:** Use analogy: “Like multiple workers in a factory, each doing a task simultaneously.”

---

### **2️⃣ How can you create a thread in Java?**

**Answer:**

> “Two ways:
>
> 1. **Extend `Thread` class** and override `run()` method.
> 2. **Implement `Runnable` interface** and pass it to a `Thread` object.
>    We call `start()` to begin execution.”

**Tip:** Mention `Runnable` is preferred when class already extends another class.

---

### **3️⃣ Difference between `start()` and `run()`**

**Answer:**

> “`start()` creates a new thread and calls `run()` internally.
> `run()` just executes the method in the current thread, no new thread is created.”

---

### **4️⃣ What is the difference between `Runnable` and `Callable`?**

**Answer:**

> “`Runnable` does not return a result and cannot throw checked exceptions.
> `Callable` returns a result and can throw exceptions, often used with ExecutorService.”

---

### **5️⃣ What is Thread Lifecycle?**

**Answer:**

> “A thread goes through these states:
> **New → Runnable → Running → Waiting/Blocked → Terminated**.
> JVM scheduler moves threads between states based on availability.”

---

### **6️⃣ What is `synchronized` keyword?**

**Answer:**

> “`synchronized` ensures **only one thread at a time** can access a block or method, preventing race conditions and data inconsistency.”

---

### **7️⃣ What is a deadlock? How can it occur?**

**Answer:**

> “Deadlock occurs when **two or more threads wait for each other’s locks indefinitely**, so none can proceed.
> Usually happens when multiple threads acquire multiple locks in different orders.”

---

### **8️⃣ Difference between `wait()`, `notify()`, and `notifyAll()`**

**Answer:**

> * `wait()` → thread waits and releases lock
> * `notify()` → wakes **one waiting thread**
> * `notifyAll()` → wakes **all waiting threads**

**Tip:** Mention these are used for **inter-thread communication** inside synchronized blocks.

---

### **9️⃣ Difference between `volatile` and `synchronized`**

**Answer:**

> “`volatile` ensures visibility of a variable across threads.
> `synchronized` ensures **mutual exclusion** and **visibility** for a block or method.”

---

### **🔟 What is `ExecutorService`?**

**Answer:**

> “`ExecutorService` is a **high-level API** to manage thread pools, submit tasks, and control execution instead of manually creating threads.”

---

### **11️⃣ Difference between `Thread` and `Process`**

**Answer:**

> “A **process** is an independent program with its own memory.
> A **thread** is a lightweight execution unit **within a process** sharing memory with other threads.”

---

### **12️⃣ What is Thread Priority?**

**Answer:**

> “Thread priority (1–10) tells JVM scheduler which thread is more important.
> Higher priority threads are likely to execute before lower priority threads, but it’s **not guaranteed**.”

---

### **13️⃣ What is Thread-safe?**

**Answer:**

> “A class or method is **thread-safe** if multiple threads can access it **concurrently without corrupting data**.
> We achieve it using `synchronized`, locks, or concurrent collections.”

---

### **14️⃣ Difference between `sleep()` and `wait()`**

**Answer:**

| Feature        | `sleep()`    | `wait()`           |
| -------------- | ------------ | ------------------ |
| Belongs to     | Thread class | Object class       |
| Releases lock  | ❌            | ✅                  |
| Purpose        | Pause thread | Wait for condition |
| Requires sync? | ❌            | ✅                  |

---

### **15️⃣ What is a race condition?**

**Answer:**

> “A race condition occurs when multiple threads **access shared data simultaneously** and the **final result depends on the order of execution**.
> We prevent it using `synchronized` or locks.”

---




---

# ✅ What is Synchronization in Java?

### 🔹 Simple Definition

> Synchronization is a mechanism to **control multiple threads accessing a shared resource**, so that only **one thread can access it at a time**.

It helps to prevent:

* Race condition
* Data inconsistency
* Unexpected output

---

# ✅ Why We Need Synchronization?

When:

* Multiple threads access the **same object**
* And at least one thread **modifies data**

Without synchronization → Data becomes inconsistent.

---

# ✅ Example Without Synchronization (Problem)

```java
class Counter {

    int count = 0;  // Shared variable

    public void increment() {

        count++;  // Not thread-safe
    }
}
```

If two threads run this method simultaneously:

* Both read count = 0
* Both increment to 1
* Final result = 1 ❌ (wrong)
* Expected = 2

This is called **Race Condition**.

---

# ✅ With Synchronization (Solution)

```java
class Counter {

    int count = 0;

    // Only one thread can execute this at a time
    public synchronized void increment() {

        count++;
    }
}
```

Now:

* One thread gets lock
* Other thread waits
* Data becomes safe ✅

---

# ✅ When Do We Use Synchronization?

Use synchronization when:

1. Multiple threads share same object
2. Shared data is being modified
3. We want thread safety

Example:

* Banking transaction
* Inventory update
* Order processing
* Counter increment
* Logging system

---

# ✅ Types of Synchronization

1. **Method Level**

```java
public synchronized void methodName() { }
```

2. **Block Level**

```java
synchronized(this) {
   // critical section
}
```

3. **Static Synchronization**

```java
public static synchronized void methodName() { }
```

---

# ✅ Important Interview Line

> “Synchronization uses intrinsic lock (monitor lock). When a thread enters a synchronized method or block, it acquires the object's lock, and other threads must wait until the lock is released.”

---

# ✅ 30-Second Perfect Interview Answer

You can say this confidently:

> “Synchronization in Java is used to control multiple threads accessing a shared resource. It ensures that only one thread executes the critical section at a time to prevent race conditions and data inconsistency. It is mainly used when multiple threads modify shared data. Internally, it works using object-level locking.”

---

# ✅ Bonus: Senior-Level Add-On Line

If interviewer asks deeper:

> “However, excessive synchronization may reduce performance, so in real-time applications we prefer Concurrent classes like ConcurrentHashMap or use ReentrantLock for better control.”

---
>"“In Java, synchronization works using an intrinsic monitor lock associated with every object. When a thread enters a synchronized block, it tries to acquire the object’s monitor. If the lock is free, it executes the critical section. If not, the thread moves to BLOCKED state until the lock is released. Internally, the JVM maintains a monitor structure that tracks the owning thread and waiting threads. Synchronization in Java is also reentrant, meaning the same thread can acquire the same lock multiple times.”

Good 👍 This is a very common basic multi-threading question.

Let me explain **volatile** clearly and how to say it in an interview.

---

# ✅ What is `volatile` in Java?

> `volatile` is a keyword used to make a variable’s value always read from and written to **main memory**, not from a thread’s local cache.

It is mainly used in **multi-threading** to ensure **visibility of changes across threads**.

---

# ✅ Why Do We Need `volatile`?

In multithreading:

Each thread has:

* **Main Memory (Heap)**
* **Thread Local Memory (CPU cache)**

Without volatile:

* Thread A updates a variable.
* Thread B may still read the old value from its cache.

This causes inconsistency.

With volatile:

* Any change made by one thread is immediately visible to all other threads.

---

# ✅ Simple Example

```java
class Test {

    volatile boolean running = true;  // Volatile variable

    public void stop() {
        running = false;  // Change will be visible to all threads
    }
}
```

If one thread sets `running = false`,
other threads will immediately see the updated value.

---

# ❗ Important Point

👉 `volatile` provides:

* ✅ Visibility
* ❌ NOT atomicity
* ❌ NO locking

---

# ❌ Where Volatile Fails

```java
volatile int count = 0;

count++;  // Not thread-safe
```

Because `count++` is 3 steps:

1. Read
2. Increment
3. Write

Multiple threads → race condition still possible.

So volatile is only good for:

* Flags
* Status variables
* Configuration updates

---

# ✅ 20-Second Interview Answer

You can say:

> “Volatile is a keyword in Java used to ensure visibility of a variable across multiple threads. It guarantees that any update made by one thread is immediately visible to other threads. However, it does not provide mutual exclusion or atomicity.”




Perfect 👍 Since you prefer **Java code with comments on every line (for interview explanation)**, I’ll give you **frequently asked multi-threading coding questions** with **clean Java code + explanation style**.

These are very commonly asked in 3+ years Java interviews.

---

# ✅ 1️⃣ Create a Thread using Thread class

### ❓ Interview Question:

Write a Java program to create a thread using the `Thread` class.

```java
// Create a class that extends Thread
class MyThread extends Thread {

    // Override run() method (this contains thread logic)
    public void run() {

        // Print message 5 times
        for (int i = 1; i <= 5; i++) {

            // Print current thread name and count
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}

// Main class
public class ThreadExample1 {

    public static void main(String[] args) {

        // Create thread object
        MyThread t1 = new MyThread();

        // Start thread (internally calls run())
        t1.start();
    }
}
```

### 🗣 How to say in interview:

> “Here I am extending the Thread class and overriding run() method. When I call start(), JVM creates a new thread and executes run().”

---

# ✅ 2️⃣ Create Thread using Runnable Interface (Most Preferred)

### ❓ Interview Question:

Write a program using Runnable interface.

```java
// Create class that implements Runnable
class MyRunnable implements Runnable {

    // Override run() method
    public void run() {

        // Loop 5 times
        for (int i = 1; i <= 5; i++) {

            // Print thread name and value
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}

public class ThreadExample2 {

    public static void main(String[] args) {

        // Create Runnable object
        MyRunnable task = new MyRunnable();

        // Pass runnable object to Thread constructor
        Thread t1 = new Thread(task);

        // Start thread
        t1.start();
    }
}
```

### 🗣 Interview Tip:

> “Runnable is preferred because Java does not support multiple inheritance, so extending Thread limits flexibility.”

---

# ✅ 3️⃣ Synchronization Example (Prevent Race Condition)

### ❓ Interview Question:

Write a program where two threads increment a shared counter safely.

```java
// Shared resource class
class Counter {

    int count = 0;  // Shared variable

    // Synchronized method to avoid race condition
    public synchronized void increment() {

        count++;  // Increase counter safely
    }
}

public class SyncExample {

    public static void main(String[] args) throws InterruptedException {

        // Create shared counter object
        Counter counter = new Counter();

        // Create first thread
        Thread t1 = new Thread(() -> {

            for (int i = 0; i < 1000; i++) {

                counter.increment();  // Call synchronized method
            }
        });

        // Create second thread
        Thread t2 = new Thread(() -> {

            for (int i = 0; i < 1000; i++) {

                counter.increment();
            }
        });

        // Start both threads
        t1.start();
        t2.start();

        // Wait for threads to finish
        t1.join();
        t2.join();

        // Print final count
        System.out.println("Final Count: " + counter.count);
    }
}
```

### 🗣 Interview Tip:

> “Without synchronized, race condition may occur and final count will not be accurate.”

---

# ✅ 4️⃣ Producer-Consumer Problem (Using wait() and notify())

### ❓ Interview Question:

Implement Producer-Consumer using wait and notify.

```java
// Shared resource class
class SharedBuffer {

    private int data;           // Data variable
    private boolean hasData = false;  // Flag to check availability

    // Produce method
    public synchronized void produce(int value) throws InterruptedException {

        // Wait if data already exists
        while (hasData) {

            wait();  // Release lock and wait
        }

        data = value;  // Set data
        hasData = true; // Mark data available

        System.out.println("Produced: " + value);

        notify();  // Notify consumer
    }

    // Consume method
    public synchronized int consume() throws InterruptedException {

        // Wait if no data available
        while (!hasData) {

            wait();  // Release lock and wait
        }

        hasData = false;  // Mark data consumed

        System.out.println("Consumed: " + data);

        notify();  // Notify producer

        return data;
    }
}
```

---

# ✅ 5️⃣ Deadlock Example (Very Frequently Asked)

### ❓ Interview Question:

Write a program that causes deadlock.

```java
public class DeadlockExample {

    public static void main(String[] args) {

        // Create two lock objects
        final Object lock1 = new Object();
        final Object lock2 = new Object();

        // Thread 1
        Thread t1 = new Thread(() -> {

            synchronized (lock1) {  // Acquire lock1

                System.out.println("Thread 1 acquired lock1");

                synchronized (lock2) {  // Try to acquire lock2

                    System.out.println("Thread 1 acquired lock2");
                }
            }
        });

        // Thread 2
        Thread t2 = new Thread(() -> {

            synchronized (lock2) {  // Acquire lock2

                System.out.println("Thread 2 acquired lock2");

                synchronized (lock1) {  // Try to acquire lock1

                    System.out.println("Thread 2 acquired lock1");
                }
            }
        });

        t1.start();
        t2.start();
    }
}
```

### 🗣 Interview Tip:

> “Deadlock occurs because threads acquire locks in different order.”

---

# ✅ 6️⃣ ExecutorService Example (Modern Approach – Important for 3+ years)

### ❓ Interview Question:

How to create thread pool?

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ExecutorExample {

    public static void main(String[] args) {

        // Create thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Submit 5 tasks
        for (int i = 1; i <= 5; i++) {

            int taskId = i;

            executor.submit(() -> {

                System.out.println("Executing Task " + taskId +
                        " by " + Thread.currentThread().getName());
            });
        }

        // Shutdown executor
        executor.shutdown();
    }
}
```

### 🗣 Interview Tip:

> “In real-time projects, we use ExecutorService instead of manually creating threads.”

---

# 🔥 Most Important Coding Topics for 3+ Years

You should definitely prepare:

1. Thread creation (Thread & Runnable)
2. Synchronization
3. wait() / notify()
4. Deadlock
5. Volatile
6. ThreadPool (ExecutorService)
7. Callable & Future
8. ConcurrentHashMap
9. CountDownLatch
10. ReentrantLock


