# Discrete Mathematics – Walks, Trails, and Eulerian Graphs (Revision Notes)

---

## Definitions

| Term                    | Definition                                                                                                                                                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Walk**                | An alternating sequence of vertices and edges (beginning and ending with a vertex), where each edge is incident with the vertices immediately before and after it. Vertices and edges **may repeat**. Length = number of edges. |
| **Trail**               | A walk in which all **edges are distinct** (no edge repeated). Vertices may still repeat.                                                                                                                                       |
| **Path**                | A walk in which all **vertices are distinct** (and therefore all edges are distinct too).                                                                                                                                       |
| **Circuit**             | A **closed** walk (same start and end vertex) in which all edges are distinct. Also called a _closed trail_.                                                                                                                    |
| **Cycle**               | A **closed** walk in which all vertices (except first and last) are distinct. Also called a _closed path_.                                                                                                                      |
| **Connected Graph**     | A graph G is **connected** if there exists a path between any pair of vertices; **disconnected** otherwise.                                                                                                                     |
| **Bridge**              | An edge in a connected graph whose deletion would make the graph disconnected.                                                                                                                                                  |
| **Eulerian Graph**      | A graph containing an **Eulerian circuit** — a closed Trail (circuit) that uses every edge exactly once.                                                                                                                        |
| **Semi-Eulerian Graph** | A connected graph with exactly **two vertices of odd degree**. Contains an open Eulerian trail using every edge exactly once.                                                                                                   |
| **Hamiltonian Graph**   | A graph containing a **Hamiltonian cycle** — a closed path that visits every vertex exactly once.                                                                                                                               |
| **Adjacency Matrix**    | For a graph with n vertices v₁…vₙ, the n×n matrix A where aᵢⱼ = 1 if vᵢvⱼ is an edge, and 0 otherwise.                                                                                                                          |

---

## Quick Reference: Types of Walk

|Term|Vertices|Edges|Start/End|Open or Closed|
|---|---|---|---|---|
|Walk|May repeat|May repeat|Anywhere|Either|
|Trail|May repeat|No repeat|Anywhere|Either|
|Path|No repeat|No repeat|Anywhere|Open|
|Circuit|May repeat|No repeat|Same vertex|Closed|
|Cycle|No repeat|No repeat|Same vertex|Closed|

---

## Eulerian Graphs

### Characterisation Theorem

> **A multigraph is Eulerian if and only if it is connected and every vertex has even degree.**

### Intuition

An Eulerian circuit is like drawing a graph without lifting your pen and without covering any edge twice. At each vertex there must be one edge "in" and one edge "out" — so every vertex must have **even degree**.

### Fleury's Algorithm (finding an Eulerian circuit)

1. **Step 0:** Choose any vertex to start.
2. **Step 1:** From the current vertex, choose any edge to traverse — choosing a **bridge only if there is no other option**.
3. **Step 2:** Traverse that edge, erase it (and remove isolated vertices), move to the next vertex.
4. **Step 3:** Repeat Steps 1–2 until all edges are traversed. You should return to the starting vertex.

### Semi-Eulerian Graphs

- A connected graph with **exactly two odd-degree vertices** has an open Eulerian trail.
- The trail **must start and end at the two odd-degree vertices**.
- To find it: start at one odd-degree vertex, construct a circuit (adding a temporary edge between the two odd vertices), and the trail emerges naturally.

---

## Hamiltonian Graphs

### Comparison with Eulerian Graphs

||Eulerian|Hamiltonian|
|---|---|---|
|**Goal**|Every **edge** visited once|Every **vertex** visited once|
|**Characterisation**|Connected + all even degrees|No simple "iff" condition known|
|**Algorithm**|Efficient — Fleury's Algorithm|No efficient algorithm known — exhaustive search only|
|**Complexity**|Polynomial time|Exponential / factorial time (worst case)|

> **Bad news:** Finding a Hamiltonian cycle is computationally hard — this is why the **Travelling Salesman Problem** is also hard.

---

## Adjacency Matrix

### Definition

For a graph G with n vertices v₁, v₂, …, vₙ, the **adjacency matrix** A is the n×n matrix where:

$$a_{ij} = \begin{cases} 1 & \text{if } v_iv_j \text{ is an edge} \\ 0 & \text{if } v_iv_j \text{ is not an edge} \end{cases}$$

### Key Properties

- **Diagonal entries are all 0** — aᵢᵢ = 0 (no self-loops in a simple graph).
- **Symmetric** — aᵢⱼ = aⱼᵢ for all i, j.
- **deg(vᵢ)** = number of 1s in row i (or column i).

### Powers of the Adjacency Matrix

For any **k ≥ 1**, the **(i, j) entry of Aᵏ** gives the **number of walks of length k** from vᵢ to vⱼ.

|Power|Diagonal entry (i,i)|Off-diagonal entry (i,j)|
|---|---|---|
|A²|deg(vᵢ)|Number of walks of length 2 from vᵢ to vⱼ|
|A³|—|Number of walks of length 3 from vᵢ to vⱼ|
|Aᵏ|—|Number of walks of length k from vᵢ to vⱼ|

### Example

For a graph with adjacency matrix A:

```
A = | 0 1 1 0 |      A² = | 2 1 1 1 |      A³ = | 2 4 3 1 |
    | 1 0 1 1 |           | 1 3 1 0 |           | 4 2 4 3 |
    | 1 1 0 0 |           | 1 1 2 1 |           | 3 4 2 1 |
    | 0 1 0 0 |           | 1 0 1 1 |           | 1 3 1 1 |
```

- **A³(1,2) = 4** → 4 walks of length 3 between v₁ and v₂: (v₁,v₂,v₁,v₂), (v₁,v₃,v₁,v₂), (v₁,v₂,v₄,v₂), (v₁,v₂,v₃,v₂)
- **A²(2,4) = 0** → no walk of length 2 between v₂ and v₄.

---

## The Königsberg Bridge Problem

The original question: _Can you walk across all seven bridges of Königsberg exactly once and return to your starting point?_

**Answer: No.** The graph has vertices of **odd degree**, so it is **not Eulerian**, and no such closed walk exists.

---

## Key Terms Checklist

- [ ] Walk, Trail, Path
- [ ] Open walk, Closed walk
- [ ] Length of a walk
- [ ] Circuit, Cycle
- [ ] Eulerian circuit, Eulerian graph
- [ ] Semi-Eulerian graph, Eulerian trail
- [ ] Hamiltonian cycle, Hamiltonian graph
- [ ] Connected graph, Bridge
- [ ] Adjacency matrix and its powers (Aᵏ)

> ⚠️ **Remember to revise matrix multiplication!**