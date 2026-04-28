
## Key Definitions

| Term                            | Definition                                                                                                                                                                                    |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Machine Language**            | The set of instructions a computer's processor can directly execute; the only language a computer understands without supporting software.                                                    |
| **Macroinstruction**            | A machine instruction implemented using a set of even lower-level instructions called microinstructions.                                                                                      |
| **Compiler**                    | A program that translates a source program written in a high-level language into an equivalent target program in a low-level language (e.g. machine code, assembly, or virtual machine code). |
| **Interpreter**                 | A program that directly executes source code written in a high-level language without first compiling it to machine language.                                                                 |
| **Hybrid Implementation**       | A system that compiles source code to an intermediate language, which is then interpreted by a virtual machine rather than compiled all the way to machine code.                              |
| **Just-In-Time (JIT) Compiler** | A system that compiles programs to intermediate code, then translates segments to machine code just before execution, caching the result for reuse.                                           |
| **Token**                       | A symbolic name representing a lexical element of the source language (e.g. `IF`, `IDENT`, `SEMICOLON`).                                                                                      |
| **Symbol Table**                | A data structure holding all identifiers in a source program, along with their attributes (type, size, scope, etc.).                                                                          |
| **Parse Tree**                  | A tree structure that represents the syntactic structure of a program as derived by the parser.                                                                                               |
| **Abstract Syntax Tree (AST)**  | A simplified version of a parse tree that still represents the program's syntactic structure, without redundant grammar nodes.                                                                |
| **Lexical Analysis**            | The first compiler phase; reads source text character by character and groups characters into tokens.                                                                                         |
| **Syntax Analysis (Parsing)**   | The second compiler phase; takes the token stream and checks that it conforms to the grammatical rules of the language, producing a parse tree / AST.                                         |
| **Semantic Analysis**           | The third compiler phase; checks that the program is semantically valid (e.g. correct types, correct number of arguments) using the AST and symbol table.                                     |
| **Code Optimisation**           | A compiler phase that improves the time and/or space efficiency of the program (e.g. constant folding, dead code elimination).                                                                |
| **Code Generation**             | The final compiler phase; produces the target program in machine language, assembly, or virtual machine code.                                                                                 |
| **Virtual Computer**            | The combination of a language implementation and an operating system, which together simulate a machine that "natively" runs a given language.                                                |

---

## 1. Layered View of a Computer

![[Pasted image 20260127140521.png]]

Computers are built in layers, from the hardware outward:

```
Bare Machine
    └── Macroinstruction Interpreter
        └── Operating System
            └── Language Implementations (Compilers / Interpreters)
                └── Virtual Computers (e.g. Virtual C Computer, Java Virtual Machine)
```

The OS is separated into several layers (0 to n). Rules for the layers:

1. The outermost layer must be the User Interface layer.
2. The innermost layer must be the Hardware layer.
3. A layer can access all layers below it but not above it (layer n−1 can access n−2 down to 0, but not n).

If the user layer wants to interact with the hardware layer, the request travels through all intermediate layers. Each layer is designed to need only services from the layers below it.

- The **bare machine** only understands its own machine language.
- The **operating system** sits above, providing higher-level primitives (I/O, file management, etc.).
- **Language implementations** sit on top of the OS.
- Each language implementation + OS = a **virtual computer** for that language (e.g. C compiler + OS = Virtual C Computer).

**Advantages:**

1. **Modularity** – each layer performs only its assigned tasks.
2. **Easy debugging** – errors can be isolated to a specific layer.
3. **Easy update** – a change in one layer does not affect others.
4. **No direct hardware access** – users use hardware services but cannot directly modify hardware.
5. **Abstraction** – each layer is concerned only with its own functions.

**Disadvantages:**

1. **Complex implementation** – layer ordering must be carefully planned (e.g. backing storage must sit below memory management).
2. **Slower execution** – requests travel through all intermediate layers, increasing response time.

---

## 2. The Three Implementation Methods

### 2.1 Compilation

- Translates the entire high-level source program into machine code **before** execution.
- Characteristic: **slow translation, fast execution**.
- Best for: large scientific or commercial applications.
- Includes **JIT** variants (see Section 5).

### 2.2 Pure Interpretation

- An interpreter reads and executes source code **directly**, statement by statement, with no prior translation.
- Characteristic: **slow execution** (every statement decoded every time it runs), **more memory** needed (source + symbol table must be present at runtime).
- Best for: small programs or where efficiency is not critical (e.g. web scripting).
- Examples: HTML & JavaScript, early LISP, early BASIC.

### 2.3 Hybrid Implementation

- Compiles source code to an **intermediate representation**, which is then **interpreted** by a virtual machine.
- Faster than pure interpretation; not as fast as full compilation.
- Best for: small to medium systems where efficiency is not the top priority.
- Examples: Perl, Python, MATLAB, Java (JDK 1.0).

> Compilation and interpretation are **not mutually exclusive** — most interpreting systems also perform some translation work.

---

## 3. Compilation in Detail

### 3.1 What is a Compiler?

![[Pasted image 20260202092334.png]]

```
Source Program  →  [ Compiler ]  →  Target Program
                         ↕
                   Error Messages
```

- Input (source): a **high-level** language program.
- Output (target): a **low-level** language program — machine code, assembly, or virtual machine bytecode.

---

### 3.2 Structure of a Compiler

The compiler is a **pipeline** of phases; the output of each phase feeds into the next. All phases interact with a shared **Symbol Table**.

![[Pasted image 20260202092409.png]]

```
Source Program
      ↓
 Lexical Analyser
      ↓
 Syntax Analyser
      ↓
 Semantic Analyser  ←→  Symbol Table
      ↓
 Code Optimiser
      ↓
 Code Generator
      ↓
Target Program
```

---

### 3.3 Phase 1 – Lexical Analysis (Scanning)

- Reads the source text **one character at a time**.
- Groups characters into **tokens** based on **patterns**.
- Whitespace and newlines are typically discarded (produce no token).

**Example – Pascal fragment `program foo; var x3:integer; begin ... end.`:**

| Program Text | Pattern Matched        | Token          |
| ------------ | ---------------------- | -------------- |
| `program`    | p, r, o, g, r, a, m   | `PROGRAM`      |
| (space)      | whitespace             | none           |
| `foo`        | letter + alphanumerics | `IDENT(foo)`   |
| `;`          | semicolon              | `SEMICOLON`    |
| `var`        | v, a, r                | `VAR`          |
| `x3`         | letter + alphanumerics | `IDENT(x3)`    |
| (end of file)| —                      | `ENDOFFILE`    |

---

### 3.4 The Symbol Table

- A data structure that stores all **identifiers** and their **attributes**.
- **Variable attributes:** type, size, scope.
- **Function/procedure attributes:** number of arguments, argument types, passing mechanisms, return type.
- Accessed and updated by **all phases** throughout compilation.

---

### 3.5 Phase 2 – Syntax Analysis (Parsing)

- Takes the token stream from the lexical analyser.
- Applies **grammar rules** of the language to check syntactic correctness.
- Produces a **parse tree** (or the simpler **Abstract Syntax Tree**).

**Example grammar rules:**

```
<assign> → <ident> := <exp>
<exp>    → <ident> | <ident> + <ident>
```

**Token stream for `x := y + z`:**

```
IDENT(x)  ASSIGN  IDENT(y)  PLUS  IDENT(z)
```

This produces a parse tree rooted at `<assign>` and the simpler AST:

```
      :=
     /   \
    x     +
         / \
        y   z
```

---

### 3.6 Phase 3 – Semantic Analysis

- Checks that the program is **semantically valid** (not just syntactically correct).
- Works from the **AST** and **Symbol Table**.
- A program can be syntactically correct but semantically wrong.

**Examples of semantic errors:**

- `y + z` where `y` is a `float` and `z` is a `string` → type mismatch.
- `doit(12, x, y, z)` where `doit` is declared to take only 3 arguments → wrong argument count.

---

### 3.7 Phase 4 – Code Optimisation

- Improves **time and/or space** efficiency of the program.
- Does **not** change the program's observable behaviour.

**Common optimisations:**

| Optimisation                  | Description                                    |
| ----------------------------- | ---------------------------------------------- |
| Constant folding              | Replace `3 + 7` with `10` at compile time      |
| Dead code elimination         | Remove code that can never be reached          |
| Flow-of-control optimisation  | Simplify unnecessary jumps                     |

---

### 3.8 Phase 5 – Code Generation

- Produces the final **target program** (machine code, assembly, or VM bytecode).
- Must decide:
  - **Instruction selection** – which machine instructions to use.
  - **Instruction scheduling** – the order of instructions.
  - **Register allocation** – which variables go in CPU registers.
  - **Debug data generation** – optional debug info.

---

## 4. Pure Interpretation – Summary

```
Source Program ─┐
                ↓
Input Data  → [Interpreter] → Results
```

**Advantages:**

- Flexible; no compilation step needed.
- Easier to implement dynamic features.

**Disadvantages:**

- Much slower execution (statement decoded on every execution).
- Higher memory usage (source code + symbol table must stay in memory at runtime).

---

## 5. Just-In-Time (JIT) Implementation

A refinement of hybrid systems:

1. Compile source to **intermediate code** (e.g. Java bytecode).
2. Load intermediate code into memory.
3. Translate **segments** (e.g. methods) to native machine code **just before** they execute.
4. **Cache** the machine code version for subsequent calls.

- Used by **Java** since JDK 1.1 — largely why Java became competitive with fully compiled languages.
- Also used by **.NET** languages (C#, VB.NET, etc.).

---

## 6. Quick Comparison Table

| Feature              | Compilation          | Pure Interpretation    | Hybrid                       | JIT                      |
| -------------------- | -------------------- | ---------------------- | ---------------------------- | ------------------------ |
| Translation timing   | Before execution     | During execution       | Partial (to intermediate)    | At runtime, on demand    |
| Execution speed      | Fast ✅              | Slow ❌                | Medium ⚠️                   | Fast ✅                  |
| Portability          | Low                  | High                   | High                         | High                     |
| Memory usage         | Lower                | Higher                 | Medium                       | Medium                   |
| Examples             | C, C++, Fortran      | Early BASIC, LISP      | Python, Perl, Java 1.0       | Java (1.1+), .NET        |
