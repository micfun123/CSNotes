
## Lecture 01: Introduction to Programming Languages 

---

# 1. What Is a Programming Language?

A **programming language** is a formal system used to write instructions that a computer can execute. These instructions tell the computer how to:

- Process data
    
- Make decisions
    
- Repeat tasks
    
- Interact with hardware
    
- Communicate with other systems
    

At its core, programming is about **controlling machine behaviour through abstraction**.

A programming language acts as an **interface between human thinking and machine execution**.

---

# 2. Why Do We Have Different Programming Languages?

Different problems require different tools.

For example:

- Scientific simulations need fast numerical computation.
    
- Banks need accurate decimal arithmetic and reporting.
    
- Operating systems need direct memory access.
    
- Web applications need user interaction and networking.
    

Because hardware, performance requirements, and problem domains vary, languages evolved to specialise.

---

# 3. Programming Domains (Application Areas)

Programming languages often evolve around specific domains.

---

## 3.1 Scientific Applications

Scientific computing involves:

- Large floating-point calculations
    
- Matrix operations
    
- Simulations (weather, physics, engineering)
    
- Heavy use of arrays
    

Key requirement: **performance and numerical accuracy**.

### Example: Fortran

- Created in the 1950s by IBM.
    
- Designed specifically for numerical and scientific computing.
    
- Highly optimised for mathematical formulas.
    
- Still used today in physics, climate modelling, and engineering.
    

Why it mattered:

- It proved high-level languages could be efficient.
    
- Influenced compiler design.
    

---

## 3.2 Business Applications

Business systems handle:

- Financial transactions
    
- Payroll
    
- Banking
    
- Report generation
    
- Text-heavy data processing
    

Key requirement: **decimal precision and structured reporting**.

### Example: COBOL

- Designed in 1959.
    
- English-like syntax for readability.
    
- Excellent support for file handling and formatted reports.
    
- Still heavily used in banking systems.
    

Why it mattered:

- Designed to be readable by non-computer specialists.
    
- Focused on business data, not scientific numbers.
    

---

## 3.3 Artificial Intelligence

AI programming involves:

- Symbol manipulation instead of numeric computation.
    
- Logical reasoning.
    
- Pattern matching.
    
- Linked list processing.
    

Unlike scientific programming, AI deals with **knowledge representation** rather than calculation.

### Example: LISP

- Created in 1958.
    
- Based on mathematical function theory.
    
- Uses lists as its primary data structure.
    
- Supports recursion naturally.
    

Why it mattered:

- Introduced automatic garbage collection.
    
- Influenced functional programming.
    
- Ideal for symbolic reasoning.
    

---

## 3.4 Systems Programming

Systems programming focuses on building:

- Operating systems
    
- Compilers
    
- Device drivers
    
- Embedded systems
    

Key requirements:

- Direct memory access
    
- Hardware interaction
    
- High performance
    
- Low-level control
    

### Example: C

- Developed in the 1970s.
    
- Used to implement UNIX.
    
- Provides:
    
    - Pointers
        
    - Manual memory management
        
    - Low-level operations
        

Why it mattered:

- Portable but efficient.
    
- Still foundational for system software.
    

---

## 3.5 Web Software

Modern web systems combine:

- Markup languages
    
- Scripting languages
    
- General-purpose languages
    

Examples:

- HTML – structures web pages
    
- PHP – server-side scripting
    
- Java – backend systems
    

Web development is multi-language by nature.

---

# 4. Language Categories by Level

Programming languages differ in abstraction level.

---

## 4.1 Machine Language

This is the lowest level.

- Binary instructions (0s and 1s).
    
- Specific to CPU architecture.
    
- Executed directly by hardware.
    

Problems:

- Extremely difficult to read.
    
- Hard to debug.
    
- Not portable.
    

---

## 4.2 Assembly Language

Assembly provides symbolic names for machine instructions.

Instead of:

```
10101010
```

You write:

```
MOV AX, BX
```

Still:

- Architecture-specific.
    
- Requires knowledge of registers and memory.
    

Advantages:

- Faster than high-level languages.
    
- More control over hardware.
    

---

## 4.3 High-Level Languages

These are machine-independent.

They provide:

- Variables
    
- Data types
    
- Functions
    
- Loops
    
- Conditionals
    
- Complex expressions
    
- Structured programs
    

Example expression:

```
2 * (y^5) >= 88 && sqrt(4.8) / 2 % 3 == 9
```

Advantages:

- Readability
    
- Maintainability
    
- Portability
    
- Faster development
    

Trade-off:

- Slightly less hardware control.
    

---

# 5. System Programming vs Application Programming

**System Programming**

- Focuses on managing computer resources.
    
- Memory management.
    
- Process scheduling.
    
- I/O control.
    

Languages: C, C++, Ada.

**Application Programming**

- Focuses on solving user problems.
    
- Web apps, databases, mobile apps.
    
- Often higher-level abstractions.
    

---

# 6. Scripting Languages

Scripting languages are used for:

- Automation
    
- Text processing
    
- System administration
    
- Connecting applications together
    

Examples:

- Python
    
- PHP
    

Characteristics:

- Often interpreted (executed line-by-line).
    
- Strong string processing.
    
- Rapid development.
    

Difference from compiled languages:

- No separate compilation step.
    
- Slower execution (traditionally).
    
- Faster development cycle.
    

---

# 7. Domain-Specific Languages (DSLs)

A DSL is designed for one narrow domain.

Example:

- PostScript
    

Used only for:

- Page layout
    
- Vector graphics
    
- Printing systems
    

Why DSLs exist:

- General-purpose languages may be too complex.
    
- DSLs increase productivity in a specific area.
    

---

# 8. Programming Paradigms

A **paradigm** is a way of thinking about programming.

---

## 8.1 Procedural Programming

Core idea:

> A program is a sequence of procedures that manipulate data.

Features:

- Variables
    
- Assignment
    
- Loops
    
- Conditionals
    
- Functions
    

Examples:

- C
    
- Java
    
- C++
    

Focus:

- Step-by-step instructions.
    

---

## 8.2 Functional Programming

Core idea:

> Computation is evaluation of mathematical functions.

Characteristics:

- No changing state (immutability).
    
- No side effects.
    
- Heavy use of recursion.
    

Examples:

- Haskell
    
- LISP
    
- F#
    

Advantages:

- Easier reasoning about code.
    
- Good for parallelism.
    

---

## 8.3 Logic Programming

Core idea:

> You describe rules and relationships, not steps.

Example:

- Prolog
    

You state facts and rules:

```
parent(john, mary).
```

The system infers answers.

Used in:

- AI
    
- Expert systems
    

---

# 9. Imperative vs Declarative

## Imperative

You specify:

- Exact steps
    
- How to do something
    

Example:

- C
    
- Java
    

Focus:

- State changes
    

---

## Declarative

You specify:

- What result you want
    
- Not how to compute it
    

Examples:

- Functional languages
    
- Logic languages
    

Focus:

- Expression of logic
    
- No explicit control flow
    

---

# 10. Most Influential Languages

## Fortran

- Showed high-level languages could replace assembly.
    

## COBOL

- Dominated business computing.
    

## ALGOL

- Introduced block structure.
    
- Influenced C, Pascal.
    

## Pascal

- Designed for teaching structured programming.
    
- Emphasised strong typing.
    

---

# Key Themes of This Lecture

1. Programming languages evolve to solve domain-specific problems.
    
2. Abstraction increases from machine code to high-level languages.
    
3. Paradigms affect how programmers think.
    
4. Imperative vs declarative is about _how_ vs _what_.
    
5. Certain languages shaped modern programming practice.
    
