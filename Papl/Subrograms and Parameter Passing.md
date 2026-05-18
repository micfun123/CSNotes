# Lecture 16: Subprograms and Parameter Passing

---

## 1. Introduction

Subprograms are the fundamental building blocks of programs and among the most important concepts of language design — they facilitate flow control at the program level.

This lecture covers:

- Pass by value
- Pass by result
- Pass by value-result
- Pass by reference

---

## 2. What is a Subprogram?

Decomposing a problem into smaller sub-problems makes complexity more manageable. All modern languages support this through **subprograms**, **procedures**, or **functions**.

A **subprogram** is a piece of code that:

- Is identified by a **name**
- Has its own **local reference environment**
- Exchanges information with the rest of the program via **parameters**

> **Note:** Both procedures and functions are subprograms. A _function_ has a return value; a _procedure_ does not.

---

## 3. Functions and Abstraction

Subprograms provide two fundamental abstraction facilities:

### Process / Control Abstraction

- Hides procedural details from the caller
- Programmers only need to know the **interface**, not the implementation
- Example: `sort(var anArray : ArrayOfInt)` — you don't need to know _how_ it sorts to use it

### Data Abstraction

- Allows use of sophisticated data types without knowing their implementation
- Promotes reusability and maintainability
- _(Covered in a separate lecture)_

---

## 4. Key Terminology

|Term|Definition|
|---|---|
|**Function definition**|The full implementation: header + body|
|**Function header**|Name, return type, and formal parameters|
|**Parameter profile**|The number, order, and types of parameters — e.g. `(int n, int a)`|
|**Function call**|An explicit request to execute the function — e.g. `y = foo(3, 0)`|
|**Function declaration / prototype**|The header only, without the body (used in C/C++)|
|**Formal parameter**|A dummy variable listed in the function header|
|**Actual parameter**|The real value or address passed at the call site|

### Example

```c
int foo (int n, int a) {      // ← function header
    int temp = a;             //
    if (temp == 0) return n;  // ← function body
    else return n + 1;        //
}
```

---

## 5. Function Declarations and Header Files (C/C++)

A **prototype** declares the function's interface without the body:

```c
int sum (int, int);   // prototype — parameter names can be omitted
```

Prototypes are usually placed in **header files** (`.h`) which are `#include`-d wherever the function is used. The actual implementation lives in a separate source file or library.

---

## 6. Parameter Binding

There are two ways to bind actual parameters to formal parameters:

### By Position (most common)

Parameters are matched by their order of appearance.

```c
x = foo(3, 0);  // 3 → n, 0 → a
```

Safe and effective; used in C, C++, Java, etc.

### By Keyword

Parameter names are used explicitly. Used in Python:

```python
func(value=my_value, array=my_array)
func(array=my_array, value=my_value)  # same result
```

- **Advantage:** Parameters can appear in any order
- **Disadvantage:** Caller must remember formal parameter names

---

## 7. Local Referencing Environments

When a function is called, a **local referencing environment** is created for all its local variables.

- In most modern languages, local variables are **stack-dynamic** — created on the stack on demand, supporting recursion naturally
- Local variables can be declared **`static`** (in C/C++) if their values need to persist between calls

---

## 8. Parameter Passing Methods

The relationship between actual and formal parameters follows one of three **semantic models**:

|Mode|Direction|Implementation|
|---|---|---|
|**In**|Caller → Function|Pass by value|
|**Out**|Function → Caller|Pass by result|
|**Inout**|Both directions|Pass by value-result _or_ pass by reference|

---

## 9. Pass by Value (In Mode)

The value of the actual parameter is **copied** to the formal parameter at the point of the call.

```c
void foo (int x) {
    x = x + 1;
}

int y = 1;
foo(y + 1);  // x starts as 2, becomes 3 inside foo; y is unchanged
```

### Characteristics

- Formal and actual parameters are **isolated** — changes inside the function don't affect the caller
- Simple and fast for small scalar types (bool, char, int, float, ...)
- **Default** in C, C++, Java, and Pascal
- **Disadvantage:** Requires extra storage (value stored twice); costly for large data

---

## 10. Pass by Result (Out Mode)

No value is passed _into_ the function. The formal parameter acts as a local variable, and its final value is **copied back** to the actual parameter when the function returns.

```c
void foo (result int x) {
    x = 8;
}

int y = 1;
foo(y);  // y becomes 8 after the call
```

### Characteristics

- Actual parameters **must be variables** (not literals or expressions)
- **Potential problem — order of copying:** if the same variable is passed twice, the result depends on the implementation:

```csharp
void myMethod(out int x, out int y) { x = 15; y = 30; }
someObj.myMethod(out a, out a);  // a could be 15 or 30 — undefined!
```

---

## 11. Pass by Value-Result (Inout Mode)

Also called **pass-by-copy**. A combination of pass-by-value and pass-by-result:

1. At the **point of call**, the actual parameter's value is copied to the formal parameter
2. At the **end of the call**, the formal parameter's value is copied back to the actual parameter

```c
void foo (valueresult int x) { x = x + 1; }

int y = 8;
foo(y);  // y becomes 9 after the call
```

Facilitates **bi-directional** data exchange while keeping formal and actual parameters **isolated** during execution.

---

## 12. Pass by Reference (Inout Mode)

Instead of copying a value, an **access path (address)** is passed. The formal parameter and actual parameter become **two names for the same memory location**.

```c
void foo (reference int x) { x = x + 1; }

int y = 0;
foo(y);  // During execution, x IS y. After the call, y = 1.
```

### Characteristics

- **Advantage:** Efficient — no copying, no duplicate storage
- **Disadvantages:**
    - No separation between formal and actual parameters (side effects possible)
    - Parameter access may be slower (requires pointer indirection)
- Considered a low-level operation; **excluded from Java, and not the default in C/C++**

---

## 13. Simulating Pass by Reference

### In C (using pointers)

C only supports pass-by-value natively, but reference-like behaviour is achieved with pointers:

```c
void swap (int *a, int *b) {
    int tmp = *a;  *a = *b;  *b = tmp;
}

swap(&v1, &v2);  // pass addresses; * dereferences inside the function
```

### In Java (using objects)

Java passes object _references_ by value — modifying the object's fields affects the original:

```java
void swap (A a, A b) {
    int tmp = a.v;  a.v = b.v;  b.v = tmp;
}
// Appears to be by-value but is effectively by-reference for objects
```

---

## 14. Parameter Passing in Major Languages

|Language|Default|Pass by Reference|
|---|---|---|
|**C**|By value|Simulate with pointers (`*`, `&`)|
|**C++**|By value|`&` for reference; `const &` for constant-reference (no copy, read-only)|
|**Java**|By value|Objects passed by reference automatically|
|**C#**|By value|Use `ref` on both formal and actual parameter; `out` for out-mode|
|**PHP**|By value|Prefix formal parameter with `&`|
|**Fortran 95+**|—|Declare with `in`, `out`, or `inout`|
|**Ada**|`in` (default)|Declare with `in`, `out`, or `in out`|

### C++ Example

```cpp
void f( int a, int &b, const int &c );
//       ↑ value  ↑ reference  ↑ constant-reference
```

---

## 15. Summary

```
┌─────────────────┬────────────┬────────────────────────────────────────────┐
│ Method          │ Mode       │ Key Behaviour                              │
├─────────────────┼────────────┼────────────────────────────────────────────┤
│ Pass by value   │ In         │ Copy in; caller unaffected                 │
│ Pass by result  │ Out        │ Copy out on return; no initial value       │
│ Pass by V-R     │ Inout      │ Copy in AND out; isolated during execution │
│ Pass by ref     │ Inout      │ Shared address; changes are immediate      │
└─────────────────┴────────────┴────────────────────────────────────────────┘
```