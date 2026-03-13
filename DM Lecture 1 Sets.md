

## Key Definitions

> [!definition] Set A **set** is a collection of objects called the **elements** (or **members**) of the set.
> 
> - No repeated occurrences of elements
> - No particular order of elements

> [!definition] Empty Set (Null Set) The set with **no elements**, denoted $\emptyset$ or ${ }$.

> [!definition] Cardinality If $X$ is a **finite set**, $|X|$ = the number of elements in $X$.

> [!definition] Subset $A \subseteq B$ if every element of $A$ is also an element of $B$.
> 
> - If $A$ is **not** a subset of $B$: $A \not\subseteq B$
> - **Proper subset**: $A \subset B$ if $A \subseteq B$ and $B$ has at least one element not in $A$

> [!definition] Equality of Sets $A = B$ if and only if $A \subseteq B$ **and** $B \subseteq A$ (they contain exactly the same elements).

> [!definition] Intersection $A \cap B = {x \mid x \in A \text{ and } x \in B}$ Sets are **disjoint** if $A \cap B = \emptyset$

> [!definition] Union $A \cup B = {x \mid x \in A \text{ or } x \in B}$

> [!definition] Difference $A \setminus B = {x \mid x \in A \text{ and } x \notin B}$ (also written $A - B$)

> [!definition] Complement Given a universe $U$: $A' = {x \mid x \in U \text{ and } x \notin A}$ (also written $\bar{A}$)

> [!definition] Power Set The collection of **all subsets** of $S$, denoted $\mathcal{P}(S)$. If $|S| = n$, then $|\mathcal{P}(S)| = 2^n$

> [!definition] Partition A collection of **nonempty, mutually disjoint** subsets of $S$ whose union is $S$. Every element of $S$ belongs to exactly one subset.

---

## Standard Number Sets

|Symbol|Name|Example|
|---|---|---|
|$\mathbb{N}$|Natural numbers|${0, 1, 2, 3, \ldots}$|
|$\mathbb{Z}$|Integers|${\ldots, -2, -1, 0, 1, 2, \ldots}$|
|$\mathbb{Q}$|Rational numbers|${0, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \ldots}$|
|$\mathbb{R}$|Real numbers|All rationals + irrationals|

Containment: $\mathbb{N} \subset \mathbb{Z} \subset \mathbb{Q} \subset \mathbb{R}$

---

## Notation & Set Description

**Two ways to describe a set:**

1. **Listing elements** (for finite sets): $A = {3, 6, 9, 12}$
2. **Set-builder notation** (by property): $B = {x \mid x \text{ is a multiple of 3 and } 0 < x < 15}$
    - `|` is read "such that" (`:` also used)

**Ellipsis notation:** ${1, 2, \ldots, 10}$ = ${1, 2, 3, 4, 5, 6, 7, 8, 9, 10}$

**Membership:** $x \in S$ (x is in S), $x \notin S$ (x is not in S)

---

## Properties of Set Operations

|Property|Rule|
|---|---|
|Identity|$A \cup \emptyset = A$, $\quad A \cap \emptyset = \emptyset$|
|Idempotent|$A \cup A = A$, $\quad A \cap A = A$|
|Commutative|$A \cup B = B \cup A$, $\quad A \cap B = B \cap A$|
|Associative|$(A \cup B) \cup C = A \cup (B \cup C)$|
|Distributive|$A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$|
|De Morgan's|$(A \cap B)' = A' \cup B'$|
|De Morgan's|$(A \cup B)' = A' \cap B'$|

---

## Counting — Inclusion-Exclusion Principle

$$|A \cup B| = |A| + |B| - |A \cap B|$$

> Simply adding $|A|$ and $|B|$ double-counts the intersection!

---

## Worked Examples

### Set Notation

Let $P = {4, 5, 7}$ and $Q = {5, 7, 4}$:

- $P = Q$ ✅ (order doesn't matter)
- $P = {7, 5, 4}$ ✅ (same elements)
- $P = (7, 5, 4)$ ❌ (round brackets denote ordered tuples, not sets)
- $6 \in P$? ❌   $5 \notin Q$? ❌ (5 IS in Q)

### Operations

Let $A = {a, b, c}$, $B = {c, d}$, $U = {a, b, c, d}$:

|Operation|Result|
|---|---|
|$A \cap B$|${c}$|
|$A \cup B$|${a, b, c, d}$|
|$A \setminus B$|${a, b}$|
|$B \setminus A$|${d}$|
|$A'$|${b, d}$ ... wait, $U \setminus A = {d}$... use $U={a,b,c,d}$, $A={a,b,c}$, $A'={d}$|

Note: $A \setminus B \neq B \setminus A$ in general.

### Power Set

$S = {a, b, c}$ → $|\mathcal{P}(S)| = 2^3 = 8$

$$\mathcal{P}(S) = {\emptyset,\ {a},\ {b},\ {c},\ {a,b},\ {b,c},\ {a,c},\ {a,b,c}}$$

### Odd Integers — Same Set, Different Notation

$$S = {\ldots, -3, -1, 1, 3, 5, \ldots} = {x \mid x \text{ is odd}} = {2k+1 \mid k \in \mathbb{Z}}$$

---

## Venn Diagrams

Used for a visual representation of sets within a universe $U$.

|Region|Set Expression|
|---|---|
|Overlap of A and B only|$A \cap B$|
|All of A and B|$A \cup B$|
|A but not B|$A \setminus B$|
|Outside A (within U)|$A'$|

For **three sets** A, B, C:

- Centre overlap (all three): $A \cap B \cap C$
- Only in C (not A or B): $C \setminus A \setminus B$

---

## Summary Checklist

- [ ] Define a set and list its two key characteristics
- [ ] Use $\in$, $\notin$, $\subseteq$, $\subset$ notation correctly
- [ ] Distinguish finite vs infinite sets; compute cardinality
- [ ] Perform intersection, union, difference, complement
- [ ] Apply De Morgan's laws and distributive properties
- [ ] Apply the inclusion-exclusion principle
- [ ] Construct the power set of a small set
- [ ] Identify a valid partition of a set

---

