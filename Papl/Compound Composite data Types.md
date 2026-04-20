
## Compound / Composite Data Types

**Compound type** = a type built from multiple values of the same type (e.g., arrays)  
**Composite type** = a type built from multiple values, possibly of different types (e.g., records/structs)

---

## Most Common Types

- Arrays
- Strings (often seen as an array of chars)
- Records / Structs
- Variant Records

Records are not directly found in OO languages; classes can be seen as extensions of records.

---

## Arrays

Arrays are the most common compound/composite type.

Arrays have the following attributes:
- **Element type** — the type of each element (also the type of the composite type)
- **Index type** — integers are normally used, but other types are possible (e.g., enumerated types)
- **Number of elements** (or index range)

### Array Sizes: Static vs Dynamic

**Static arrays** — subscript ranges are statically bounded and storage is allocated at compile time.  
*Advantage:* efficient (no dynamic allocation needed).

**Stack-dynamic arrays** — subscript ranges are dynamically bound and storage is allocated at run-time. Lives on the stack; size is fixed once created.  
*Advantage:* flexibility — the size of the array may not be known until the array is used.

**Heap-dynamic arrays** — lives on the heap and can change size. More flexible, as they can grow and shrink during program execution.

---

## Data Organisation: Rectangular & Jagged Arrays

A **rectangular array** is one in which all rows have the same number of elements and all columns have the same number of elements.

```
num rows == num columns
```

A **jagged array** has rows with a varying number of elements (and has no concept of columns). Therefore, multi-dimensional jagged arrays are actually arrays of arrays.

Jagged arrays are more flexible and memory-efficient. For example, the second dimension of array `a` can be allocated separately:

```java
int[][] a = new int[3][];
a[0] = new int[1]; // first row has 1 element
a[1] = new int[2]; // second row has 2 elements
a[2] = new int[3]; // third row has 3 elements
```

If `a` is a large triangular array, almost half the memory can be saved compared to a rectangular array.

A **heterogeneous array** is one where the elements do not all need to be of the same type.

---

## Records

A record is a composite type made up of a fixed number of named elements called **fields**, which can each be of a different type. Unlike arrays (which are homogeneous — all elements are the same type), records are **heterogeneous** — each field can hold a different type.

Records are found in languages like Pascal, Ada, and COBOL. In C/C++ the equivalent is a `struct`; in OO languages, records are replaced by classes.

```pascal
{ Pascal example }
type Student = record
    name    : string;
    age     : integer;
    gpa     : real;
end;
```

```c
/* C equivalent using struct */
struct Student {
    char name[50];
    int age;
    float gpa;
};
```

### Field Access

Fields are accessed by name using dot notation:

```c
struct Student s;
s.age = 21;
s.gpa = 3.7;
```

This is in contrast to arrays, where elements are accessed by index (`a[0]`, `a[1]`, etc.).

### Memory Layout

Fields of a record are stored **contiguously in memory**, in the order they are declared. However, the compiler may insert **padding** between fields to satisfy alignment requirements.

```
| name (50 bytes) | [2 bytes padding] | age (4 bytes) | gpa (4 bytes) |
```

This means the size of a record in memory may be larger than the sum of its field sizes.

### Records vs Arrays

| Feature       | Array                  | Record                     |
|---------------|------------------------|----------------------------|
| Element types | All the same (homogeneous) | Can differ (heterogeneous) |
| Access        | By index (`a[i]`)      | By name (`s.field`)        |
| Size          | Variable (can be large) | Typically small, fixed     |
| Use case      | Collection of similar items | Grouping related data  |

### Structs vs Classes

Structurally, structs are similar to classes (without constructors). "Member function" is an alternative term for "method".

---

## Classes

A class is an extension of a record — it bundles data (fields/attributes) together with the operations that act on that data (methods). This is the foundation of object-oriented programming.

Key additions classes have over records/structs:
- **Encapsulation** — access to fields and methods can be restricted using access modifiers (`public`, `private`, `protected`)
- **Constructors** — special methods that initialise an object when it is created
- **Methods** — functions that belong to the class and operate on its data
- **Inheritance** — a class can extend another class, inheriting its fields and methods
- **Polymorphism** — objects of different classes can be treated as instances of a common parent class

### Objects vs Classes

A **class** is the type definition (the blueprint). An **object** (or instance) is a value of that type, created at runtime.

```java
class Student {
    private String name;
    private boolean graduated;

    public Student(String name) { // constructor
        this.name = name;
        this.graduated = false;
    }

    public void graduate() {      // method
        this.graduated = true;
    }
}

Student s = new Student("Alice"); // object (instance of Student)
```

### Access Modifiers

| Modifier    | Accessible from                        |
|-------------|----------------------------------------|
| `public`    | Anywhere                               |
| `protected` | Same class, subclasses, same package   |
| `private`   | Same class only                        |

### Classes vs Structs (recap)

| Feature        | Struct (C/C++) | Class (OO languages) |
|----------------|----------------|----------------------|
| Access control | All public by default | public/private/protected |
| Methods        | Possible in C++ | Yes                  |
| Constructors   | No (C), Yes (C++) | Yes                |
| Inheritance    | Limited (C++)  | Yes                  |

---

## Variant Records

Records can be inflexible and memory-inefficient because all values of a record type have a fixed set of fields. With variant records, the set of available data can change based on some other property. For example, a student's data could use different fields based on whether they have graduated yet.

---

## Unions

C/C++ has unions instead of variant records. Unions are designed for storing data items of multiple types in the same memory space.

```c
typedef enum { INTEGER, DOUBLE } MyType;

typedef struct {
    MyType a_type;
    union {
        int i;
        double d;
    } myUnion;
} Value;
```

Usage:

```c
Value v;
v.a_type = INTEGER;
v.myUnion.i = 5;
// or
v.a_type = DOUBLE;
v.myUnion.d = 5.4321;
```

Here, `union` provides storage for either an integer (`5`) or a double (`5.4321`), but not both at the same time.
