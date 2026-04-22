
An expression is a combination of values, variables, operators and function calls. Expressions perform operations on data and move data around.

Types of expressions:
- Arithmetic expression
- Relational expression
- Boolean expression
- Assignment

To correctly evaluate expressions, we need to know the rules of precedence and the rules of associativity of operators.

## Arithmetic Expressions

Arithmetic evaluation was one of the motivations for the development of the first programming languages. Arithmetic expressions consist of operators, operands, parentheses, and function calls.


## Operators

- A **unary operator** has one operand.
  - Negation operator `-`: `-b` where `-` is the operator and `b` is the operand
  - (Integer) promotion operator `+`: `+b` converts `b` to int if it is a short, byte, or char
- When operators precede (or follow) their operands, we say the operators are **prefix** (or **postfix**). Unary operators can be prefix or postfix. E.g., increment operator `++`: `++i` and `i++`
- A **binary operator** has two operands. E.g., `+`, `-`, `*`, `/`
- In most languages, binary operators are **infix**, meaning they appear between their operands.


## Operator Associativity Rules

Operator associativity is a property that determines how operators of the same precedence are grouped in the absence of parentheses.

Which operand an operator applies to is determined by the associativity of the operators.

Operations may be:
- **Associative** — the operation can be grouped arbitrarily, e.g., `a*b*c` could be `a*(b*c)` or `(a*b)*c`
- **Left-associative** — operations are grouped from the left
- **Right-associative** — operations are grouped from the right

Some mathematical operators have inherent associativity:
- Subtraction (`-`) and division (`/`) are inherently left-associative.
- Addition (`+`) and multiplication (`*`) are both left and right associative. E.g., `(a * b) * c = a * (b * c)`.


## Prefix Notation

In prefix notation, operators appear before their operands.

For example, the infix expression `a+b-c*d` would be written in prefix form as:
```
-+ab*cd
```
It is evaluated left to right by combining two operands with the operator in front of them:
```
-(+ab)*cd  →  -(+ab)(*cd)  →  (-(+ab)(*cd))
```
Prefix notation is inherently unambiguous.


## Postfix Notation

In postfix notation, operators appear after their operands.

The expression `a+b-c*d` in postfix would be written as:
```
ab+cd*-   or   abcd*-+
```
It is evaluated left to right by combining two operands with the operator after them:
```
(ab+)(cd*)-  →  ((ab+)(cd*)-)
```
Postscript (printer control language) uses this notation.


## Cambridge Prefix Notation

Cambridge notation introduces parentheses into prefix notation.

E.g., `a+b-c*d` would be written as:
```
(-(+ab)(*cd))
```
An advantage: it makes operators like `+` and `-` n-ary. E.g., `a+b+c+d` would be written as `(+abcd)`.

Lisp uses this notation.


## Operator Overloading

Use of an operator for more than one purpose is called **operator overloading**.

- E.g., in Java, `+` is used for `int` and `float` addition but is also the string concatenation operator.
  - The semantics of the operator can be inferred from program context.
- C++ and C# allow user-defined overloaded operators.
  - When used sensibly, such operators can aid readability (avoid method calls, expressions appear natural).
- Overloading can cause problems:
  - E.g., ampersand `&` in C and C++ specifies both bitwise AND (binary) and "address of" (unary) operations.
  - Compiler error detection may be affected (e.g., missing operand `x` in `x&y`).


## Side Effects of Expressions

An expression has a **side effect** if, in addition to returning a value, it also modifies variables or causes something else to happen.

Side effects arise when an expression involves:
- an assignment
- increment/decrement operations
- a function call, or
- a method invocation

In the presence of side effects, a program's behavior may depend on execution history; the order of evaluation matters. Sometimes the side effect is exactly what we want, e.g., in an assignment.


## Assignment as an Expression

In C-based languages (e.g., Java, Perl, JavaScript), the assignment operator `=` is treated like other binary operators (e.g., `+`).

- Assignment returns a value, but has the side effect of changing its left operand.
- For example, the expression `x = y + 1;` returns a value equal to the value assigned to `x`, and the actual assignment to `x` is (just) a side effect.


## Use/Abuse of Assignment as an Expression

In the following statement:
```c
while ((ch = getchar()) != EOF) { … }
```
`ch = getchar()` is an expression (assignment) that returns a value and also assigns a value to `ch`.

Such uses may cause loss of error detection. E.g., in C:
```c
if (x = y) …    // assignment — returned numeric value used as boolean
```
instead of:
```c
if (x == y) …   // relational expression
```
This mistake is not detectable by the compiler.


## Compound Assignment Operators

Compound assignment combines assignment with arithmetic operators: `+=`, `-=`, `*=`, `/=`, `<<=`, etc. General form: `operator=`

It is a shorthand for a commonly needed form of assignment. Introduced in ALGOL; adopted by C and C-based languages.

E.g., `a = a + b` can be written as `a += b`.

Normally `a += b` has the same effect as `a = a + b`, but consider:
```c
a[i++] *= 2;        // index i++ evaluated once
a[i++] = a[i++] * 2;  // i++ (and a) evaluated twice
```
In `a[i++] *= 2`, index `i++` is evaluated once. In `a[i++] = a[i++] * 2`, the evaluation order is:
1. `i++` in `a[i++]` on the right-hand side is evaluated; value of `a[i++]` is retrieved; multiplication performed
2. `i++` in `a[i++]` on the left is evaluated; assignment performed


## Unary Assignment Operators (Short-Circuit Evaluation)

Consider a Java loop searching for `aValueToFind` in a list:
```java
index = 0;
while (index < length && list[index] != aValueToFind)
    index++;
```
Without short-circuit evaluation (using `&` instead of `&&`), the right-hand relational expression is always evaluated:
```java
while (index < length & list[index] != aValueToFind)
```
This causes the program to terminate with a subscript out-of-range exception if the item is not in the list (when `index == length`).


## Potential Problems with Short-Circuit Evaluation

Short-circuit evaluation can allow subtle errors. E.g.:
```java
(a > b || b++ > 3)
```
- `b++ > 3` is only evaluated when `a > b` is false (i.e., `a <= b`).
- If the programmer assumes `b++ > 3` is evaluated every time, the program will behave incorrectly.
- The order expressions are written matters — short-circuit evaluation does not allow the compiler to reorder or prune expressions freely.
