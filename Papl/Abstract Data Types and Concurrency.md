
Abstract data types enable us to separate how we use a data structure from the implementation of that data structure.

Concurrency is about running concurrent threads on a computer or computer systems. We will look at typical problems and techniques of solutions:
- Introduction to subprogram-level concurrency
- Types of synchronisation & implementation methods: semaphores & monitors

---

## Concept of Abstraction

Abstraction means separating the top-level usefulness of a thing from the details of its implementation, freeing the programmer from worrying about low-level details.

The idea of abstraction is to promote **readability**, **maintainability**, **reusability**, and **security** of software.

---

## Abstraction Mechanisms

**Data abstraction** (this lecture):
- Nearly all programming languages designed since 1980 support data abstraction.
- Some achieve abstraction by borrowing OO concepts (constructors, accessors, mutators) — e.g., Python, JavaScript, C#.
- Java and C++ provide data abstraction via classes and interfaces.

**Control/process abstraction** via subprograms, functions, or procedures:
- Necessary for achieving program **modularity** — dividing a system into components that can each be designed, implemented, tested, and reused independently.

---

## Data Abstraction

Data abstraction enforces a clear separation between:
- The **abstract properties** (the uses of data) of a data type, and
- The **concrete details** of its implementation.

Data abstraction is achieved by defining **Abstract Data Types (ADTs)** — user-defined data types consisting of:
- A set of data, and
- The necessary operations on that data.

---

## ADTs and Data Structures

An ADT often implements a **data structure** — a representation of data and the operations allowed on it.

**Common ADT examples:**

| ADT | Typical Operations |
|-----|-------------------|
| Stack | push, pop, peek, isEmpty |
| Queue | enqueue, dequeue, front, isEmpty |
| List | add, remove, get, size |
| Set | add, remove, contains, union, intersection |
| Map/Dictionary | put, get, remove, containsKey |

---

## Interface of ADTs

An **interface** is a contract between two parties:
- The **implementer** of the ADT, who is concerned with making operations correct and efficient.
- The **applications programmer**, who just wants to use the ADT to get a job done.

Even if you are both parties, the contract is still essential for good code. This **separation of concerns** is essential in any large project.

---

## Support for ADTs

Many high-level languages (C++, Java, C#, Ada) provide **encapsulation mechanisms** that support data abstraction and provide built-in ADTs.

---

## Designing Your Own ADT

Designing an ADT involves choosing a set of **core operations** for users. Every ADT should provide a way to:
- Add an item
- Remove an item
- Find, retrieve, or access an item

And many non-essential but useful operations, e.g.:
- Check if a collection is empty
- Make a collection empty
- Retrieve a subset of the collection

---

## Implementing an ADT

To implement an ADT, you need to choose a **data representation** and **algorithms**.

**Data representation:**
- An internal storage container holds the items (e.g., an array or linked list).
- Users of the ADT need not know the representation.
- Users should not be allowed to tamper with the representation.
- **Make all data private.**
- If users need access to data, use **accessors** (getters) and **mutators** (setters).

**Algorithms:**
- The logic behind each operation should be encapsulated inside the ADT.
- The same interface can be backed by different algorithms (e.g., a sorted list vs. a hash map for a Set ADT).

---

## Introduction to Concurrency

**Concurrency**: the existence of multiple simultaneously active execution contexts.

Concurrency can occur at different levels:
- **Machine instruction level** — via processor design (e.g., pipelining).
- **Statement level** — statements of high-level languages that support parallel computing.
- **Subprogram level** — a single program has multiple concurrently running subprograms/threads on a single computer.
- **Program level**:
  - Multiple programs run concurrently on a single computer, or
  - A program/application runs on multiple networked computers or on multi-core processors.

---

## Different Names for Concurrency Levels

| Level | Term | Example |
|-------|------|---------|
| Multiple programs on one computer | **Multitasking** | OS scheduler |
| Single program, multiple threads | **Multithreading** | Java threads |
| Program across networked computers | **Distributed computing** | client-server apps |

---

## Subprogram-Level Concurrency

A **task**, **process**, or **thread** is a program unit that can be in concurrent execution with other program units.

A task/process/thread differs from an ordinary subprogram in that:
- A process/task may be **implicitly started**.
- When a multithreaded program starts a thread, **the rest of the program is not necessarily suspended**.
- When a thread's execution is completed, **control may not return to the caller**.

---

## General Categories of Tasks

A task/thread is **disjoint** if it does not communicate with (or affect the execution of) any other tasks in the program.

Otherwise it is a **joint task** and needs to be **synchronised**.

Inter-thread communication is necessary for joint tasks because a thread may need:
- Exclusive access to some resource, or
- To exchange data with another thread.

If not synchronised, joint tasks can lead to **race conditions** or **deadlocks**.

---

## Race Condition

A **race condition** occurs when the resulting value of a variable (or the status of an attribute) depends on the execution order of two or more threads.

**Example:** Two threads both read a shared counter (value = 5), both increment it, and both write back — the result is 6 instead of 7 because the second write overwrites the first.

---

## Deadlock

A **deadlock** is a situation in which two or more competing threads are each waiting for the other to finish, while holding resources the other needs — so neither ever does.

**Example:** Thread A holds resource X and waits for Y. Thread B holds resource Y and waits for X. Neither can proceed.

---

## Necessary Conditions for Deadlock (Coffman Conditions)

For a deadlock to occur, **all four** of the following conditions must hold simultaneously:

1. **Mutual exclusion** — Resources may only be used by one process at a time.
2. **Hold and wait** — A process holds resources while waiting for others held by other processes.
3. **No preemption** — Resources cannot be forcibly removed once granted to a process.
4. **Circular wait** — A circular chain of threads exists where each holds a resource needed by the next.

Deadlock **cannot occur** without the presence of ALL four conditions. Preventing or breaking any one condition prevents deadlock.

---

## Starvation

**Starvation** is related to but distinct from deadlock. A thread suffers starvation when it is perpetually denied access to a resource it needs because other threads are always given priority — even though no circular wait exists.

---

## Task Synchronisation

To remove race conditions and deadlocks, the order of execution of tasks must be **controlled**, i.e., synchronised.

Synchronisation requires communication between tasks, which can be provided by:
- Shared nonlocal variables
- Message passing
- Special data types — **semaphores** & **monitors**

Synchronisation can be **cooperative** or **competitive**, depending on the nature of the shared resources.

---

## Cooperative Synchronisation

**Cooperative synchronisation** ensures two or more tasks work together to avoid deadlock — one task must wait for another to finish before it can proceed.

Best illustrated by the **producer-consumer problem**:
- A **producer** task generates data and places it in a shared buffer.
- A **consumer** task reads and processes data from the buffer.
- The consumer must wait if the buffer is empty; the producer must wait if the buffer is full.

---

## Competitive Synchronisation

**Competitive synchronisation** ensures **exclusive access** to a critical resource by a single task at any one time — to avoid race conditions.

**Critical section**: the section of code that accesses the shared resource.

Examples: a shared counter, a bank account — simultaneous access by multiple threads must never happen.

---

## Synchronisation Implementation

Synchronisation (cooperative or competitive) can be implemented using special data structures called **semaphores** and **monitors**:
- **Semaphores** can implement both cooperative and competitive synchronisation.
- **Monitors** wrap resources with a built-in mechanism for exclusive access control, used for competitive synchronisation.

---

## Semaphores

A **semaphore** is a data structure consisting of:
- A **counter** (integer) tracking the units of available resources (e.g., starts at 10).
- A **queue** storing processes waiting for access to the resource.
- Two operations: **wait()** (also called P or down) and **signal()** (also called V, release, or up).

Processes must access shared resources only through these two operations.

### Types of Semaphores

- **Binary semaphore (mutex)**: counter is 0 or 1; used for mutual exclusion (competitive synchronisation).
- **Counting semaphore**: counter can be any non-negative integer; used to manage a pool of resources (cooperative synchronisation).

### Request — Calling wait()

When a process needs access to a guarded resource, it calls `wait()`:
1. Decrements the counter by 1.
2. If the counter is **≥ 0** → access is granted; the process is placed on the ready list.
3. If the counter is **< 0** → the process is blocked and added to the semaphore's waiting queue.

### Release — Calling signal()

When a process finishes using a resource, it calls `signal()`:
1. Increments the counter by 1.
2. If the counter is **≤ 0** (threads are waiting) → transfers one blocked thread from the waiting queue to the ready list.

---

## Monitors

A **monitor** is an object that encapsulates shared data/resources and guarantees that **at most one thread may access the shared data at any point in time**. This is the monitor's **mutual exclusion property**.

Monitors implement **competitive synchronisation**.

### Implementation of Monitors

Mutual exclusion is achieved by equipping an object with a **private lock**:
- The lock is initially **unlocked**.
- The lock is **acquired** at the start of each public method call.
- The lock is **released** on return from each public method call.

This ensures no two threads can be executing the object's methods simultaneously.

Monitors are used for synchronisation control in Java, C#, Python, concurrent Pascal, Ada, and others.

### Condition Variables (inside monitors)

Monitors also support **condition variables** to allow threads to wait inside the monitor without holding the lock:
- **wait(condition)** — releases the lock and suspends the thread until the condition is signalled.
- **signal(condition)** — wakes up one thread waiting on the condition.

This allows cooperative synchronisation within the mutual exclusion framework of the monitor.

### Semaphores vs Monitors

| Feature | Semaphore | Monitor |
|---------|-----------|---------|
| Access control | Explicit wait/signal calls | Automatic via lock |
| Risk of misuse | High (programmer must call correctly) | Low (encapsulated) |
| Use case | Both cooperative & competitive | Primarily competitive |
| Abstraction level | Low-level | Higher-level |
