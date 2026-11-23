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

## Previous-semester questions (scanned papers)

> [!info] Source
> Scanned CSE 4-2 previous Mid Term/Final papers from `../Previous QW/` were OCR’d. Only Artificial Intelligence (CSE 421) questions are included below. Some tables/diagrams could not be read clearly by OCR; answers use standard definitions and the course summary.

### AI — Final Fall 2025, CSE 421 (page 1)

**Q1(a).** Apply simple hill-climbing to an assumed problem and illustrate failure when all neighbors have equal or lower heuristic values. [10]

**Q1(b).** Given state value 10 and neighbors 9, 12, and 7 from left to right, find the state steepest-ascent hill climbing chooses. [10]

**Q1(c).** Apply minimax to the given tree and find the values for A, B, C, and D nodes. [10]

**Answer.**
(a) Hill climbing repeatedly moves to the best neighbor by heuristic value. If all neighbors of the current state have equal or lower values, there is no uphill move, so the search stops on a plateau or local maximum even if a better state exists farther away. Example: current h = 10, neighbors h = 9, 10, 10 → no strictly better neighbor, so stop.
(b) Choose the neighbor with the highest value: **12 (right neighbor)**. Move from 10 to 12; repeat until no neighbor is strictly better.
(c) Propagate leaf values upward: at a minimizing node take the child minimum; at a maximizing node take the child maximum. The tree image was OCR-garbled, so exact A/B/C/D values cannot be recovered; apply the bottom-up minimax rule to the readable tree.

### AI — Mid Term Fall 2025, CSE 421 (page 3)

**Q1(a).** In a dynamic environment where doors open and close unpredictably, examine how a Model-Based Agent and a Learning Agent would plan and adjust actions. [10]

**Q1(b).** A crop-monitoring drone fails during cloudy weather. Identify which environment characteristic is affecting performance. [10]

**Q1(c).** A cleaning robot slows down as the floor accumulates more dirt. Determine whether this is due to the agent or the environment. [10]

**Answer.**
(a) **Model-Based Agent:** keeps an internal model of which doors are open/closed and updates it as observations arrive; chooses actions using the model and goal. Useful when the environment changes between observations. **Learning Agent:** improves its policy from experience (which door actions succeeded or failed); better when door patterns are unknown or change over time.
(b) The environment is **partially observable and dynamic**. Cloudy weather reduces sensor reliability and conditions change while the drone is operating.
(c) Primarily the **environment**: accumulated dirt changes floor condition/friction and slows the robot. It is an agent problem only if the robot lacks dirt sensing or a cleaning-mode policy.

### AI — Mid Term Spring 2026, CSE 421 (page 11)

**Q1(a).** A robot vacuum cleaner repeatedly cleans already clean spots. Analyze the agent type and why it behaves this way. [10]

**Q1(b).** A futuristic AI traffic light works like traffic police. Identify and classify the environment characteristics. [10]

**Q1(c) (OR).** A goal-based warehouse robot completes delivery early but skips an item. Examine how goal-based logic caused this error. [10]

**Answer.**
(a) The vacuum behaves like a **simple reflex/model-based agent without a visited-set**: it reacts to “dirt detected” but does not mark cleaned spots, so it revisits them. Fix: add a cleaned-spots map and make the goal “clean every dirty spot exactly once.”
(b) **Partially observable** (cannot see all vehicles), **dynamic** (traffic changes continuously), **sequential** (each signal decision affects later states), **multi-agent** (drivers and pedestrians), and **stochastic/continuous** (arrival times are uncertain).
(c) The goal was formulated as “complete delivery early” without the constraint “deliver every item.” Fix: make the goal conjunctive (deliver all items and minimize time) or add an item-check/pickup step before ending the task.
