# Lecture 15: Statement-Level Control Structures
### Programming Applications and Programming Languages — Dr Jiacheng Tan, University of Portsmouth

---

## Definitions

| Term | Definition |
|------|-----------|
| **Control Statement** | A statement that selects among alternative control flow paths or causes the repeated execution of a collection of statements. |
| **Selection Statement** | A statement that chooses between two or more execution paths in a program. |
| **Two-Way Selection** | A selection statement that picks one of exactly two execution paths (e.g. `if-then-else`). |
| **Multiple-Way Selection** | A selection statement that picks one of many execution paths (e.g. `switch`). |
| **Iterative Statement** | A mechanism for the repeated execution of a statement or compound statement; implemented via loops or recursion. |
| **Counter-Controlled Loop** | A loop driven by a counter variable (e.g. `for` loop). |
| **Logically-Controlled Loop** | A loop driven by a Boolean condition (e.g. `while`, `do...while`). |
| **Pre-test Loop** | A loop where the condition is tested *before* the loop body executes (e.g. `while`). |
| **Post-test Loop** | A loop where the loop body executes *at least once* before the condition is tested (e.g. `do...while`). |
| **Unconditional Branching** | A statement that transfers control flow without any condition (e.g. `goto`, `break`, `continue`, `return`). |
| **Fall-Through Behaviour** | In a `switch` statement, once a case is matched, execution continues into subsequent cases until a `break` or end of the `switch` is reached. |
| **Structured Programming Theorem** | States that all algorithms expressible by flowcharts can be coded using only two control statements: selection and a pre-test logical loop. |
| **Compound Statement (Block)** | A group of statements treated as a single unit, enclosed by braces `{}` in most languages, or by indentation in Python. |
| **Labelled Break** | A `break` that exits a specifically labelled outer loop or statement, not just the innermost one. |
| **Labelled Continue** | A `continue` that skips the current iteration of a specifically labelled outer loop. |

---

## 1. Introduction & Levels of Flow Control

Flow control (execution sequence) makes it possible to implement algorithms. It can be examined at three levels:

- **Within expressions** — governed by operator precedence and associativity (covered in the previous lecture).
- **Statement level** — this lecture.
- **Program unit level** — covered in the next lecture.

---

## 2. Evolution of Control Structures

- In the **1950s**, little was understood about the complexity of programming.
- In the **1960s**, there was significant debate over the use of the `goto` statement.
- Overuse of `goto` and `break` (often due to poor style or lack of proper subprogram structures) led to code that was **hard to read and maintain** — sometimes called "spaghetti code".
- Research eventually concluded that **unconditional branching is not necessary** — any algorithm can be expressed without `goto`.

---

## 3. The Structured Programming Theorem

> All algorithms expressible by flowcharts can be coded using only **two** control statements:
> 1. **Selection** (choosing between two control flow paths)
> 2. **Pre-test logical loop** (condition tested before the loop body, e.g. `while`)

These two are the *minimum necessary* for any imperative language. In practice, most languages provide many variations of these.

---

## 4. Selection Statements

### 4.1 Two-Way Selection (`if-then-else`)

General form:
```
if control_expression
  then clause
  else clause
```

Key design points:
- **Control expression:** C89 used arithmetic expressions (zero = false, non-zero = true). Most modern languages (Java, C#) require a Boolean expression. Python and C++ still allow arithmetic.
- **Clauses** can be single statements or compound statements (blocks).
- Languages like Java/C use `{}` braces for blocks; Python uses **indentation**.

**Python shorthand (ternary):**
```python
print("b>a") if b > a else print("b<=a")
```

**Java shorthand (ternary operator):**
```java
int x = (expression) ? -1 : 1;
```

### 4.2 Nested Selectors — The Dangling Else Problem

When `if` statements are nested, ambiguity can arise:
```java
if (sum == 0)
    if (count == 0)
        result = 0;
    else
        result = 1;  // Which if does this else belong to?
```

**Java's rule:** `else` matches the **nearest previous unmatched `if`**. The above is equivalent to:
```java
if (sum == 0) {
    if (count == 0)
        result = 0;
    else
        result = 1;
}
```
Use braces to make intent explicit and avoid bugs.

---

### 4.3 Multiple-Way Selection (`switch`)

General form in C, C++, Java, JavaScript:
```java
switch (expression) {
    case const_expr1: stmt1;
    ...
    case const_exprn: stmtn;
    [default: stmtn+1]
}
```

**Control expression types in Java:** `char`, `byte`, `short`, `int`, or `String`.

**Fall-through behaviour:** Without a `break`, execution continues into the next case automatically. This is sometimes useful (e.g. grouping cases 1 & 3 together), but can cause bugs if unintended.

```java
// With explicit break to prevent fall-through:
switch (index) {
    case 1:
    case 3: odd += 1;
            sumodd += index;
            break;
    case 2:
    case 4: even += 1;
            sumeven += index;
            break;
    default: System.out.println("Error!");
}
```

> **C# difference:** Does NOT allow fall-through. Every case segment must end with `break`, `goto`, or `return`.

---

## 5. Iterative Statements

### 5.1 `for` Loop (Counter-Controlled)

```
for (expr_1; expr_2; expr_3)
    loop body
```

| Part | Purpose | When evaluated |
|------|---------|----------------|
| `expr_1` | Initialisation | Once, at the start |
| `expr_2` | Loop condition / termination control | Before each iteration |
| `expr_3` | Step / increment | After each iteration |

- In **C/C++**, `expr_2` can be arithmetic (0 = false, non-zero = true). If absent, the loop is **infinite**.
- In **Java/C#**, `expr_2` must be Boolean.

**Example:**
```java
for (int count = 1; count <= 10; count++) { ... }
```

### 5.2 Logically-Controlled Loops

| Type | Syntax | Body executes at least once? |
|------|--------|------------------------------|
| Pre-test | `while (condition) { }` | No — condition checked first |
| Post-test | `do { } while (condition);` | **Yes** — body runs before check |

- `for` loops can always be rewritten as `while` loops.
- In **C/C++**, the control expression can be arithmetic. In **Java**, it must be Boolean.

---

## 6. Unconditional Branching

Statements that transfer control without a condition:

| Statement | Behaviour |
|-----------|-----------|
| `break` | Exits a loop or `switch` entirely |
| `continue` | Skips the rest of the current loop iteration; loop condition is re-evaluated |
| `return` | Terminates a function/method, optionally returning a value |

### Labelled vs Unlabelled

- **C, C++, Python:** Only unlabelled `break` and `continue` (affects innermost loop only).
- **Java, Perl:** Support both **labelled** and **unlabelled** versions.

### Labelled `break` (Java)

Exits the loop associated with the given label — useful for breaking out of **nested loops**:
```java
search:
for (int i = 0; i < row; i++) {
    for (int j = 0; j < col; j++) {
        if (anArray[i][j] == 5) {
            foundIt = true;
            break search;  // exits the OUTER loop
        }
    }
}
```

### Labelled `continue` (Java)

Skips to the next iteration of the **labelled** (outer) loop:
```java
test:
for (int i = 0; i <= max; i++) {
    while (n > 0) {
        if (searchMe.charAt(j) != substring.charAt(k))
            continue test;  // skip to next i
        ...
    }
}
```

### `return`
- Can return a value: `return <expression>;`
- Pascal does **not** have a `return` statement.

---

## 7. Summary Table

| Category | Examples | Key Feature |
|----------|----------|-------------|
| Two-way selection | `if-then-else`, ternary `? :` | Choose one of two paths |
| Multiple-way selection | `switch` | Choose one of many paths; beware fall-through |
| Counter loop | `for` | Best when number of iterations is known |
| Pre-test loop | `while` | May execute zero times |
| Post-test loop | `do...while` | Always executes at least once |
| Unconditional branch | `break`, `continue`, `return` | Transfer control immediately; use sparingly |
