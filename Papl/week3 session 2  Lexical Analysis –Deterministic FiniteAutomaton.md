# Regular Expressions, Languages, and Finite Automata

## Regular Expressions (RE)

### Basic Examples

```
(0|1|2|3|...|9)+
```

- The `+` means **one or more** occurrences.
    
- This describes **one or more digits**.
    

```
(a|...|z|A|...|Z)*
```

- The `*` means **zero or more** occurrences.
    
- This describes any string (including empty) made only of letters.
    

---

### Building Identifiers

We can define components:

```
letter = A | B | ... | Z | a | b | ... | z
digit  = 0 | 1 | ... | 9
```

A typical identifier:

```
ident = letter (_ | letter | digit)*
```

Meaning:

- The first character must be a **letter**
    
- After that, we can have:
    
    - underscore `_`
        
    - letter
        
    - digit
        
- Zero or more times
    

✔ This matches common programming-language identifier rules.

---

## Languages

A **language** is a set of strings over some alphabet.

### Formal Definition

A language ( L ) over an alphabet ( \Sigma ) is:

[  
L \subseteq \Sigma^*  
]

Where:

- ( \Sigma ) = alphabet
    
- ( \Sigma^* ) = set of all possible strings over ( \Sigma ) (including ε)
    

---

### Examples

- `{ε, aab, bb}` is a language over alphabet `{a, b}`
    
- The set of all Java programs is a language over the ASCII alphabet
    
- The set of all C++ programs is also a language
    
- `∅` = empty language (contains no strings)
    
- `{ε}` = language containing only the empty string
    
- `{ a^n b | n ≥ 0 }` = all strings of:
    
    - zero or more `a`’s
        
    - followed by exactly one `b`
        

Examples:

```
b
ab
aab
aaab
...
```

- `Σ*` is a language over Σ containing all possible strings over Σ.
    

---

### Important Note

There is an **infinite number of strings** over most alphabets (including English letters), therefore many languages are infinite sets.

---

## Language of a Regular Expression

We denote the language described by a regular expression `RE` as:

```
L(RE)
```

Examples:

```
L(a*) = { ε, a, aa, aaa, ... }
```

```
L(a|b) = L(a) ∪ L(b)
```

Regular expressions can be nested —  
we can put REs inside other REs.

---

# Decidability of Languages

Given a language ( L \subseteq \Sigma^* ),

We want an **algorithm** that:

For any input string ( w \in \Sigma^* ):

1. Outputs **Yes** if ( w ∈ L )
    
2. Outputs **No** if ( w ∉ L )
    

If such an algorithm exists, the language is **decidable**.

---

## Decision Procedures for Regular Languages

For languages defined by regular expressions, we can construct:

- A **Deterministic Finite Automaton (DFA)**
    
- A **Nondeterministic Finite Automaton (NFA)**
    

Both recognize exactly the **regular languages**.

---

# Finite Automata

## Finite State Automaton (FSA)

A **finite automaton (FA)** consists of:

1. A finite set of states ( Q )
    
2. A finite input alphabet ( \Sigma )
    
3. A distinguished start state ( q_0 \in Q )
    
4. A set of accepting (final) states ( F \subseteq Q )
    
5. A transition function:
    

[  
\delta : Q \times \Sigma \rightarrow Q  
]

---

## Deterministic vs Nondeterministic

### DFA (Deterministic Finite Automaton)

- For each state and input symbol, there is **exactly one** transition.
    
- The machine has **no choice** about what to do next.
    

### NFA (Nondeterministic Finite Automaton)

- For a state and input symbol, there may be:
    
    - Multiple possible transitions
        
    - Or none
        
- May include ε-transitions (transitions without consuming input).
    

Important fact:

> Every NFA has an equivalent DFA.

---

# DFA for Lexical Analysis

DFAs are commonly used in **lexical analysis** (tokenizing source code).

They can verify whether a string matches a token pattern (e.g., identifier, number, keyword).

---

## DFA Diagram Conventions

- States are drawn as **circles**
    
- Start state has an incoming arrow
    
- Accepting states are drawn with **double circles**
    
- Transitions are labeled with input symbols
    

---

## How a DFA Processes Input

1. Start in the initial state
    
2. Read input **one symbol at a time**
    
3. Follow transitions according to the transition function
    
4. After the final symbol:
    
    - If in an accepting state → **accept**
        
    - Otherwise → **reject**
        

---

### Example

If processing the string:

```
abb
```

The DFA might:

- Start in state 1
    
- On `a` → go to state 2
    
- On `b` → go to state 4
    
- On final `b` → remain in state 4
    

If state 4 is accepting → `abb` is accepted.

---

# Summary

- Regular Expressions describe **regular languages**
    
- Languages are sets of strings over an alphabet
    
- Regular languages are **decidable**
    
- They can be recognized by:
    
    - DFA
        
    - NFA
        
- DFAs are widely used in compilers for **lexical analysis**
    

