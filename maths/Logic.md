
## Proposition

A **proposition** is a declarative statement that is either **true or false**, but not both.

---

## Propositional Variable

A **propositional variable** (usually denoted $p, q, r, \dots$) represents a proposition and takes one of two truth values:

- True (T)
- False (F)

---

## Negation ($\neg$)

If $p$ is a proposition, the **negation** of $p$, written $\neg p$, means "not p".

|p|¬p|
|---|---|
|T|F|
|F|T|

---

## Conjunction ($\wedge$)

The **conjunction** of $p$ and $q$, written $p \wedge q$, means "p and q".  
It is true only when both $p$ and $q$ are true.

|p|q|p ∧ q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|F|

---

## Disjunction ($\vee$)

The **(inclusive) disjunction** of $p$ and $q$, written $p \vee q$, means "p or q".  
It is true when at least one of $p$ or $q$ is true.

|p|q|p ∨ q|
|---|---|---|
|T|T|T|
|T|F|T|
|F|T|T|
|F|F|F|

---

## Implication ($\to$)

The **implication** $p \to q$ means "if p then q".

- $p$: hypothesis
- $q$: conclusion

|p|q|p → q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|T|
|F|F|T|

---

## Biconditional ($\leftrightarrow$)

The **biconditional** $p \leftrightarrow q$ means "p if and only if q" (iff).  
It is true when $p$ and $q$ have the same truth value.

|p|q|p ↔ q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|T|

---

## Tautology

A statement that is **true for all possible truth values** of its variables.  
Example: $p \vee \neg p$

---

## Contradiction

A statement that is **false for all possible truth values**.  
Example: $p \wedge \neg p$

---

## Contingency

A statement that is sometimes true and sometimes false, depending on the truth values of its variables.

---

## Logical Equivalence ($\equiv$)

Two statements are **logically equivalent**, written $p \equiv q$, if they have identical truth values for all possible assignments of their variables.

---

## Negation of a Conditional

$$\neg(p \to q) \equiv p \wedge \neg q$$

---

## Contrapositive

The **contrapositive** of $p \to q$ is:

$$\neg q \to \neg p$$

A conditional statement is logically equivalent to its contrapositive.

---

## Necessary Condition

"r is necessary for s" means:

$$s \to r$$

---

## Sufficient Condition

"r is sufficient for s" means:

$$r \to s$$

---

# Modus Ponens

If:

1. $p \to q$
2. $p$

Then:

- $q$

---

# Order of Operations (Precedence of Connectives)

1. Brackets
2. $\neg$
3. $\wedge$
4. $\vee$
5. $\to$
6. $\leftrightarrow$

---

# Core Logical Equivalences

### Idempotent Laws

- $p \wedge p \equiv p$
- $p \vee p \equiv p$

### Identity Laws

- $p \wedge T \equiv p$
- $p \vee F \equiv p$

### Domination Laws

- $p \vee T \equiv T$
- $p \wedge F \equiv F$

### Double Negation

- $\neg(\neg p) \equiv p$

### Complement Laws

- $p \vee \neg p \equiv T$
- $p \wedge \neg p \equiv F$

### Commutative Laws

- $p \wedge q \equiv q \wedge p$
- $p \vee q \equiv q \vee p$

### Associative Laws

- $(p \wedge q) \wedge r \equiv p \wedge (q \wedge r)$
- $(p \vee q) \vee r \equiv p \vee (q \vee r)$

### Distributive Laws

- $p \vee (q \wedge r) \equiv (p \vee q) \wedge (p \vee r)$
- $p \wedge (q \vee r) \equiv (p \wedge q) \vee (p \wedge r)$

### Implication Law

- $p \to q \equiv \neg p \vee q$

### De Morgan's Laws

- $\neg(p \vee q) \equiv \neg p \wedge \neg q$
- $\neg(p \wedge q) \equiv \neg p \vee \neg q$

---

# Methods for Proving Logical Equivalence

### 1. Truth Tables

Construct full truth tables and compare final columns.

### 2. Using Logical Identities

Apply equivalence laws to simplify expressions.

---

# Example Simplification

Show that $(\neg(p \vee q)) \vee ((\neg p) \wedge q) \equiv \neg p$:

$$(\neg(p \vee q)) \vee ((\neg p) \wedge q)$$

$$\equiv (\neg p \wedge \neg q) \vee (\neg p \wedge q) \quad \text{(De Morgan's Law)}$$

$$\equiv \neg p \wedge (\neg q \vee q) \quad \text{(Distributive Law)}$$

$$\equiv \neg p \wedge T \quad \text{(Complement Law)}$$

$$\equiv \neg p \quad \text{(Identity Law)}$$

---

# Summary

- Propositions and propositional variables
- Logical connectives: $\neg, \wedge, \vee, \to, \leftrightarrow$
- Truth tables
- Logical equivalence
- Tautology, contradiction, contingency
- Contrapositive
- Necessary and sufficient conditions
