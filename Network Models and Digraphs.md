
---

## Definitions (Quick Reference)

> **Digraph:** A pair $(V, E)$ of sets where $V$ is a nonempty set of vertices and $E$ is a set of _ordered pairs_ of distinct elements of $V$, called **arcs** (edges). Each arc has an orientation indicated by an arrow.

> **Indegree** of a vertex: the number of arcs directed _into_ that vertex.

> **Outdegree** of a vertex: the number of arcs directed _out of_ that vertex.

> **Adjacency Matrix** of a digraph $G$ with vertices $v_1, v_2, \ldots, v_n$: a matrix $A$ where $a_{ij} = 1$ if there is an arc from $v_i$ to $v_j$, and $0$ otherwise. $A$ is generally **not symmetric**.

> **Network:** A directed weighted graph $G = (V, E)$ with:
> 
> - a **source** $S$ (no incoming arcs),
> - a **sink** $T$ (no outgoing arcs),
> - a nonnegative **capacity** $c(e) \geq 0$ on each arc $e$.

> **Flow:** A mapping that assigns to each arc $e$ a number $f(e)$ satisfying:
> 
> 1. **Feasibility condition:** $0 \leq f(e) \leq c(e)$ for each arc $e \in E$.
> 2. **Conservation of flow:** For each internal vertex $u$ (i.e. $u \neq S, T$): the sum of flows _into_ $u$ equals the sum of flows _out of_ $u$.

> **Value of a flow:** $\sum_{v \in V} f(Sv)$ — the sum of flows on all arcs leaving the source $S$ (equivalently, the sum of flows on all arcs entering the sink $T$).

> **Maximum flow:** A flow of maximum value.

> **Forward arc** (w.r.t. a path $P$ in the underlying undirected graph): an arc whose orientation _follows_ the direction of $P$.

> **Backward arc** (w.r.t. a path $P$): an arc whose orientation goes _against_ the direction of $P$.

> **Flow-augmenting path:** A path $P$ from $S$ to $T$ in the underlying undirected graph such that:
> 
> - for each **forward** arc $e$ in $P$: $f(e) < c(e)$ (unsaturated),
> - for each **backward** arc $e$ in $P$: $f(e) > 0$ (carrying non-zero flow).

> **Saturated arc:** An arc $e$ where $f(e) = c(e)$ — no additional flow can be pushed through it.

> **(S, T)-cut:** A partition ${S, \mathcal{T}}$ of $V$ such that $S \in S$ and $T \in \mathcal{T}$.

> **Capacity of an (S, T)-cut** ${S, \mathcal{T}}$: the sum of capacities of all arcs directed _from_ $S$ to $\mathcal{T}$.

> **Minimum (S, T)-cut:** An $(S, T)$-cut of the smallest possible capacity.

---

## 1. Directed Graphs (Digraphs)

Graphs model real-life situations; when edges represent roads or pipes they need direction and weights. A digraph captures this by making each edge an ordered pair — the direction matters, so arc $uv$ and arc $vu$ are _different_.

**Example:**

- $V = {u, v, w}$, $E = {vu, vw, uw}$
- The arc $vu$ goes _from_ $v$ _to_ $u$.

### Indegree and Outdegree

Each vertex has two degree values:

- **Indegree** = number of arcs coming _in_
- **Outdegree** = number of arcs going _out_

**Example** (four vertices $u, v, w, z$):

|Vertex|Indegree|Outdegree|
|---|---|---|
|$u$|1|1|
|$v$|1|2|
|$w$|2|0|
|$z$|0|1|

---

## 2. Adjacency Matrix of a Digraph

The adjacency matrix $A$ is defined as before for graphs, but $a_{ij} = 1$ iff there is an arc _from_ $v_i$ _to_ $v_j$. Because direction matters, $A$ is **not symmetric** in general.

**Key properties:**

- The **outdegree** of $v_i$ = number of 1s in _row_ $i$.
- The **indegree** of $v_i$ = number of 1s in _column_ $i$.
- The $(i,j)$ entry of $A^k$ = number of walks of length $k$ from $v_i$ to $v_j$ respecting arc orientations.

**Example:**

$$A = \begin{pmatrix} 0 & 0 & 0 & 0 \ 1 & 0 & 0 & 0 \ 1 & 1 & 0 & 0 \ 0 & 0 & 1 & 0 \end{pmatrix}, \quad A^2 = \begin{pmatrix} 0 & 0 & 0 & 0 \ 0 & 0 & 0 & 0 \ 1 & 0 & 0 & 0 \ 1 & 1 & 0 & 0 \end{pmatrix}$$

The entry $(4,1)$ in $A^2$ being 1 means there is exactly one walk of length 2 from $v_4$ to $v_1$.

---

## 3. Network Models

Directed graphs model networks where something _flows_:

- Transportation networks (commodities)
- Pipeline networks (oil, gas)
- Computer networks (data)

In each case the central problem is: **find a maximum flow**.

### Structure of a Network

The network from the running example has:

- Source $S$, Sink $T$
- Internal nodes $A, B, C, D$
- Arc capacities: $SA=10$, $SB=11$, $AC=12$, $AD=4$, $BC=8$, $BD=2$, $CT=11$, $DT=14$

---

## 4. Flows

A flow assigns to each arc $e$ a value $f(e)$ satisfying the feasibility and conservation conditions (see Definitions above).

**Notation on diagrams:** each arc is labelled `flow, capacity` — e.g. `5,10` means flow = 5, capacity = 10.

**Value of a flow** = sum of flows leaving $S$ = sum of flows entering $T$ (guaranteed equal by conservation).

### Example of a Simple Flow

Pumping 2 units along path $S \to A \to D \to T$ with 0 on all other arcs:

- Feasibility: $f(e) \leq c(e)$ holds everywhere.
- Conservation: flow in = flow out at every internal vertex.
- **Value = 2.**

---

## 5. Building Up to a Maximum Flow

### Greedy Path Augmentation

A simple starting strategy:

1. Find a directed path from $S$ to $T$.
2. Push flow along it up to the bottleneck capacity (the minimum capacity arc on the path — a **saturated arc**).
3. Repeat with new paths.

**Example trace:**

|Step|Path used|Flow added|Total flow|
|---|---|---|---|
|1|$S \to A \to C \to T$|10 (SA saturated)|10|
|2|$S \to B \to D \to T$|2 (BD saturated)|12|
|3|$S \to B \to C \to T$|1 (CT saturated)|13|

After step 3, **every directed path from $S$ to $T$ contains a saturated arc**. But the flow can still be improved — we need a smarter approach.

---

## 6. Forward and Backward Arcs; Flow-Augmenting Paths

To go beyond simple directed paths, we consider paths in the _underlying undirected graph_. Each arc on such a path is either:

- **Forward:** its direction agrees with the path direction — we can push _more_ flow through it if it is unsaturated ($f(e) < c(e)$).
- **Backward:** its direction opposes the path — we can _reduce_ flow through it if it currently carries flow ($f(e) > 0$).

A **flow-augmenting path** uses both forward and backward arcs to route additional flow without violating any constraint.

### Computing the Improvement $\Delta$

For an augmenting path $P$, the maximum improvement $\Delta$ is:

$$\Delta = \min \left( \min_{\text{forward arcs}} {c(e) - f(e)},\quad \min_{\text{backward arcs}} {f(e)} \right)$$

Then update:

- **Forward arc:** $f(e) := f(e) + \Delta$
- **Backward arc:** $f(e) := f(e) - \Delta$

**Why this preserves conservation:** at every internal vertex on the path, any gain from a forward arc or loss from a backward arc is exactly offset by the corresponding change on the adjacent arc.

### Example

Starting from flow value 13, consider path $P = (S, B, C, A, D, T)$ in the undirected graph:

|Arc|Type|Value available|
|---|---|---|
|$SB$|Forward|$c - f = 11 - 3 = 8$|
|$BC$|Forward|$c - f = 8 - 1 = 7$|
|$CA$|Backward|$f = 10$|
|$AD$|Forward|$c - f = 4 - 0 = 4$|
|$DT$|Forward|$c - f = 14 - 2 = 12$|

$$\Delta = \min{8, 7, 10, 4, 12} = 4$$

Flow increases by 4. **New total flow = 17.**

---

## 7. Algorithm for Maximum Flow

```
1. Start with any valid flow (e.g. f(e) = 0 for all arcs).

2. Search for a flow-augmenting path P (from S to T in the
   underlying undirected graph, satisfying the conditions above).
   - If no such path exists → STOP. The current flow is MAXIMUM.

3. Compute Δ = min over:
     { f(e)        | e is a backward arc in P }
     { c(e) - f(e) | e is a forward arc in P  }

4. Update flows:
     - For each forward arc e in P:  f(e) := f(e) + Δ
     - For each backward arc e in P: f(e) := f(e) − Δ

5. Go to step 2.
```

**Notes:**

- Use an exhaustive search over all paths from $S$ to $T$ to find augmenting paths.
- The order in which augmenting paths are chosen does **not** affect the final maximum flow value.

---

## 8. Cuts and the Max-Flow Min-Cut Theorem

### (S, T)-Cuts

An $(S, T)$-cut partitions $V$ into sets $\mathcal{S}$ (containing $S$) and $\mathcal{T}$ (containing $T$). Its **capacity** is the sum of capacities of arcs going _from_ $\mathcal{S}$ _to_ $\mathcal{T}$ — arcs in the reverse direction are **not** counted.

**Key inequality:** For any flow $f$ and any $(S,T)$-cut: $$\text{value of } f \leq \text{capacity of cut}$$

### Max-Flow Min-Cut Theorem

> **Theorem:** In a directed graph, the value of a maximum flow equals the capacity of a minimum $(S, T)$-cut.

This gives a way to **verify** that a flow is maximum: find an $(S,T)$-cut whose capacity equals the flow value.

### Example Verification

With flow value 17, consider the cut $\mathcal{S} = {S, A, B, C}$, $\mathcal{T} = {D, T}$:

$$\text{cap} = c(AD) + c(BD) + c(CT) = 4 + 2 + 11 = 17$$

Flow value (17) = cut capacity (17) → **flow is maximum, no further improvement possible.**

---

## Summary

- A **digraph** is a graph with directed edges (arcs); direction must be respected in all walks and paths.
- A **network** adds a source, sink, and capacities on arcs.
- A **flow** assigns values to arcs respecting feasibility and conservation.
- The **maximum flow algorithm** repeatedly finds flow-augmenting paths (allowing backward arcs) and increases the flow until none exist.
- The **Max-Flow = Min-Cut** theorem confirms optimality and provides a certificate.