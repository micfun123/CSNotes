
#discrete-maths #graphs #revision

---

## 📖 All Definitions

> [!definition] Graph A **graph** $G$ is a pair $(V, E)$ where:
> 
> - $V$ is a non-empty set of **vertices** (nodes)
> - $E$ is a set of **edges**, each edge being a set of two _distinct_ elements of $V$

> [!definition] Edge An element $e \in E$ of the form $e = {u, v}$, connecting two distinct vertices $u$ and $v$.
> 
> - Written as $uv$ (same as $vu$ — order doesn't matter)
> - $u$ and $v$ are called the **end vertices** of $e$
> - $e$ **joins** (connects) $u$ and $v$

> [!definition] Incident A vertex $v$ is **incident** with an edge $e$ if $v$ is one of the end vertices of $e$.

> [!definition] Adjacent Two vertices $u$ and $v$ are **adjacent** if $uv \in E$ (i.e. they are connected by an edge).

> [!definition] Degree The **degree** of a vertex $v$, written $\deg v$, is the number of edges incident with $v$.
> 
> - A vertex with $\deg v = 0$ is called an **isolated vertex**

> [!definition] Degree Sequence The degrees $d_1 \leq d_2 \leq \cdots \leq d_n$ of all vertices of $G$, listed in non-decreasing order. Written as the tuple $(d_1, d_2, \ldots, d_n)$.

> [!definition] Multigraph / Pseudograph Like a graph, but may contain:
> 
> - **Loops** — an edge from a vertex to itself
> - **Multiple edges** — more than one edge between the same pair of vertices
> 
> _The Königsberg bridge graph is a multigraph._

> [!definition] Complete Graph $K_n$ A graph on $n$ vertices where **every pair of vertices is adjacent**. $$|E| = \frac{n(n-1)}{2}$$

> [!definition] Bipartite Graph A graph whose vertices can be partitioned into two disjoint sets $V_1$ and $V_2$ such that **every edge connects a vertex in $V_1$ to a vertex in $V_2$** (no edges within $V_1$ or within $V_2$).

> [!definition] Complete Bipartite Graph $K_{m,n}$ A bipartite graph where **every vertex in $V_1$ is joined to every vertex in $V_2$**.
> 
> - $|V_1| = m$, $|V_2| = n$
> - Number of edges $= m \times n$

> [!definition] Subgraph A graph $H$ is a **subgraph** of $G$ if: $$V(H) \subseteq V(G) \quad \text{and} \quad E(H) \subseteq E(G)$$

> [!definition] Isomorphic Graphs Graphs $G$ and $H$ are **isomorphic** ($G \cong H$) if there exists a bijection $f: V(G) \to V(H)$ such that: $$uv \in E(G) \iff f(u)f(v) \in E(H)$$ Informally: $H$ can be obtained from $G$ by **re-labelling the vertices**.

---

## 📐 Key Theorems

### Euler Theorem (Handshaking Lemma)

> [!theorem] Euler Theorem In any graph $G = (V, E)$: $$\sum_{v \in V} \deg v = 2|E|$$ The sum of all vertex degrees equals **twice** the number of edges.

**Why?** Every edge contributes $+1$ to each of its two end vertices, so each edge adds $2$ to the total.

#### Consequences

> [!important] Corollary 1 In any graph, the **sum of all vertex degrees is even**.

> [!important] Corollary 2 In any graph, the **number of vertices with odd degree is even**.

#### Examples — Invalid Degree Sequences

|Sequence|Why invalid|
|---|---|
|$(1, 2, 3, 3)$|Sum $= 9$ — **odd**, violates Euler Theorem|
|$(1, 2, 2, 2)$|Only **one** odd-degree vertex — must be even|
|$(1, 2, 3, 4, 4, 5)$|Sum $= 19$ — **odd**|

---

### Complete Graph Edge Formula

$$K_n \text{ has } \frac{n(n-1)}{2} \text{ edges}$$

**Proof:** Every vertex has degree $n-1$. By Euler: $2|E| = n(n-1)$, so $|E| = \frac{n(n-1)}{2}$.

|Graph|Vertices|Edges|
|---|---|---|
|$K_1$|1|0|
|$K_2$|2|1|
|$K_3$|3|3|
|$K_4$|4|6|
|$K_5$|5|10|

---

## 🌉 Motivating Problems

### 1. Königsberg Bridge Problem

**Question:** Can you walk over all 7 bridges exactly once and return to your start?

- Euler (1736) modelled land masses as **vertices** and bridges as **edges**
- Answer: **No** — proved using what we now call Eulerian circuits
- This problem _invented graph theory_

### 2. Travelling Salesman Problem (TSP)

**Question:** Given cities and distances, find the shortest tour visiting each city exactly once.

- Modelled as a **weighted complete graph**
- Type: **optimisation (minimisation)**
- No efficient general solution is known

### 3. Map Colouring Problem

**Question:** Colour a map so no two neighbouring regions share a colour. How many colours are needed?

- Modelled as a graph: regions → vertices, shared borders → edges
- **Four Colour Theorem:** any planar map needs at most 4 colours
- 3 colours are **not** always enough

---

## 🗂️ Types of Graph Problems

|Type|Question|Example|
|---|---|---|
|**Existence**|Does a solution exist?|Königsberg bridge walk|
|**Optimisation**|What is the _best_ solution?|Travelling Salesman Problem|
|**Construction**|_How_ do we find a solution?|Finding a valid map colouring|
|**Enumeration**|_How many_ solutions are there?|Number of shortest TSP tours|

---

## 🔷 Special Graph Families

### Complete Graphs $K_n$

- Every pair of vertices connected
- Each vertex has degree $n - 1$
- $|E| = \frac{n(n-1)}{2}$

### Bipartite Graphs

- Vertices split into $V_1$ and $V_2$; edges only cross between them
- A graph is bipartite $\iff$ it contains **no odd-length cycles**

### Complete Bipartite $K_{m,n}$

- Every vertex in $V_1$ connects to every vertex in $V_2$
- $|E| = m \times n$
- Example: $K_{4,2}$ has $4 \times 2 = 8$ edges

---

## 🔁 Graph Isomorphism

Two graphs are isomorphic if one is a **re-labelling** of the other — same structure, different names.

### Necessary Conditions

> [!warning] To prove graphs are NOT isomorphic, show any ONE of these fails:
> 
> 1. Different number of vertices
> 2. Different number of edges
> 3. Different degree sequence
> 4. Different connectivity (one connected, one not)

> [!caution] These conditions are **necessary but not sufficient**. Graphs can satisfy all four and still not be isomorphic. Proving isomorphism requires constructing the bijection $f$ explicitly.

### Labelled vs Unlabelled Graphs on 3 Vertices

- **Labelled** (distinct vertex names): **8** graphs (every subset of 3 possible edges)
- **Unlabelled** (up to isomorphism): **4** graphs
    - Empty graph (no edges)
    - One edge
    - Path of length 2 (two edges)
    - Triangle $K_3$ (three edges)

---

## ⚡ Quick Reference

```
Sum of degrees = 2 × number of edges
Edges in Kₙ   = n(n-1)/2
Edges in Km,n  = m × n
```

**Degree sequence valid?** → Sum must be **even** AND number of odd values must be **even**

**Graphs not isomorphic?** → Show they differ in vertex count, edge count, or degree sequence

---

## 🏷️ Key Terms

`graph` `vertex` `edge` `multigraph` `loop` `multiple edges` `incident` `adjacent` `degree` `deg v` `isolated vertex` `degree sequence` `complete graph` `Kn` `bipartite graph` `complete bipartite graph` `Km,n` `subgraph` `isomorphic` `isomorphism` `Euler Theorem` `Handshaking Lemma`

---

_Lecture DM-7 — Janka Chlebíková — School of Computing, University of Portsmouth_