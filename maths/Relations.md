# Discrete Mathematics – Relations (Revision Notes)


---

## 📖 Definitions

|Term|Definition|
|---|---|
|**Ordered Pair**|A pair $(a, b)$ where **order matters** — $(a, b) \neq (b, a)$ unless $a = b$.|
|**Cartesian Product**|$A \times B = {(a, b) \mid a \in A \text{ and } b \in B}$ — the set of all ordered pairs with first element from $A$ and second from $B$.|
|**Binary Relation from $A$ to $B$**|Any subset $T \subseteq A \times B$. If $(a, b) \in T$, we say "$a$ is related to $b$ by $T$", written $aTb$.|
|**Relation on $A$**|A relation from $A$ to itself; a subset of $A \times A$.|
|**Digraph**|A pictorial representation of a relation on a set: vertices = elements, directed edges = related pairs.|
|**Reflexive**|$R$ is reflexive iff $(x, x) \in R$ for **all** $x \in A$.|
|**Symmetric**|$R$ is symmetric iff for all $x, y \in A$: if $(x, y) \in R$ then $(y, x) \in R$.|
|**Transitive**|$R$ is transitive iff for all $x, y, z \in A$: if $(x, y) \in R$ and $(y, z) \in R$ then $(x, z) \in R$.|
|**Equivalence Relation**|A relation that is **reflexive**, **symmetric**, and **transitive**.|
|**Equivalence Class**|For an equivalence $R$ on $A$, the equivalence class of $a$ is $[a] = {x \mid x \in A \text{ and } (x, a) \in R}$ — all elements related to $a$.|

---

## 1. Ordered Pairs

Sets are **unordered** — ${a, b} = {b, a}$. Ordered pairs are **different**: $(a, b) \neq (b, a)$ unless $a = b$.

This distinction matters when modelling directed relationships (e.g. "student $x$ is registered on module $y$" is not the same as "module $y$ is registered on student $x$").

---

## 2. Cartesian Product

$$A \times B = {(a, b) \mid a \in A \text{ and } b \in B}$$

> **Example:** If $X = {1, 2, 3}$ and $Y = {a, b}$, then: $$X \times Y = {(1,a),(1,b),(2,a),(2,b),(3,a),(3,b)}$$

**Key fact:** $|A \times B| = |A| \times |B|$

**Practical example:** Cartesian coordinates — every point in the 2D plane is an element of $\mathbb{R} \times \mathbb{R} = \mathbb{R}^2$.

Can be extended to more sets: $A \times B \times C$ gives ordered triples, etc. (used in relational databases).

---

## 3. Relations

### From $A$ to $B$

A binary relation $T$ from $A$ to $B$ is any subset $T \subseteq A \times B$.

> **Example:** Let $A = {a,b,c,d,e}$ and $B = {1,2,3}$. Then $R_1 = {(a,1),(b,1),(c,2),(c,3)}$ is a relation from $A$ to $B$ because $R_1 \subset A \times B$.

Note that one element of $A$ can be related to **multiple** elements of $B$ (e.g. $c$ maps to both 2 and 3 above). This is what distinguishes a relation from a function.

### On a Set ($A = B$)

A relation **on** $A$ is a subset of $A \times A$.

> **Example:** The "divides" relation on $A = {1,2,3,4}$: $$R = {(1,1),(1,2),(1,3),(1,4),(2,2),(2,4),(3,3),(4,4)}$$ Here $(x,y) \in R$ iff $x$ divides $y$.

### Describing Relations by a Property

Rather than listing pairs, relations are often defined by a rule:

> **Example:** Let $A = {1,2}$ and $B = {1,2,3}$. Define $R$ from $A$ to $B$ by: $x \mathrel{R} y$ iff $x \leq y$. Then: $$R = {(1,1),(1,2),(1,3),(2,2),(2,3)}$$

---

## 4. Digraphs

A **digraph** visualises a relation on a set:

- Each element of $A$ is a **vertex** (dot)
- If $(x, y) \in R$, draw a **directed edge** (arrow) from $x$ to $y$
- Self-loops $(x, x)$ appear as arrows from a vertex back to itself

This is useful for checking reflexivity (every vertex has a self-loop), symmetry (every arrow has a reverse), and transitivity (if there's a path $x \to y \to z$, there must be an arrow $x \to z$).

---

## 5. Properties of Relations

### Reflexivity

$R$ is **reflexive** iff $(x, x) \in R$ for every $x \in A$.

|Relation|Reflexive?|Why|
|---|---|---|
|$R_1 = {(x,y) \mid x \leq y}$ on ${1,2,3,4,5}$|✅ Yes|$(1,1),(2,2),(3,3),(4,4),(5,5) \in R_1$|
|$R_2 = {(x,y) \mid x < y}$ on ${1,2,3,4,5}$|❌ No|$(1,1) \notin R_2$ — nothing equals itself under strict $<$|

> **Tip:** To show NOT reflexive, find just one $x$ where $(x,x) \notin R$.

### Symmetry

$R$ is **symmetric** iff whenever $(x,y) \in R$, also $(y,x) \in R$.

|Relation|Symmetric?|Why|
|---|---|---|
|$R = {(1,1),(1,4),(4,1),(3,3)}$|✅ Yes|$(1,4) \in R$ and $(4,1) \in R$|
|$T = {(1,1),(1,3)}$|❌ No|$(1,3) \in T$ but $(3,1) \notin T$|
|$R_1 = {(x,y) \mid x < y}$|❌ No|$(1,2) \in R_1$ but $(2,1) \notin R_1$|

> **Tip:** In a digraph, symmetry means every arrow has a matching reverse arrow.

### Transitivity

$R$ is **transitive** iff whenever $(x,y) \in R$ and $(y,z) \in R$, also $(x,z) \in R$.

|Relation|Transitive?|Why|
|---|---|---|
|$R_1 = {(x,y) \mid x < y}$ on $\mathbb{N}$|✅ Yes|If $x < y$ and $y < z$, then $x < z$ — standard property of $<$|
|$R_2 = {(1,3),(3,4)}$|❌ No|$(1,3),(3,4) \in R_2$ but $(1,4) \notin R_2$|

> **Tip:** To show NOT transitive, find $x, y, z$ where $(x,y)$ and $(y,z)$ are in $R$ but $(x,z)$ is not.

---

## 6. Equivalence Relations

A relation $R$ on $A$ is an **equivalence relation** iff it is simultaneously **reflexive**, **symmetric**, and **transitive**.

**Checking strategy — work through all three properties in order:**

> **Example:** $R = {(x,y) \mid x,y \in A \text{ and } x,y \text{ have the same remainder when divided by 3}}$ on $A = {1,...,12}$
> 
> - **Reflexive?** ✅ $x$ always has the same remainder as itself.
> - **Symmetric?** ✅ If $x$ and $y$ have the same remainder, so do $y$ and $x$.
> - **Transitive?** ✅ If $x \equiv y \pmod{3}$ and $y \equiv z \pmod{3}$, then $x \equiv z \pmod{3}$.
> 
> All three hold, so $R$ is an equivalence relation.

---

## 7. Equivalence Classes

Given an equivalence relation $R$ on $A$, the **equivalence class** of element $a$ is:

$$[a] = {x \mid x \in A \text{ and } (x, a) \in R}$$

Because $R$ is symmetric, $(x, a) \in R$ iff $(a, x) \in R$, so $[a]$ is the set of all elements that $a$ is related to.

> **Example:** $R = {(x,y) \mid x,y$ have same remainder mod 3$}$ on $A = {1,2,3,4,5,6,7}$:
> 
> |Class|Elements|
> |---|---|
> |$[1] = [4] = [7]$|${1, 4, 7}$ — remainder 1|
> |$[2] = [5]$|${2, 5}$ — remainder 2|
> |$[3] = [6]$|${3, 6}$ — remainder 0|

**Key observation:** Different representatives give the **same** class — $[1] = [4] = [7]$. There are only **3 distinct** equivalence classes.

---

## 8. Equivalence Classes & Partitions ⭐

### Fundamental Theorem

> **Theorem:** If $A$ is a nonempty set and $R$ is an equivalence relation on $A$, then the **distinct equivalence classes of $R$ form a partition of $A$**.

This means:

- The classes are **mutually disjoint** (no element is in two different classes)
- Their **union equals** $A$ (every element is in some class)

This is a deep and beautiful connection between the concepts from Lecture 1 (partitions) and Lecture 2 (equivalence relations).

> **Example (continued):** The distinct equivalence classes ${1,4,7}$, ${2,5}$, ${3,6}$ form a partition of $A = {1,2,3,4,5,6,7}$. ✅

---

## 9. Application: Relational Databases

Relations generalise naturally to **$n$-tuples** and underpin relational database theory:

A relation $R \subseteq A \times B \times C$ where:

- $A$ = student ID numbers
- $B$ = student names
- $C$ = course codes

contains tuples like $(625687, \text{John Smith}, \text{C0056S})$, displayed as rows in a table.

|Set operation|SQL equivalent|Effect|
|---|---|---|
|Union $\cup$|`UNION`|Combines tuples from two tables, removes duplicates|
|Intersection $\cap$|`INTERSECT`|Returns tuples common to both tables|

---

