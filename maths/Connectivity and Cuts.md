
---

## Definitions

> **Connected Graph:** A graph G is _connected_ if there is a path between any given pair of vertices; _disconnected_ otherwise.

> **Bridge:** An edge in a connected graph is a _bridge_ if deleting it would create a disconnected graph.

> **Edge Cut:** A set of edges whose removal renders the graph disconnected.

> **Edge-Connectivity λ(G):** The smallest number of edges whose removal may disconnect G. Equivalently, the size of the smallest edge cut of G.

> **k-Edge-Connected:** A graph G is _k-edge-connected_ when λ(G) ≥ k — it remains connected whenever fewer than k edges are removed.

> **Vertex Cut:** A set of vertices whose removal renders a connected graph G disconnected. (When a vertex is removed, all edges incident to it are also removed.)

> **Vertex-Connectivity κ(G):** The smallest number of vertices whose removal may disconnect G. Equivalently, the size of the smallest vertex cut.
> 
> - Special case: for the complete graph K_n, κ(K_n) = n − 1 (it cannot be disconnected by vertex removal, so this is defined by convention).

> **k-Vertex-Connected (k-Connected):** A graph G is _k-vertex-connected_ if it remains connected when fewer than k vertices are deleted.

> **Optimal Connectivity:** A graph G has _optimal connectivity_ when κ(G) = λ(G) = δ(G) = 2|E|/|V|, giving the maximum possible vertex- and edge-connectivity for a graph with |V| vertices and |E| edges.

> **δ(G):** The minimum vertex degree in G (the degree of the lowest-degree vertex).

---

## Key Theorem: Upper Bounds on Connectivity

For any connected graph G = (V, E):

$$\kappa(G) \leq \lambda(G) \leq \delta(G) \leq \frac{2|E|}{|V|}$$

- **κ(G)** ≤ **λ(G)**: vertex-connectivity never exceeds edge-connectivity.
- **λ(G)** ≤ **δ(G)**: edge-connectivity never exceeds the minimum degree (you can always cut all edges at the lowest-degree vertex).
- **δ(G)** ≤ **2|E|/|V|**: minimum degree is at most the average degree.

> Note: 2|E|/|V| is the **average vertex degree** (sum of all degrees = 2|E|).

---

## Edge-Connectivity λ(G)

G has edge-connectivity λ(G) if:

- There **exist** λ(G) edges whose removal disconnects G.
- Removal of any λ(G) − 1 edges does **not** disconnect G.

### Examples

|Graph|λ(G)|Reason|
|---|---|---|
|G₁|1|One edge (a bridge) disconnects it|
|G₂|2|Two edges disconnect it; removing any one edge leaves it connected|
|G₃|3|Three edges needed to disconnect|

**Edge cuts need not all have the same size** — the same graph can have edge cuts of different sizes (e.g. 3, 4, 5, or 6 edges). The edge-connectivity is the _minimum_ over all edge cuts.

---

## Vertex-Connectivity κ(G)

G has vertex-connectivity κ(G) if:

- There **exist** κ(G) vertices whose removal disconnects G.
- Removal of any κ(G) − 1 vertices does **not** disconnect G.

### Examples

|Graph|κ(G)|Reason|
|---|---|---|
|G₁|1|One vertex (a cut vertex) disconnects it|
|G₂|2|Two vertices must be removed; any one removal leaves it connected|
|G₃|3|Three vertices needed to disconnect|

---

## Optimal Connectivity

A graph achieves **optimal connectivity** when:

$$\kappa(G) = \lambda(G) = \delta(G) = \frac{2|E|}{|V|}$$

- All optimally connected graphs are **regular** (every vertex has the same degree).
- But **not** every regular graph has optimal connectivity.

### Non-equality example

A graph can have δ(G) = 3, λ(G) = 2, κ(G) = 1 — showing all three values can be strictly different.

---

## Practical Motivation: Telecommunication Networks

Graph connectivity directly models network reliability:

- **Vertices** = telephone exchanges / subscribers
- **Edges** = communication links

|Failure type|Relevant measure|
|---|---|
|Links (edges) fail|Edge-connectivity λ(G)|
|Exchanges (vertices) fail|Vertex-connectivity κ(G)|

A network with higher λ(G) or κ(G) is more reliable — more simultaneous failures are needed before communication breaks down.

---

## Summary

- A **bridge** is an edge whose removal disconnects the graph (λ = 1 at that edge).
- **Edge-connectivity λ(G)**: minimum edge cut size.
- **Vertex-connectivity κ(G)**: minimum vertex cut size.
- Inequality chain: κ(G) ≤ λ(G) ≤ δ(G) ≤ 2|E|/|V|.
- **Optimal connectivity**: all three equal — maximally robust graph.
- Complete graph K_n has κ(K_n) = n − 1.