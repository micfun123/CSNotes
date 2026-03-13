# Discrete Mathematics – Lecture 3: Functions (Revision Notes)

## Definitions

### Function

A **(total) function** $f: A \rightarrow B$ is a relation from set $A$ to set $B$ such that **every element of $A$ is associated with exactly one element in $B$**.

- If $x \in A$, the associated element in $B$ is written as $f(x)$.

---

### Partial Function

A **partial function** from $A$ to $B$ is like a function but **may not be defined for some elements of $A$**.

**Example:** $f(x) = \frac{1}{x}$ from $\mathbb{Z} \rightarrow \mathbb{Q}$ is undefined when $x = 0$.

---

### Domain

The **domain** of a function $f$ is the **set of all inputs for which the function is defined**.

- For a **total function**: Domain $= A$
- For a **partial function**: Domain is a subset of $A$

---

### Co-domain

The **co-domain** of a function $f: A \rightarrow B$ is the **target set $B$**.

---

### Range (Image)

The **range** of a function is the **set of actual outputs produced by the function**.

$$\text{range}(f) = { f(x) \mid x \in A }$$

---

### Injective Function (One-to-One)

A function $f: A \rightarrow B$ is **injective** if **distinct inputs map to distinct outputs**.

$$x \ne y \Rightarrow f(x) \ne f(y)$$

---

### Surjective Function (Onto)

A function $f: A \rightarrow B$ is **surjective** if **every element in $B$ has at least one element in $A$ mapping to it**.

$$\forall y \in B,\ \exists x \in A \text{ such that } f(x) = y$$

---

### Bijective Function

A function is **bijective** if it is **both injective and surjective**.

- Every element maps uniquely.
- Every element in the co-domain is reached.

---

### Composite Function

If $f: A \rightarrow B$ and $g: B \rightarrow C$, the **composition** is:

$$(g \circ f)(x) = g(f(x))$$

This means **apply $f$ first, then $g$**.

---

### Inverse Function

If a function $f$ is **bijective**, then it has an **inverse function** $f^{-1}$.

$$f^{-1}(y) = x \quad \text{if and only if} \quad f(x) = y$$

---

### Operator

An **operator** is a function whose domain contains multiple copies of the same set.

**Example:**

$$f: A \times A \rightarrow A$$

$f(x, y) = x + y$ is a **binary operator**.

---

### Arity

**Arity** is the number of inputs an operator takes.

- **Unary operator** → 1 input
- **Binary operator** → 2 inputs

---

## Key Concepts

### Functions as Special Relations

A function is a **special type of relation** where each input has **exactly one output**.

**Example:** $f(x) = 2x$ from $\mathbb{Z} \rightarrow \mathbb{Z}$

**Identity function:**

$$Id_A(x) = x$$

---

## Ways to Describe Functions

#### 1. Diagram

Mapping elements from set $A$ to set $B$.

#### 2. Formula

$$f(x) = x^3$$

#### 3. List of Associations

```
g(a) = 1
g(b) = 1
g(c) = 2
```

Equivalent ordered pairs: ${(a,1),\ (b,1),\ (c,2)}$

---

## Examples of Functions

### ASCII Functions

- **Asc(c)** → returns ASCII code of character
- **Chr(n)** → returns character with ASCII code $n$

```
Asc('A') = 65
Chr(65) = 'A'
```

---

### String Functions

Let $S$ = set of all strings.

#### First

```
First(s) = first character of string
```

**Example:** `First("valentine") = 'v'`

#### Rest

```
Rest(s) = string with first character removed
```

**Example:** `Rest("valentine") = "alentine"`

Both are **partial functions** because they are **undefined for the empty string**.

---

### Other Examples

#### IsEmpty

```
IsEmpty(s) =
  true   if s = ""
  false  otherwise
```

#### AddFirst

Adds a character to the start of a string.

**Example:** `AddFirst('b', "ee") = "bee"`

---

## Composition Example

$$f(n) = n + 1 \qquad g(n) = n^2$$

#### Compute $(g \circ f)(7)$

$$g(f(7)) = g(8) = 64$$

#### Compute $(f \circ g)(7)$

$$f(g(7)) = f(49) = 50$$

> [!warning] Order matters! $f \circ g \neq g \circ f$

---

## Example: Composite Partial Function

$$\text{magic} = \text{First} \circ \text{Rest} \circ \text{Rest}$$

Returns the **3rd character of a string**.

**Example:** `magic("hello") = 'l'`

It is a **partial function** because strings shorter than 3 characters are undefined.

---

## Key Exam Tips

> [!tip] Remember these!
> 
> - **Function:** every input → exactly one output
> - **Injective:** no two inputs share an output
> - **Surjective:** every element in co-domain is used
> - **Bijective:** injective + surjective
> - **Inverse exists only for bijective functions**
> - **Composition order matters:** $g \circ f \neq f \circ g$