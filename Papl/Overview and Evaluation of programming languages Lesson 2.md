## Lecture 02: Overview and Evaluation of Programming Languages

---

# 1. Lecture Overview

## Objectives

- Introduce the most influential programming languages
    
- Understand how programming languages are evaluated
    
- Focus on characteristics affecting:
    
    - Readability
        
    - Writability
        
    - Reliability
        
    - Cost
        

---

# 2. Most Influential Programming Languages

Several languages shaped modern programming practice:

- Fortran – Scientific computing
    
- COBOL – Business data processing
    
- Algol – Structured programming foundations
    
- Pascal – Teaching and structured design
    
- C – Systems programming
    
- Object-oriented languages (Simula → C++ → Java → C#)
    
- Scripting languages (Python, JavaScript, etc.)
    
- Logical languages (Prolog)
    

To compare languages, we use the **TPK Algorithm**.

---

# 3. The TPK Algorithm (Trabb Pardo–Knuth)

## What It Is

The TPK Algorithm is a small benchmark-style program designed in the 1970s for illustrating and comparing programming languages.

It is not meant to solve a real-world problem. Its purpose is educational.

---

## What the TPK Algorithm Does

1. Reads 11 numbers from input
    
2. Stores them in an array
    
3. Processes the array in reverse order
    
4. Applies the function:
    
    f(t) = sqrt(|t|) + 5t^3
    
5. For each result:
    
    - If result > 400 → print "TOO LARGE"
        
    - Otherwise → print the computed value
        

---

## Why It Is Used

### 1. Small but Non-Trivial

The algorithm includes:

- Input
    
- Arrays
    
- Reverse loops
    
- Function definitions
    
- Conditionals
    
- Mathematical computation
    
- Output formatting
    

It is more realistic than "Hello World" but still manageable.

### 2. Good for Comparing Language Features

Because the logic is fixed, we can compare:

- Syntax style
    
- Loop constructs
    
- Function definitions
    
- Type handling
    
- Readability
    
- Expressiveness
    

Example differences:

- C → explicit types and manual structure
    
- Python → concise and expressive
    
- Early Fortran → rigid formatting and implicit typing
    

### 3. Demonstrates Evaluation Criteria

It helps evaluate:

- Readability
    
- Writability
    
- Reliability
    
- Expressiveness
    

### 4. Shows Language Evolution

Implementing TPK across languages clearly shows evolution:

- Machine-oriented → Structured → Object-oriented → High-level expressive languages
    

---

# 4. Fortran

## Background

- Developed by John Backus at IBM
    
- First compiler released in 1957
    
- Designed for scientific computing
    
- Aimed to compete with assembly for speed
    

## Early Features

- Assignments
    
- DO loops
    
- GOTO
    
- Arithmetic IF
    
- Arrays
    
- Integers and reals
    

## Fixed Source Format (Early Versions)

Based on 80-column punch cards:

|Columns|Purpose|
|---|---|
|1|Comment indicator (C)|
|1–5|Label field|
|6|Continuation|
|7–72|Statement|
|73–80|Ignored / ID|

Removed in Fortran 90 (free-form syntax).

## Other Characteristics

- Implicit typing (I–N = integer, others = real)
    
- Still used today in high-performance scientific computing
    

---

# 5. COBOL

## Background

- Created late 1950s
    
- Designed by US Department of Defense
    
- Focused on business data processing
    

## Key Feature: Verbosity

Example:

```
SUBTRACT TAX FROM GROSS-PAY GIVING NET-PAY.
```

## Advantages

- Intended to be readable by non-programmers
    

## Criticism

- Very long programs
    
- Verbosity does not always improve clarity
    

Still widely used in legacy business systems.

---

# 6. Algol

## Purpose

- Designed to overcome limitations of Fortran
    
- Highly influential language
    

## Major Contributions

- Backus–Naur Form (BNF) syntax notation
    
- Block structure
    
- Local variables
    
- Recursive procedures
    
- Structured if and for statements
    

Influenced Pascal, C, and Simula.

Limitation: Less efficient compilers than Fortran.

---

# 7. Pascal

## Background

- Derived from Algol
    
- Designed by Niklaus Wirth
    
- Popular as a teaching language in the 1970s
    

## Key Features

- Strong typing
    
- Structured programming style
    
- Clear program structure:
    
    - program
        
    - begin
        
    - end.
        

Later evolved into Object Pascal (Delphi).

---

# 8. C

## Background

- Developed at Bell Labs (1972)
    
- Created alongside UNIX
    

## Designed For

- Systems programming
    
- Operating systems
    
- Compilers
    

## Characteristics

- High-level constructs (loops, functions)
    
- Low-level memory manipulation
    
- Weak typing
    
- Very efficient
    

## Criticism

- Less readable than Pascal
    
- Error-prone due to weak typing
    

---

# 9. Object-Oriented Languages

## Origins

- Simula 67 introduced classes and objects
    

## Influential OOP Languages

- Smalltalk
    
- Eiffel
    
- C++
    
- Java
    
- C#
    

## Purpose of OOP

- Model real-world systems
    
- Improve abstraction
    
- Improve maintainability
    

---

# 10. Scripting Languages

Originally used for task automation, now general-purpose.

Examples:

- Python
    
- Perl
    
- Ruby
    
- PHP
    
- JavaScript
    
- MATLAB
    

## Characteristics

- Often dynamically typed
    
- Interpreted
    
- Simple syntax
    
- Highly expressive
    
- Fast to learn and write
    

---

# 11. Prolog (Logical Programming)

## Core Elements

- Variables (start with capital letter)
    
- Constants (atoms or integers)
    
- Structures (functor + arguments)
    

Programs consist of facts and rules.

Used for query-based reasoning and AI applications.

---

# 12. Language Evaluation Criteria

From Sebesta’s framework.

Languages are evaluated based on:

- Readability
    
- Writability
    
- Reliability
    
- Cost
    

---

# 13. Simplicity

## Definition

- Small number of constructs
    
- Clear syntax
    

Example (C increment styles):

```
i = i + 1;
i += 1;
i++;
++i;
```

Too many options may reduce readability.

Over-simplicity (e.g., assembly) also reduces readability.

---

# 14. Lexical Elements

Lexical elements = words and symbols in a language.

Issues affecting readability:

- Short variable name limits (e.g., Fortran 77: 6 characters)
    
- Symbol clarity (= vs ==)
    
- Unclear keywords (e.g., static)
    

Good lexical design improves readability.

---

# 15. Orthogonality

## Definition

A language is orthogonal if:

1. It has a small number of constructs
    
2. Constructs can be combined freely
    
3. All combinations are meaningful
    

## Benefits

- Fewer special cases
    
- Easier to learn
    
- Easier to read and write
    

---

# 16. Non-Orthogonality Examples

## Pascal

- set of char allowed
    
- set of integer not allowed
    
- Functions cannot return arrays
    

## Java

- Primitive types are not objects
    
- Generics do not work with primitives directly
    

Non-orthogonality reduces readability and writability.

---

# 17. Data Types

## Importance

- Rich set of data types improves clarity
    
- Boolean type improves readability
    

Example:

```
finished = 1;
finished = true;
```

Second version is clearer.

## Poor Design Example

Fortran 77 lacked record types, requiring parallel arrays:

```
number[]
name[]
balance[]
```

Harder to maintain and manage.

---

# 18. Expressiveness

Expressiveness = amount of code needed to perform a task.

Example:

C:

```
for (i = 0; i <= 10; i++)
```

Python:

```
a = [input() for i in range(11)]
```

More expressive languages:

- Reduce code length
    
- Improve productivity
    
- May reduce errors
    

---

# 19. Summary

## Language Evolution

1. Scientific → Fortran
    
2. Business → COBOL
    
3. Structured → Algol, Pascal
    
4. Systems → C
    
5. Object-Oriented → Simula → C++ → Java → C#
    
6. Scripting → Python, JavaScript
    
7. Logic → Prolog
    

## Key Evaluation Criteria

- Simplicity
    
- Readability
    
- Orthogonality
    
- Data types
    
- Expressiveness
    

---


![[Pasted image 20260218215218.png]]