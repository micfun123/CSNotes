
## Proposition

A **proposition** is a declarative statement that is either **true or false**, but not both.

---

## Propositional Variable

A **propositional variable** (usually denoted ( p, q, r, \dots )) represents a proposition and takes one of two truth values:

- True (T)
    
- False (F)
    

---

## Negation (¬)

If ( p ) is a proposition, the **negation** of ( p ), written ( ¬p ), means “not p”.

|p|¬p|
|---|---|
|T|F|
|F|T|

---

## Conjunction (∧)

The **conjunction** of ( p ) and ( q ), written ( p ∧ q ), means “p and q”.  
It is true only when both ( p ) and ( q ) are true.

|p|q|p ∧ q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|F|

---

## Disjunction (∨)

The **(inclusive) disjunction** of ( p ) and ( q ), written ( p ∨ q ), means “p or q”.  
It is true when at least one of ( p ) or ( q ) is true.

|p|q|p ∨ q|
|---|---|---|
|T|T|T|
|T|F|T|
|F|T|T|
|F|F|F|

---

## Implication (→)

The **implication** ( p → q ) means “if p then q”.

- ( p ): hypothesis
    
- ( q ): conclusion
    

|p|q|p → q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|T|
|F|F|T|

---

## Biconditional (↔)

The **biconditional** ( p ↔ q ) means “p if and only if q” (iff).  
It is true when ( p ) and ( q ) have the same truth value.

|p|q|p ↔ q|
|---|---|---|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|T|

---

## Tautology

A statement that is **true for all possible truth values** of its variables.  
Example: ( p ∨ ¬p )

---

## Contradiction

A statement that is **false for all possible truth values**.  
Example: ( p ∧ ¬p )

---

## Contingency

A statement that is sometimes true and sometimes false, depending on the truth values of its variables.

---

## Logical Equivalence (≡)

Two statements are **logically equivalent**, written ( p ≡ q ), if they have identical truth values for all possible assignments of their variables.

---

## Negation of a Conditional

[  
¬(p → q) ≡ p ∧ ¬q  
]

---

## Contrapositive

The **contrapositive** of ( p → q ) is:  
[  
¬q → ¬p  
]

A conditional statement is logically equivalent to its contrapositive.

---

## Necessary Condition

“r is necessary for s” means:  
[  
s → r  
]

---

## Sufficient Condition

“r is sufficient for s” means:  
[  
r → s  
]

---

# Modus Ponens

If:

1. ( p → q )
    
2. ( p )
    

Then:

- ( q )
    

---

# Order of Operations (Precedence of Connectives)

1. Brackets
    
2. ¬
    
3. ∧
    
4. ∨
    
5. →
    
6. ↔
    

---

# Core Logical Equivalences

### Idempotent Laws

- ( p ∧ p ≡ p )
    
- ( p ∨ p ≡ p )
    

### Identity Laws

- ( p ∧ T ≡ p )
    
- ( p ∨ F ≡ p )
    

### Domination Laws

- ( p ∨ T ≡ T )
    
- ( p ∧ F ≡ F )
    

### Double Negation

- ( ¬(¬p) ≡ p )
    

### Complement Laws

- ( p ∨ ¬p ≡ T )
    
- ( p ∧ ¬p ≡ F )
    

### Commutative Laws

- ( p ∧ q ≡ q ∧ p )
    
- ( p ∨ q ≡ q ∨ p )
    

### Distributive Laws

- ( p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r) )
    
- ( p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r) )
    

### Implication Law

- ( p → q ≡ ¬p ∨ q )
    

### De Morgan’s Laws

- ( ¬(p ∨ q) ≡ ¬p ∧ ¬q )
    
- ( ¬(p ∧ q) ≡ ¬p ∨ ¬q )
    

---

# Methods for Proving Logical Equivalence

### 1. Truth Tables

Construct full truth tables and compare final columns.

### 2. Using Logical Identities

Apply equivalence laws to simplify expressions.

---

# Example Simplification

Show that:

[  
(¬(p ∨ q)) ∨ ((¬p) ∧ q)  
]

[  
≡ (¬p ∧ ¬q) ∨ (¬p ∧ q)  
]

[  
≡ ¬p ∧ (¬q ∨ q)  
]

[  
≡ ¬p ∧ T  
]

[  
≡ ¬p  
]

---

# Summary

- Propositions and propositional variables
    
- Logical connectives: ¬, ∧, ∨, →, ↔
    
- Truth tables
    
- Logical equivalence
    
- Tautology, contradiction, contingency
    
- Contrapositive
    
- Necessary and sufficient conditions
    

---

If you'd like it reformatted into atomic linked Obsidian notes instead of one long note, I can restructure it that way.