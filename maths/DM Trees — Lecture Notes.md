
## Definitions

> **Tree:** A connected graph that contains no cycles.

> **Spanning Tree:** A subgraph of a connected graph G that is a tree and includes every vertex of G.

> **Minimum Spanning Tree (MST):** A spanning tree of a weighted graph whose total edge weight is the smallest among all possible spanning trees.

> **Rooted Tree:** A tree in which one vertex is designated as the root.

> **Leaf (Terminal Vertex):** A vertex of degree 1 in a tree.

> **Parent:** A vertex that has one or more children (vertices directly below it in a rooted tree).

> **Child:** A vertex directly below another vertex in a rooted tree.

> **Siblings:** Vertices that share the same parent in a rooted tree.

---

## 1. What is a Tree?

> **Definition:** A tree is a connected graph that contains no cycles.

Trees are a subclass of graphs used extensively in computer science, chemistry, and linguistics (e.g. directory structures, family trees, tournament brackets).

### Alternative (Equivalent) Definitions

All three of the following statements about a graph G are equivalent:

1. G is a **tree**
2. G is **connected and acyclic** (no cycles)
3. Between any two vertices of G there is **precisely one path**

---

## 2. Key Properties

### Leaves

- A tree with more than one vertex **must contain a vertex of degree 1**
- This vertex is called a **leaf** (or terminal vertex)

### Edge Count Theorem

> **Theorem:** A connected graph with **n vertices** is a tree **if and only if** it has **n − 1 edges**.

This gives us two useful tools:

- If a connected graph with n vertices has n − 1 edges → it **must be a tree**
- If a tree has n vertices → it has **exactly n − 1 edges**

**Example:** A connected graph with degree sequence (1, 1, 2, 2, 2) has 5 vertices and 4 edges (by the Handshaking Lemma) → it must be a tree.

### Adding an Edge to a Tree

Adding any edge (without new vertices) to a tree **must create a cycle**, because:

- The original tree on n vertices had n − 1 edges
- The new graph still has n vertices but now n edges
- So it can no longer be a tree → a cycle must exist

---

## 3. Spanning Trees

> **Definition:** A **spanning tree** of a connected graph G is a subgraph that is a tree and includes **every vertex** of G.

- Spanning trees are **different** if they use different edges
- A connected graph can have **many** spanning trees

### How to Find a Spanning Tree

1. If G has no cycles, it is already a spanning tree
2. Otherwise: **delete an edge from a cycle** (without removing any vertex)
3. Repeat until no cycles remain → result is a spanning tree

---

## 4. Depth-First Search (DFS)

DFS is an algorithm used to find a spanning tree, test connectivity, and detect cycles.

### Steps

1. **Start** at any vertex (label it, e.g. label = 1)
2. Move to an **adjacent unlabelled vertex**, label it, repeat
3. When no unlabelled adjacent vertex exists → **backtrack** to the last labelled vertex that has an unlabelled neighbour
4. Finish when back at the starting vertex with no options left

### DFS to Build a Spanning Tree

- Every time a **new vertex is labelled**, add the edge used to reach it to the spanning tree T
- The result is a spanning tree T = (V, E)

### DFS Algorithm (Pseudocode)

```
Input:  Connected graph G with vertices v1, v2, ..., vn
Output: Spanning tree T = (V', E')

V' = {v1}, E' = ∅, w = v1

while (true):
    while (∃ edge wv such that adding wv doesn't create a cycle in T):
        choose vk with minimum index k
        E' = E' ∪ {wvk}, V' = V' ∪ {vk}, w = vk
    if w = v1:
        return T
    w = parent of w in T   // backtrack
```

---

## 5. Minimum Spanning Tree (MST)

Used for **weighted graphs**, where each edge has an assigned weight (e.g. distance).

> **Definition:** A **minimum spanning tree** is a spanning tree whose total edge weight is the **smallest among all spanning trees**.

Two classic greedy algorithms solve this problem:

---

### 5.1 Kruskal's Algorithm

A **greedy algorithm** — at each step, make the locally best choice without concern for future steps.

**Steps:**

1. Find the edge of **least weight** → call it e₁
2. Repeatedly add the next **lightest edge** that does **not create a cycle**
3. Stop when you have **n − 1 edges** (a spanning tree)

**Pseudocode:**

```
e1 = edge of minimum weight,  k = 1

while k < n:
    if ∃ edge e such that {e, e1, ..., ek} contains no circuit:
        ek+1 = lightest such edge
        k = k + 1
    else:
        output e1, e2, ..., ek and stop
```

---

### 5.2 Prim's Algorithm

Builds the MST by **expanding outward** from a starting vertex.

**Steps:**

1. Start with any single vertex in set W
2. Repeatedly add the **minimum weight edge** connecting a vertex in W to a vertex outside W
3. Stop when W = V (all vertices included)

**Pseudocode:**

```
T = ∅, W = {v}   (pick any starting vertex v)

while W ≠ V:
    find minimum weight edge {x, y} where x ∈ W, y ∉ W
    T = T ∪ {{x, y}}
    W = W ∪ {y}
```

---

### Kruskal's vs Prim's — Quick Comparison

|Feature|Kruskal's|Prim's|
|---|---|---|
|Approach|Edge-based|Vertex-based|
|Starts with|Lightest edge globally|Any single vertex|
|Grows by|Adding globally cheapest safe edge|Expanding outward from current tree|
|Best for|Sparse graphs|Dense graphs|

---

## 6. Rooted Trees

> A tree is **rooted** if one vertex is designated as the **root**.

In computer science, trees are typically drawn with the root at the top, growing downwards.

### Terminology

|Term|Definition|
|---|---|
|**Root**|The designated top/starting vertex|
|**Leaf**|A vertex with no children (degree 1, except possibly the root)|
|**Child**|A vertex directly below another vertex|
|**Parent**|A vertex directly above its children|
|**Siblings**|Vertices that share the same parent|

**Example:** In a tree rooted at B with children A, G, H, C:

- A, G, H, C are **siblings**
- B is the **parent** of A, G, H, C
- E and F are **children** of A

---

## 7. Key Terms Summary

- **Tree** — connected, acyclic graph
- **Leaf** — vertex of degree 1
- **Spanning tree** — a tree subgraph containing all vertices
- **Minimum spanning tree (MST)** — spanning tree of least total weight
- **Depth-First Search (DFS)** — algorithm for traversal and spanning tree construction
- **Kruskal's algorithm** — greedy MST via globally cheapest edges
- **Prim's algorithm** — greedy MST via outward expansion
- **Root, parent, child, sibling** — rooted tree terminology