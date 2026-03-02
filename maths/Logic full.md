# Lecture DM-4: Logic Definitions

- **Proposition:** A statement (declarative sentence) that is either true or false, but not both.
    
- **Modus Ponens:** A logic rule stating "If X then Y" is true and "X" is true, so "Y" must be true.
    
- **Negation ($\neg p$):** If $p$ is a statement, the negation of $p$ is the statement "not $p$".
    
- **Conjunction ($p \wedge q$):** The compound statement "$p$ and $q$", which is true only if both $p$ and $q$ are true.

- **Disjunction ($p \vee q$):** The compound statement "$p$ or $q$", which is true if at least one of $p$ or $q$ is true (inclusive or).

- **Implication ($p \rightarrow q$):** The compound statement "if $p$ then $q$", where $p$ is the hypothesis and $q$ is the conclusion.
    
- **Biconditional ($p \leftrightarrow q$):** The compound statement "$p$ if and only if $q$" (iff).

- **Tautology:** A statement that is true for all possible values of its propositional variables.
    
- **Contradiction:** A statement that is false for all possible values of its propositional variables.
    
- **Contingency:** A statement that can be either true or false depending on the truth values of its propositional variables.
    
- **Logical Equivalence ($p \equiv q$):** Two statements are logically equivalent if they have identical truth values for each possible value of their statement variables.
    
- **Sufficient Condition:** In the statement "If $r$ then $s$", $r$ is a sufficient condition for $s$.
    
- **Necessary Condition:** In the statement "If $r$ then $s$" (equivalent to "$r$ only if $s$"), $s$ is a necessary condition for $r$.

---

# Lecture Notes

## 1. Introduction to Logic

- **Role of Logic:**
    
    - Used in mathematics to prove theorems.
        
    - Used in computer science to verify program correctness.
        
    - Used in natural/physical sciences to draw conclusions from experiments.
        
- **Modus Ponens:** The fundamental rule of reasoning: If $X \rightarrow Y$ is true, and $X$ is true, then $Y$ must be true.
    

## 2. Propositions and Variables

- **Propositional Variables:** Letters like $p, q, r$ denote variables that have a truth value of either **True (T)** or **False (F)**.
    
    - _Example:_ $p$: "Djokovic will win Wimbledon".
        
- **Compound Statements:** Variables are combined using logical connectives. Truth values depend on the individual statements and the connectives used .
    
 
    

## 3. Logical Connectives

### Negation ($\neg$)

- **Symbol:** $\neg$ or $-$ (not).
    
    +2
    
- **Function:** Reverses the truth value.
    
    - If $p$ is True, $\neg p$ is False.
        
    - _Example:_ $p: 2+3 > 1$ (True) $\rightarrow \neg p: 2+3 \le 1$ (False).
        

### Conjunction ($\wedge$)

- **Symbol:** $\wedge$ (and).
    
    +2
    
- **Truth Table:** True only when **both** $p$ and $q$ are True.
    
    - T $\wedge$ T = T
        
    - T $\wedge$ F = F
        
    - F $\wedge$ T = F
        
    - F $\wedge$ F = F
        

### Disjunction ($\vee$)

- **Symbol:** $\vee$ (or).
    
 
    
- **Truth Table:** True if **at least one** is True (Inclusive OR).
    
    - T $\vee$ T = T
        
    - T $\vee$ F = T
        
    - F $\vee$ T = T
        
    - F $\vee$ F = F
        
- **Note:** In logic, "or" is inclusive (one or both), unlike the exclusive "or" (one or the other but not both) often used in natural language .
    

### Implication ($p \rightarrow q$)

- **Symbol:** $\rightarrow$ (if-then).

- **Truth Table:** False only when Hypothesis ($p$) is True and Conclusion ($q$) is False.
    
    - T $\rightarrow$ T = T
        
    - T $\rightarrow$ F = F
        
    - F $\rightarrow$ T = T (Vacuously true)
        
    - F $\rightarrow$ F = T
        

### Biconditional ($p \leftrightarrow q$)

- **Symbol:** $\leftrightarrow$ (if and only if / iff).

- **Truth Table:** True only when $p$ and $q$ have the **same** truth value.
    
    - T $\leftrightarrow$ T = T
        
    - F $\leftrightarrow$ F = T
        

### Hierarchy of Evaluation

Similar to algebraic order of operations, logical connectives are evaluated in this order:

1. Brackets `()`
    
2. Negation $\neg$
    
3. Conjunction $\wedge$, Disjunction $\vee$
    
4. Implication $\rightarrow$
    
5. Biconditional $\leftrightarrow$
    

## 4. Truth of Compound Propositions

### Classifications

- **Tautology:** Always true (e.g., $p \vee \neg p$).
    
- **Contradiction:** Always false (e.g., $p \wedge \neg p$).
    
- **Contingency:** Can be true or false depending on inputs.
    

### Logical Equivalence

- Two statements are equivalent ($p \equiv q$) if their truth tables are identical.
    
- **Determining Equivalence:**
    
    1. **Truth Tables:** Check if final truth values match for all inputs (adding variables doubles table size).
        
    2. **Basic Laws:** Simplify propositions using established equivalences.
        

## 5. Basic Logical Equivalences

- **Identity/Domination:**
    
    - $p \wedge T \equiv p$
        
    - $p \vee F \equiv p$
        
    - $p \vee (\neg p) \equiv T$
        
    - $p \wedge (\neg p) \equiv F$
        
- **Double Negation:** $\neg(\neg p) \equiv p$.
    
- **Commutativity:**
    
    - $p \wedge q \equiv q \wedge p$
        
    - $p \vee q \equiv q \vee p$
        
- **Distributivity:**
    
    - $p \vee (q \wedge r) \equiv (p \vee q) \wedge (p \vee r)$
        
    - $p \wedge (q \vee r) \equiv (p \wedge q) \vee (p \wedge r)$
        
- **De Morgan's Laws:**
    
    - $\neg(p \vee q) \equiv (\neg p) \wedge (\neg q)$
        
    - $\neg(p \wedge q) \equiv (\neg p) \vee (\neg q)$
        
- **Implication Rules:**
    
    - **Definition:** $p \rightarrow q \equiv \neg p \vee q$.
        
    - **Negation:** $\neg(p \rightarrow q) \equiv p \wedge \neg q$.
        
    - **Contrapositive:** $p \rightarrow q \equiv \neg q \rightarrow \neg p$.
        

## 6. Necessary and Sufficient Conditions

- Statements of the form "$p$ if and only if $q$" represent the conjunction of two conditionals:
    
    1. **Sufficiency:** "If $p$ then $q$" ($p \rightarrow q$).
        
    2. **Necessity:** "$p$ only if $q$" or "If not $q$ then not $p$" ($q \rightarrow p$ or $\neg q \rightarrow \neg p$) .