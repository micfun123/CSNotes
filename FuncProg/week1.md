# Introduction to Functional Programming

**Weekly Practical Worksheets = 15 marks**

## Programming Paradigms

A **programming paradigm** is a style of programming and program execution that provides a fundamental approach to building software.

---

## Imperative Programming

Imperative programming is a style of programming where:

- Computation consists of executing statements
- Statements operate on a program state
- The program state changes over time

**Changing the state is an example of a side effect.**

Side effects are not always desirable because they:

- Make programs harder to reason about
- Make debugging more difficult
- Make testing more complex
- Can introduce bugs when order of execution matters

### State Examples

**Python (Imperative):**

```python
# Example 1: Counter with mutable state
counter = 0

def increment():
    global counter
    counter += 1  # Side effect: modifies global state
    return counter

print(increment())  # 1
print(increment())  # 2
print(increment())  # 3
```

```python
# Example 2: List modification
numbers = [1, 2, 3]

def add_number(n):
    numbers.append(n)  # Side effect: modifies the list
    return numbers

print(add_number(4))  # [1, 2, 3, 4]
print(add_number(5))  # [1, 2, 3, 4, 5]
```

**Haskell (Note: Pure functional, shown for comparison):**

```haskell
-- Haskell doesn't allow mutable state in pure functions
-- Instead, we pass state explicitly and return new state

increment :: Int -> Int
increment counter = counter + 1

-- Usage:
-- increment 0  -- Returns 1
-- increment 1  -- Returns 2
-- increment 2  -- Returns 3

-- For lists, we create new lists rather than modifying
addNumber :: Int -> [Int] -> [Int]
addNumber n numbers = numbers ++ [n]

-- Usage:
-- addNumber 4 [1,2,3]  -- Returns [1,2,3,4]
-- addNumber 5 [1,2,3,4]  -- Returns [1,2,3,4,5]
```

---

## Functional Programming

In contrast to imperative programming, functional programming is characterized by:

- **No statements** – only expressions that evaluate to values
- **No mutable state** – data is immutable
- **No side effects** – functions don't modify external state
- **Collection of stateless functions** – functions depend only on their inputs

### Core Principles

1. **Pure Functions**: Output depends only on input, no side effects
2. **Immutability**: Data cannot be changed after creation
3. **First-class Functions**: Functions can be passed as arguments and returned as values
4. **Higher-order Functions**: Functions that take other functions as parameters
5. **Referential Transparency**: Same input always produces same output

### Examples of Pure vs Impure Functions

**Python:**

```python
# IMPURE: Uses external state
total = 0
def add_to_total(x):
    global total
    total += x
    return total

# PURE: No side effects, same input = same output
def add(x, y):
    return x + y

# PURE: Even with lists, we don't modify the original
def append_pure(lst, item):
    return lst + [item]  # Creates new list
```

**Haskell:**

```haskell
-- All Haskell functions are pure by default

-- Pure function: adds two numbers
add :: Int -> Int -> Int
add x y = x + y

-- Pure function: appends to list (creates new list)
appendPure :: [a] -> a -> [a]
appendPure lst item = lst ++ [item]

-- Pure function: doubles each element
doubleAll :: [Int] -> [Int]
doubleAll lst = map (*2) lst
```

---

## Key Definitions

### Arguments

**Definition**: The data coming into a function.

Also called **parameters** or **inputs**.

**Python:**

```python
def greet(name, age):  # 'name' and 'age' are parameters
    return f"Hello {name}, you are {age} years old"

greet("Alice", 25)  # "Alice" and 25 are arguments
```

**Haskell:**

```haskell
-- 'name' and 'age' are parameters
greet :: String -> Int -> String
greet name age = "Hello " ++ name ++ ", you are " ++ show age ++ " years old"

-- Usage: greet "Alice" 25
```

---

### Expression

**Definition**: A piece of code that evaluates to a value.

Expressions can be combined to create larger expressions.

**Python:**

```python
# Simple expressions
5 + 3                    # Evaluates to 8
"Hello" + " World"       # Evaluates to "Hello World"
max(10, 20)              # Evaluates to 20

# Complex expressions
(5 + 3) * 2 if True else 0   # Evaluates to 16

# Function as expression
lambda x: x * 2          # Anonymous function expression
```

**Haskell:**

```haskell
-- Simple expressions
5 + 3                    -- Evaluates to 8
"Hello" ++ " World"      -- Evaluates to "Hello World"
max 10 20                -- Evaluates to 20

-- Complex expressions
if True then (5 + 3) * 2 else 0  -- Evaluates to 16

-- Function as expression
\x -> x * 2              -- Anonymous function (lambda)
```

---

### Value

**Definition**: A piece of data in its simplest, fully evaluated form.

Values are the end result of evaluating expressions.

**Examples of values:**

- Numbers: `42`, `3.14`
- Strings: `"Hello"`, `'World'`
- Booleans: `True`, `False`
- Lists: `[1, 2, 3]`

**Python:**

```python
# These are values
42
"Hello"
True
[1, 2, 3]

# These are expressions that evaluate to values
5 + 3           # Evaluates to the value 8
len([1, 2, 3])  # Evaluates to the value 3
```

**Haskell:**

```haskell
-- These are values
42
"Hello"
True
[1, 2, 3]

-- These are expressions that evaluate to values
5 + 3           -- Evaluates to the value 8
length [1,2,3]  -- Evaluates to the value 3
```

---

### Evaluation

**Definition**: The process of computing an expression to produce a value.

Evaluation follows specific rules depending on the programming language.

**Python:**

```python
# Step-by-step evaluation example
result = (2 + 3) * (4 - 1)

# Evaluation steps:
# 1. (2 + 3) * (4 - 1)
# 2. 5 * (4 - 1)
# 3. 5 * 3
# 4. 15

# Function evaluation
def square(x):
    return x * x

square(5)
# 1. square(5)
# 2. 5 * 5
# 3. 25
```

**Haskell:**

```haskell
-- Step-by-step evaluation example
result = (2 + 3) * (4 - 1)

-- Evaluation steps:
-- 1. (2 + 3) * (4 - 1)
-- 2. 5 * (4 - 1)
-- 3. 5 * 3
-- 4. 15

-- Function evaluation
square :: Int -> Int
square x = x * x

-- square 5
-- 1. square 5
-- 2. 5 * 5
-- 3. 25
```

**Haskell uses lazy evaluation**: Expressions are not evaluated until their values are needed.

```haskell
-- Infinite list (only possible with lazy evaluation)
ones = 1 : ones  -- [1,1,1,1,1,...]

-- Only evaluates what's needed
take 5 ones  -- [1,1,1,1,1]
```

---

## Data Types

Data types specify what kind of values can be stored and manipulated in a program.

### Basic Data Types

#### Integers

Whole numbers without decimal points.

**Python:**

```python
x = 42
y = -17
z = 0

# Operations
print(x + y)    # 25
print(x * 2)    # 84
print(x // 5)   # 8 (integer division)
```

**Haskell:**

```haskell
x :: Int
x = 42

y :: Int
y = -17

z :: Int
z = 0

-- Operations
x + y    -- 25
x * 2    -- 84
x `div` 5  -- 8 (integer division)
```

---

#### Floating Point Numbers

Numbers with decimal points.

**Python:**

```python
pi = 3.14159
temperature = -5.5

# Operations
print(pi * 2)           # 6.28318
print(temperature + 10) # 4.5
```

**Haskell:**

```haskell
pi :: Float
pi = 3.14159

temperature :: Float
temperature = -5.5

-- Operations
pi * 2           -- 6.28318
temperature + 10 -- 4.5
```

---

#### Booleans

Truth values: `True` or `False`.

**Python:**

```python
is_valid = True
is_empty = False

# Boolean operations
print(True and False)   # False
print(True or False)    # True
print(not True)         # False

# Comparison
print(5 > 3)           # True
print(10 == 10)        # True
```

**Haskell:**

```haskell
isValid :: Bool
isValid = True

isEmpty :: Bool
isEmpty = False

-- Boolean operations
True && False   -- False (AND)
True || False   -- True (OR)
not True        -- False

-- Comparison
5 > 3          -- True
10 == 10       -- True
```

---

#### Strings

Sequences of characters.

**Python:**

```python
greeting = "Hello"
name = 'Alice'

# String operations
print(greeting + " " + name)  # "Hello Alice"
print(len(greeting))          # 5
print(greeting[0])            # "H"
print(greeting.upper())       # "HELLO"
```

**Haskell:**

```haskell
greeting :: String
greeting = "Hello"

name :: String
name = "Alice"

-- String operations
greeting ++ " " ++ name  -- "Hello Alice"
length greeting          -- 5
head greeting            -- 'H'
map toUpper greeting     -- "HELLO" (need to import Data.Char)
```

---

#### Characters

Single characters.

**Python:**

```python
letter = 'A'
symbol = '$'

# Character operations
print(ord('A'))        # 65 (ASCII value)
print(chr(65))         # 'A'
print('A' < 'B')       # True
```

**Haskell:**

```haskell
letter :: Char
letter = 'A'

symbol :: Char
symbol = '$'

-- Character operations
ord 'A'       -- 65 (need to import Data.Char)
chr 65        -- 'A'
'A' < 'B'     -- True
```

---

### Composite Data Types

#### Lists

Ordered collections of elements of the same type.

**Python:**

```python
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
empty = []

# List operations
print(numbers[0])           # 1 (first element)
print(numbers[-1])          # 5 (last element)
print(len(numbers))         # 5
print(numbers + [6, 7])     # [1, 2, 3, 4, 5, 6, 7]

# Functional operations
print(list(map(lambda x: x * 2, numbers)))    # [2, 4, 6, 8, 10]
print(list(filter(lambda x: x > 3, numbers))) # [4, 5]
```

**Haskell:**

```haskell
numbers :: [Int]
numbers = [1, 2, 3, 4, 5]

names :: [String]
names = ["Alice", "Bob", "Charlie"]

empty :: [a]  -- Polymorphic empty list
empty = []

-- List operations
head numbers        -- 1 (first element)
last numbers        -- 5 (last element)
length numbers      -- 5
numbers ++ [6, 7]   -- [1, 2, 3, 4, 5, 6, 7]

-- List construction with cons operator
1 : [2, 3, 4, 5]    -- [1, 2, 3, 4, 5]

-- Functional operations
map (*2) numbers          -- [2, 4, 6, 8, 10]
filter (>3) numbers       -- [4, 5]
```

---

#### Tuples

Fixed-size collections that can contain elements of different types.

**Python:**

```python
point = (3, 4)
person = ("Alice", 25, True)

# Tuple operations
print(point[0])        # 3
print(person[1])       # 25
print(len(person))     # 3

# Unpacking
x, y = point
name, age, active = person
```

**Haskell:**

```haskell
point :: (Int, Int)
point = (3, 4)

person :: (String, Int, Bool)
person = ("Alice", 25, True)

-- Tuple operations (for pairs)
fst point        -- 3 (first element of pair)
snd point        -- 4 (second element of pair)

-- Pattern matching for unpacking
getX :: (Int, Int) -> Int
getX (x, y) = x

getName :: (String, Int, Bool) -> String
getName (name, age, active) = name
```

---

### Type Annotations

**Python (Type hints - optional):**

```python
from typing import List, Tuple

def add(x: int, y: int) -> int:
    return x + y

def get_names(people: List[Tuple[str, int]]) -> List[str]:
    return [name for name, age in people]

# Without type hints, Python is dynamically typed
def multiply(a, b):  # Types inferred at runtime
    return a * b
```

**Haskell (Type signatures - strongly encouraged):**

```haskell
-- Type signatures are explicit
add :: Int -> Int -> Int
add x y = x + y

-- More complex type
getNames :: [(String, Int)] -> [String]
getNames people = [name | (name, age) <- people]

-- Polymorphic types (works with any type)
identity :: a -> a
identity x = x

myLength :: [a] -> Int
myLength [] = 0
myLength (x:xs) = 1 + myLength xs
```

---

## Higher-Order Functions

Functions that take other functions as arguments or return functions.

### Map

Apply a function to every element in a list.

**Python:**

```python
numbers = [1, 2, 3, 4, 5]

# Using map
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]

# List comprehension (Pythonic alternative)
doubled = [x * 2 for x in numbers]
```

**Haskell:**

```haskell
numbers :: [Int]
numbers = [1, 2, 3, 4, 5]

-- Using map
doubled :: [Int]
doubled = map (*2) numbers  -- [2, 4, 6, 8, 10]

-- List comprehension
doubled2 :: [Int]
doubled2 = [x * 2 | x <- numbers]
```

---

### Filter

Select elements from a list that satisfy a predicate.

**Python:**

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

# Using filter
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8]

# List comprehension
evens = [x for x in numbers if x % 2 == 0]
```

**Haskell:**

```haskell
numbers :: [Int]
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

-- Using filter
evens :: [Int]
evens = filter even numbers  -- [2, 4, 6, 8]

-- List comprehension
evens2 :: [Int]
evens2 = [x | x <- numbers, even x]
```

---

### Reduce/Fold

Combine all elements of a list into a single value.

**Python:**

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
total = reduce(lambda acc, x: acc + x, numbers, 0)
print(total)  # 15

# Product of all numbers
product = reduce(lambda acc, x: acc * x, numbers, 1)
print(product)  # 120
```

**Haskell:**

```haskell
numbers :: [Int]
numbers = [1, 2, 3, 4, 5]

-- Left fold
total :: Int
total = foldl (+) 0 numbers  -- 15

-- Right fold
product :: Int
product = foldr (*) 1 numbers  -- 120

-- Manually implementing fold
mySum :: [Int] -> Int
mySum [] = 0
mySum (x:xs) = x + mySum xs
```

---

## Recursion

Recursion is a fundamental technique in functional programming where a function calls itself.

### Factorial Example

**Python:**

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120
```

**Haskell:**

```haskell
factorial :: Int -> Int
factorial 0 = 1
factorial n = n * factorial (n - 1)

-- factorial 5 = 120
```

### List Sum Example

**Python:**

```python
def sum_list(lst):
    if not lst:
        return 0
    else:
        return lst[0] + sum_list(lst[1:])

print(sum_list([1, 2, 3, 4, 5]))  # 15
```

**Haskell:**

```haskell
sumList :: [Int] -> Int
sumList [] = 0
sumList (x:xs) = x + sumList xs

-- sumList [1, 2, 3, 4, 5] = 15
```

---

## Pattern Matching

Pattern matching allows you to destructure data and handle different cases elegantly.

**Python (limited pattern matching):**

```python
# Python 3.10+ has match statements
def describe_list(lst):
    match lst:
        case []:
            return "Empty list"
        case [x]:
            return f"Single element: {x}"
        case [x, y]:
            return f"Two elements: {x} and {y}"
        case _:
            return f"Multiple elements, first is {lst[0]}"

# Traditional approach
def get_first(lst):
    if not lst:
        return None
    return lst[0]
```

**Haskell:**

```haskell
-- Pattern matching on lists
describeList :: [a] -> String
describeList [] = "Empty list"
describeList [x] = "Single element"
describeList [x, y] = "Two elements"
describeList (x:xs) = "Multiple elements, first is x"

-- Pattern matching on tuples
getFirst :: (a, b) -> a
getFirst (x, y) = x

-- Pattern matching with guards
classify :: Int -> String
classify n
    | n < 0     = "Negative"
    | n == 0    = "Zero"
    | otherwise = "Positive"
```

---

## Lambda Functions (Anonymous Functions)

Functions without names, useful for short, one-off operations.

**Python:**

```python
# Lambda syntax: lambda arguments: expression
square = lambda x: x * x
add = lambda x, y: x + y

print(square(5))    # 25
print(add(3, 4))    # 7

# Common use in higher-order functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
```

**Haskell:**

```haskell
-- Lambda syntax: \arguments -> expression
square = \x -> x * x
add = \x y -> x + y

-- square 5    = 25
-- add 3 4     = 7

-- Common use in higher-order functions
numbers = [1, 2, 3, 4, 5]
squared = map (\x -> x ^ 2) numbers
```

---

## Function Composition

Combining simple functions to build more complex operations.

**Python:**

```python
def compose(f, g):
    return lambda x: f(g(x))

# Individual functions
def add_one(x):
    return x + 1

def double(x):
    return x * 2

# Composed function
add_then_double = compose(double, add_one)
print(add_then_double(5))  # (5 + 1) * 2 = 12
```

**Haskell:**

```haskell
-- Built-in composition operator (.)
addOne :: Int -> Int
addOne x = x + 1

double :: Int -> Int
double x = x * 2

-- Composed function
addThenDouble :: Int -> Int
addThenDouble = double . addOne

-- addThenDouble 5 = (5 + 1) * 2 = 12

-- Chaining multiple compositions
process :: Int -> Int
process = (+10) . (*2) . (+1)
-- process 5 = ((5 + 1) * 2) + 10 = 22
```

---

## Currying

Converting a function that takes multiple arguments into a sequence of functions each taking a single argument.

**Python:**

```python
# Manual currying
def add_curried(x):
    def inner(y):
        return x + y
    return inner

add_5 = add_curried(5)
print(add_5(3))  # 8

# Using functools
from functools import partial

def multiply(x, y, z):
    return x * y * z

double_and = partial(multiply, 2)
print(double_and(3, 4))  # 2 * 3 * 4 = 24
```

**Haskell:**

```haskell
-- Haskell functions are curried by default!
add :: Int -> Int -> Int
add x y = x + y

-- Partial application
add5 :: Int -> Int
add5 = add 5

-- add5 3 = 8

-- Another example
multiply :: Int -> Int -> Int -> Int
multiply x y z = x * y * z

doubleAnd :: Int -> Int -> Int
doubleAnd = multiply 2

-- doubleAnd 3 4 = 24
```

---

## Advantages of Functional Programming

1. **Easier to Reason About**: No hidden state means you can understand functions in isolation
2. **Easier to Test**: Pure functions always give the same output for the same input
3. **Easier to Debug**: No side effects means fewer sources of bugs
4. **Parallelization**: Pure functions can be safely executed in parallel
5. **Modularity**: Functions can be easily composed and reused
6. **Referential Transparency**: Expressions can be replaced with their values without changing program behavior

---

## Comparison Summary

|Feature|Imperative|Functional|
|---|---|---|
|**State**|Mutable|Immutable|
|**Execution**|Statements|Expressions|
|**Side Effects**|Common|Avoided|
|**Control Flow**|Loops, conditionals|Recursion, higher-order functions|
|**Focus**|How to do it|What to do|

---

## Practice Exercises

### Exercise 1: Write a function to find the maximum element in a list

**Python:**

```python
# Imperative approach
def find_max_imperative(lst):
    max_val = lst[0]
    for num in lst:
        if num > max_val:
            max_val = num
    return max_val

# Functional approach
def find_max_functional(lst):
    if len(lst) == 1:
        return lst[0]
    return max(lst[0], find_max_functional(lst[1:]))

# Using built-in
result = max([3, 7, 2, 9, 1])
```

**Haskell:**

```haskell
-- Pattern matching and recursion
findMax :: [Int] -> Int
findMax [x] = x
findMax (x:xs) = max x (findMax xs)

-- Using built-in
result = maximum [3, 7, 2, 9, 1]
```

### Exercise 2: Reverse a list

**Python:**

```python
# Functional approach
def reverse_list(lst):
    if not lst:
        return []
    return reverse_list(lst[1:]) + [lst[0]]

print(reverse_list([1, 2, 3, 4]))  # [4, 3, 2, 1]
```

**Haskell:**

```haskell
reverseList :: [a] -> [a]
reverseList [] = []
reverseList (x:xs) = reverseList xs ++ [x]

-- reverseList [1, 2, 3, 4] = [4, 3, 2, 1]
```

### Exercise 3: Calculate the length of a list

**Python:**

```python
def length(lst):
    if not lst:
        return 0
    return 1 + length(lst[1:])

print(length([1, 2, 3, 4, 5]))  # 5
```

**Haskell:**

```haskell
myLength :: [a] -> Int
myLength [] = 0
myLength (x:xs) = 1 + myLength xs

-- myLength [1, 2, 3, 4, 5] = 5
```

---

## Additional Resources

- **Python Functional Programming**: `functools`, `itertools` modules
- **Haskell**: Learn You a Haskell for Great Good! (online book)
- **Practice**: Try implementing more list operations functionally (flatten, zip, take, drop)

---

## Notes for Weekly Practicals

Remember:

- Practice writing pure functions
- Avoid using loops; use recursion or higher-order functions instead
- Think in terms of transforming data, not modifying state
- Test your functions with different inputs
- Compare imperative vs functional approaches

**Weekly Practical Worksheets = 15 marks**

- Complete all exercises
- Submit functional implementations
- Include both Python and Haskell code where requested