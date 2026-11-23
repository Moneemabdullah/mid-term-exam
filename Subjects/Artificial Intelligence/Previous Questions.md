---
type: previous-questions
subject: Artificial Intelligence
source: ClassTestQuestions.pdf
last_updated: 2026-11-23
---

# Artificial Intelligence — Previous Questions

> [!info] Source
> Transcribed from `ClassTestQuestions.pdf` (5-page scanned class-test paper, scanned 17 November 2026). AI questions are **CT-1**. Set A and Set B share Question 1.

## Question bank

| Set | Question | Marks | Topic | Status |
|---|---|---|---|---|
| B | Q1. Branching factor and time/space complexity | 5 | Search complexity | Answered |
| B | Q2. Repeated states and visited-node checking | 5 | Graph search | Answered |
| A | Q1. Branching factor and time/space complexity | 5 | Search complexity | Answered (same as Set B Q1) |
| A | Q2. DFS exploration and infinite paths | 5 | DFS | Answered |

## Set B

> [!question] Q1. Explain how the branching factor influences the time and space complexity of a search algorithm. [5]

**Answer.**

The **branching factor** `b` is the maximum number of successors generated from a node. It determines how quickly the search tree grows. If the solution is at depth `d`, a complete search may generate roughly

\[
1 + b + b^2 + \cdots + b^d = O(b^d)
\]

nodes. Therefore, time and space complexity are **exponential in `d`** and grow very quickly as `b` increases.

| Strategy | Time | Space | Effect of larger `b` |
|---|---|---|---|
| BFS | `O(b^d)` | `O(b^d)` | More nodes per level; memory grows fastest |
| DFS | `O(b^m)` | `O(bm)` | More branches to explore; memory grows linearly with depth and `b` |
| UCS | `O(b^d)` worst case | `O(b^d)` | More frontier nodes with distinct costs |
| A* | `O(b^d)` worst case | `O(b^d)` | A good heuristic reduces the effective branching factor |

For example, with `b = 2` and `d = 5`, the tree has about `2^5 = 32` leaves; with `b = 10`, it has `10^5 = 100,000` leaves. This is why uninformed search becomes impractical in large state spaces.

**Exam point:** `b` affects both time and space; the effect is exponential. A heuristic does not change the true branching factor, but it can reduce the number of nodes actually expanded.

> [!question] Q2. Describe how repeated states can affect the efficiency of a search algorithm and how visited-node checking helps overcome this problem. [5]

**Answer.**

A **repeated state** is a state reached by more than one path. Repeated states arise from cycles, reversible actions, or different action orders that lead to the same state (transpositions). In a **tree search**, the algorithm may expand the same state many times, causing duplicated work and exponential blow-up. In an infinite graph, a cycle can make DFS loop forever.

**Visited-node checking** (also called a closed list or explored set) stores states that have already been expanded. Before adding or expanding a successor, the algorithm checks whether the state is already visited. If it is, the duplicate is discarded.

```text
frontier = {start}
visited = {}
while frontier is not empty:
    node = remove(frontier)
    if node is goal: return path
    if node.state in visited: continue
    visited.add(node.state)
    for child in expand(node):
        if child.state not in visited:
            frontier.add(child)
```

**Benefits:** avoids duplicate expansion, prevents infinite loops in cyclic graphs, and can greatly improve efficiency.

**Trade-off:** the visited set uses extra memory. For optimal search with unequal step costs, a simple visited set may be unsafe; the algorithm may need to reopen a state if a cheaper path is found later (as in UCS/A* with a consistent heuristic, reopening is not needed).

## Set A

> [!question] Q1. Explain how the branching factor influences the time and space complexity of a search algorithm. [5]

Same question as Set B Q1. Use the answer above.

> [!question] Q2. Describe how Depth-First Search (DFS) explores a search tree and why it may get stuck in an infinite path. [5]

**Answer.**

DFS uses a **stack** (LIFO). It starts at the root, expands one child, then goes as deep as possible along that branch before backtracking. When a node has no unvisited children, DFS backtracks to the most recent node with an unexplored child.

```text
stack = [start]
visited = {}
while stack is not empty:
    node = stack.pop()
    if node is goal: return path
    if node.state in visited: continue
    visited.add(node.state)
    push unvisited children onto stack
```

**Why it can get stuck:** if the state space has an infinite branch or a cycle, DFS may follow that branch forever without reaching the goal. DFS has no depth limit and no guarantee that the goal is on the first branch it explores. It is therefore **not complete** in infinite spaces and is **not optimal** even in finite spaces.

**Fixes:** use a depth limit (DLS), check visited states, or use iterative deepening (IDDFS) to combine DFS's low memory with BFS's completeness.

## Exam tips

- For complexity questions, always define `b`, `d`, and `m`.
- For repeated states, mention both cycles and transpositions.
- For DFS, mention the stack, backtracking, infinite depth, and the fixes.
- For A*, remember `f(n) = g(n) + h(n)` and `h(n) <= h*(n)` for admissibility.
