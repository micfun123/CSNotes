# Discrete Mathematics – Sets (Revision Notes)

---

## 📖 Definitions

| Term                      | Definition                                                                                               |
| ------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Set**                   | A collection of objects called **elements** (or **members**). No repeated elements; no particular order. |
| **Element / Member**      | An object belonging to a set. Written $x \in S$ (x is in S) or $x \notin S$ (x is not in S).             |
| **Empty Set (Null Set)**  | The set with no elements, denoted $\emptyset$ or ${}$.                                                   |
| **Finite Set**            | A set whose elements can be counted in a finite amount of time.                                          |
| **Infinite Set**          | A set whose elements cannot be fully counted.                                                            |
| **Cardinality**           | The number of elements in a finite set $X$, written $|X|$.                                               |
| **Subset**                | $A \subseteq B$ if every element of $A$ is also in $B$.                                                  |
| **Proper Subset**         | $A \subset B$ if $A \subseteq B$ and $B$ has at least one element not in $A$.                            |
| **Equal Sets**            | $A = B$ if $A \subseteq B$ and $B \subseteq A$ (same elements).                                          |
| **Intersection**          | $A \cap B = {x \mid x \in A \text{ and } x \in B}$ — elements in both sets.                              |
| **Disjoint Sets**         | Sets $A$ and $B$ where $A \cap B = \emptyset$ (no common elements).                                      |
| **Union**                 | $A \cup B = {x \mid x \in A \text{ or } x \in B}$ — elements in either set.                              |
| **Difference**            | $A \setminus B = {x \mid x \in A \text{ and } x \notin B}$ (also written $A - B$).                       |
| **Complement**            | $A' = {x \mid x \in U \text{ and } x \notin A}$ — everything in the universe $U$ not in $A$.             |
| **Universe of Discourse** | The set $U$ containing all sets under consideration.                                                     |
| **Power Set**             | $\mathcal{P}(S)$ — the collection of **all subsets** of $S$. If $|S| = n$, then $|\mathcal{P}(S)| = 2^n$. |
| **Partition**             | A collection of non-empty, mutually disjoint subsets of $S$ whose union equals $S$.                      |
| **Venn Diagram**          | A pictorial representation of sets and their relationships.                                              |

---

## 1. Sets

A **set** is a collection of objects. Two key characteristics:

- **No repeated elements** — ${1, 1, 2}$ is the same as ${1, 2}$
- **No particular order** — ${4, 5, 7} = {7, 5, 4}$

### Notation

- Elements enclosed in braces: $A = {1, 2, 3}$, $C = {\text{Portsmouth, Brighton, London}}$
- $x \in S$ means $x$ is an element of $S$
- $x \notin S$ means $x$ is not an element of $S$

---

## 2. Describing Sets

**Two methods:**

**① Listing elements** (mainly for finite sets): $$A = {3, 6, 9, 12}$$

**② Set-builder notation** (specifying a property): $$B = {x \mid x \text{ is a multiple of 3 and } 0 < x < 15}$$

- `|` is read as "such that" (`:` is also used)
- Three-dots notation: ${1, 2, \ldots, 10}$ is the same as ${1, 2, 3, 4, 5, 6, 7, 8, 9, 10}$

---

## 3. Standard Sets of Numbers

|Symbol|Set|Example|
|---|---|---|
|$\mathbb{N}$|Natural numbers|${0, 1, 2, 3, 4, \ldots}$|
|$\mathbb{Z}$|Integers|${\ldots, -2, -1, 0, 1, 2, \ldots}$|
|$\mathbb{Q}$|Rational numbers|${0, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \ldots}$|
|$\mathbb{R}$|Real numbers|All numbers on the number line|

**Example** — multiple ways to describe the set of odd integers $S$: $$S = {\ldots, -5, -3, -1, 1, 3, 5, \ldots} = {x \mid x = 2k+1 \text{ for some } k \in \mathbb{Z}} = {2k+1 \mid k \in \mathbb{Z}}$$

---

## 4. Empty, Finite & Infinite Sets

- **Empty set:** $\emptyset = {}$ — e.g. ${x \mid x \in \mathbb{N} \text{ and } x < 10 \text{ and } x > 20} = \emptyset$
- **Finite set:** $A = {3, 7, 9}$ has cardinality $|A| = 3$
- **Infinite sets:** $\mathbb{N}$ and $\mathbb{Z}$ are infinite

---

## 5. Subsets & Equality

- $\emptyset \subseteq A$ for **any** set $A$
- $A \subseteq A$ always (every set is a subset of itself)
- ${a, b} \subseteq {a, b, c}$ and $\mathbb{N} \subset \mathbb{Z} \subset \mathbb{Q} \subset \mathbb{R}$
- ${1, 2, 3} \not\subseteq {1, 2, 4}$ (3 is not in the second set)

**Proving equality:** To show $A = B$, prove both $A \subseteq B$ and $B \subseteq A$.

> **Example:** If $A = {2, 4, 6}$ and $B = {6, 4, 2}$, then $A = B$.

---

## 6. Set Operations

### Intersection $A \cap B$

Elements in **both** $A$ and $B$. $$A \cap B = {x \mid x \in A \text{ and } x \in B}$$

> If $A = {a, b, c}$ and $B = {c, d}$, then $A \cap B = {c}$

### Union $A \cup B$

Elements in $A$ **or** $B$ (or both). $$A \cup B = {x \mid x \in A \text{ or } x \in B}$$

> If $A = {a, b, c}$ and $B = {c, d}$, then $A \cup B = {a, b, c, d}$

### Difference $A \setminus B$

Elements in $A$ but **not** in $B$. Note: $A \setminus B \neq B \setminus A$ in general. $$A \setminus B = {x \mid x \in A \text{ and } x \notin B}$$

> If $A = {a, b, c}$ and $B = {c, d}$, then $A \setminus B = {a, b}$ and $B \setminus A = {d}$

### Complement $A'$

Everything in the universe $U$ that is **not** in $A$. $$A' = {x \mid x \in U \text{ and } x \notin A}$$

> If $U = {a,b,c,d}$ and $A = {c,d}$, then $A' = {a,b}$  
> If $U = \mathbb{Z}$ and $A$ = even numbers, then $A'$ = odd numbers

---

## 7. Properties of Set Operations

|Property|Union|Intersection|
|---|---|---|
|**Identity**|$A \cup \emptyset = A$|$A \cap U = A$|
|**Domination**|$A \cup U = U$|$A \cap \emptyset = \emptyset$|
|**Idempotent**|$A \cup A = A$|$A \cap A = A$|
|**Complement**|$A \cup A' = U$|$A \cap A' = \emptyset$|
|**Commutative**|$A \cup B = B \cup A$|$A \cap B = B \cap A$|
|**Associative**|$(A \cup B) \cup C = A \cup (B \cup C)$|$(A \cap B) \cap C = A \cap (B \cap C)$|

**Distributive laws:** $$A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$$ $$A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$$

**De Morgan's Laws:** $$(A \cap B)' = A' \cup B'$$ $$(A \cup B)' = A' \cap B'$$

---

## 8. Inclusion-Exclusion Principle

For finite sets $A$ and $B$, simply adding $|A| + |B|$ counts $|A \cap B|$ **twice**, so:

$$\boxed{|A \cup B| = |A| + |B| - |A \cap B|}$$

This can be generalised to more than two sets.

---

## 9. Power Set

$$\mathcal{P}(S) = \text{the set of ALL subsets of } S$$

> If $S = {a, b, c}$, then: $$\mathcal{P}(S) = {\emptyset,\ {a},\ {b},\ {c},\ {a,b},\ {b,c},\ {a,c},\ {a,b,c}}$$

**Key fact:** If $|S| = n$, then $|\mathcal{P}(S)| = 2^n$

---

## 10. Partition

A **partition** of $S$ is a collection of non-empty subsets such that:

1. The subsets are **mutually disjoint** ($A_i \cap A_j = \emptyset$ for $i \neq j$)
2. Their union equals $S$ (every element of $S$ is in exactly one subset)

> If $S = {a, b, c, d, e, f}$, then ${{a, e}, {c}, {f, d}, {b}}$ is a partition of $S$.

---

## 11. Venn Diagrams

Venn diagrams provide pictorial views of sets within a universe $U$. For three sets $A$, $B$, $C$, each region corresponds to a specific set expression:

|Region colour (slide example)|Set expression|
|---|---|
|Green (centre)|$A \cap B \cap C$|
|Grey|$C \setminus A \setminus B$|
|Yellow|$A \setminus B \setminus C$|
|Cyan|$B \setminus A \setminus C$|
|Magenta|$(A \cap B) \setminus C$|
|Orange|$(B \cap C) \setminus A$|
|Blue overlap|$(A \cap C) \setminus B$|

---

## Summary Checklist

- [ ] Define a set and identify elements using $\in$ / $\notin$ notation
- [ ] Describe sets by listing or by set-builder notation
- [ ] Identify $\mathbb{N}$, $\mathbb{Z}$, $\mathbb{Q}$, $\mathbb{R}$ and their relationships
- [ ] Distinguish finite/infinite sets; compute cardinality $|X|$
- [ ] Determine subsets ($\subseteq$), proper subsets ($\subset$), and set equality
- [ ] Compute intersection, union, difference, and complement
- [ ] Apply De Morgan's laws and distributive properties
- [ ] Apply the inclusion-exclusion formula $|A \cup B| = |A| + |B| - |A \cap B|$
- [ ] Construct the power set $\mathcal{P}(S)$ and know $|\mathcal{P}(S)| = 2^n$
- [ ] Verify whether a collection of subsets forms a valid partition