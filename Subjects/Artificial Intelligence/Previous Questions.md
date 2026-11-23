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

**Marking scheme:** Definition of branching factor (1 mark) + complexity formula (1 mark) + strategy table / comparison (2 marks) + example (1 mark).

**Definition.** The **branching factor** `b` is the maximum number of successor nodes generated from a single state. It measures how many actions are available at a state.

**Formula.** If the shallowest solution is at depth `d`, a complete tree search may generate roughly:

\[
1 + b + b^2 + \cdots + b^d = O(b^d)
\]

nodes. Hence time and space complexity are **exponential in `d`** and grow very quickly as `b` increases.

**Effect on common strategies:**

| Strategy | Time | Space | Effect of larger `b` |
|---|---|---|---|
| BFS | `O(b^d)` | `O(b^d)` | More nodes per level; memory grows fastest |
| DFS | `O(b^m)` | `O(bm)` | More branches per node; memory grows with depth × `b` |
| UCS | `O(b^d)` worst case | `O(b^d)` | More frontier nodes with distinct path costs |
| A* | `O(b^d)` worst case | `O(b^d)` | A good heuristic reduces the *effective* branching factor `b*` |

**Example.** With `b = 2` and `d = 5`, leaves ≈ `2^5 = 32`. With `b = 10` and `d = 5`, leaves ≈ `10^5 = 100,000`. This is why uninformed search becomes impractical in large state spaces.

**Exam point.** `b` affects both time and space; the effect is exponential. A heuristic does not change the true `b`, but it can reduce the number of nodes actually expanded (effective branching factor `b*`). Always define `b`, `d`, and `m` in your answer.

---

> [!question] Q2. Describe how repeated states can affect the efficiency of a search algorithm and how visited-node checking helps overcome this problem. [5]

**Answer.**

**Marking scheme:** Definition of repeated state (1 mark) + causes (1 mark) + problem/inefficiency (1 mark) + visited-node checking algorithm (1 mark) + benefit/trade-off (1 mark).

**Definition.** A **repeated state** is a state reached by more than one path. Repeated states arise from:
- **Cycles:** going A → B → A.
- **Reversible actions:** move north then move south.
- **Transpositions:** different action orders reaching the same state (e.g., A→B→C and A→C→B).

**Problem.** In **tree search**, the algorithm may expand the same state many times, causing duplicated work and exponential blow-up. In an infinite graph, a cycle can make DFS loop forever without reaching the goal.

**Visited-node checking (closed/explored set):** Store every state that has already been expanded. Before adding or expanding a successor, check whether its state is in the visited set; if yes, discard the duplicate.

```text
frontier = {start}
visited  = {}
while frontier is not empty:
    node = remove(frontier)
    if node is goal: return path
    if node.state in visited: continue
    visited.add(node.state)
    for child in expand(node):
        if child.state not in visited:
            frontier.add(child)
```

**Benefits:** avoids duplicate expansion, prevents infinite loops in cyclic graphs, greatly improves efficiency.

**Trade-off:** the visited set uses extra memory. For optimal search with unequal step costs, a simple visited set may be unsafe; the algorithm may need to reopen a state if a cheaper path is found later (UCS/A* with a consistent heuristic avoids reopening).

**Lecture link:** State Space Search — problem formulation, completeness, optimality, time/space complexity.

---

## Set A

> [!question] Q1. Explain how the branching factor influences the time and space complexity of a search algorithm. [5]

**Answer.** Same as Set B Q1. Use the full answer above (definition, formula, table, example, exam point).

---

> [!question] Q2. Describe how Depth-First Search (DFS) explores a search tree and why it may get stuck in an infinite path. [5]

**Answer.**

**Marking scheme:** Stack/LIFO idea (1 mark) + expansion/backtracking steps (1 mark) + why infinite path / not complete (1 mark) + not optimal (1 mark) + fixes (1 mark).

**How DFS explores.** DFS uses a **stack** (LIFO). It starts at the root, expands one child, then goes as deep as possible along that branch before backtracking. When a node has no unvisited children, DFS backtracks to the most recent node with an unexplored child.

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

**Why it gets stuck.** If the state space has an infinite branch or a cycle, DFS may follow that branch forever without reaching the goal. DFS has no depth limit and no guarantee that the goal is on the first branch explored. It is **not complete** in infinite spaces and **not optimal** even in finite spaces (it may find a deep costly goal before a shallow cheap one).

**Fixes:** use a depth limit (DLS), check visited states, or use iterative deepening (IDDFS) to combine DFS’s low memory with BFS’s completeness.

**Lecture link:** Uninformed search — BFS/DFS/UCS/DLS/IDDFS/BDS; completeness, optimality, time/space.

---

## Previous-semester questions (scanned papers)

> [!info] Source
> Scanned CSE 4-2 previous Mid Term/Final papers from `../Previous QW/` were OCR’d. Only Artificial Intelligence (CSE 421) questions are included below.

### AI — Final Fall 2025, CSE 421 (page 1)

**Q1(a).** Apply simple hill-climbing to an assumed problem and illustrate failure when all neighbors have equal or lower heuristic values. [10]

**Q1(b).** Given state value 10 and neighbors 9, 12, and 7 from left to right, find the state steepest-ascent hill climbing chooses. [10]

**Q1(c).** Apply minimax to the given tree and find the values for A, B, C, and D nodes. [10]

**Answer.**

**Marking:** hill-climbing steps (3) + local maximum/plateau illustration (3) + steepest choice with reasoning (3) + minimax bottom-up rule + example (4).

**(a) Simple hill climbing:** Start from an initial state. Repeatedly generate all neighbors, compute each neighbor’s heuristic `h(n)`, and move to the neighbor with the **highest** `h`. Stop when no neighbor has a strictly higher value than the current state.
**Failure illustration:** Suppose current state `h = 10`, neighbors have `h = 9, 10, 10`. No neighbor is strictly better (`>10`), so hill climbing stops at this state even though a better state may exist farther away. This is a **local maximum** (all neighbors equal/lower) or a **plateau** (neighbors equal).

**(b)** Choose the neighbor with the highest value: **12 (right neighbor)**. Move from current `10` → `12`. Repeat: at `12`, if no neighbor has `h > 12`, stop at `12` (local maximum). Otherwise keep moving to the highest neighbor.

**(c) Minimax:** Propagate leaf values upward through the tree. At a **maximizing** node, take the **maximum** of child values; at a **minimizing** node, take the **minimum**. The root value is the maximizer’s guaranteed value under optimal play.
*(Note: The tree image was OCR-garbled, so exact A/B/C/D numeric values could not be read. Apply the bottom-up maximin rule to the readable tree in the exam paper.)*

**Lecture link:** Informed search — hill climbing, local search; adversarial search — minimax.

---

### AI — Mid Term Fall 2025, CSE 421 (page 3)

**Q1(a).** In a dynamic environment where doors open and close unpredictably, examine how a Model-Based Agent and a Learning Agent would plan and adjust actions. [10]

**Q1(b).** A crop-monitoring drone fails during cloudy weather. Identify which environment characteristic is affecting performance. [10]

**Q1(c).** A cleaning robot slows down as the floor accumulates more dirt. Determine whether this is due to the agent or the environment. [10]

**Answer.**

**Marking:** agent descriptions (4 each) + environment characteristic identification (4) + justification (3) + agent/environment attribution (3) + example (3).

**(a)**
- **Model-Based Agent:** Maintains an internal model of the world (e.g., which doors are open/closed). It updates the model from percepts and chooses actions using the model + goal. Best when the environment changes between observations but the agent can sense the current state.
- **Learning Agent:** Improves its policy from experience (which door actions succeeded/failed). Has a performance element, critic, learning element, and problem generator. Best when door patterns are unknown or change over time; it does not need a perfect model upfront.

**(b)** The environment is **partially observable** (the drone cannot see through clouds / full field at once) and **dynamic** (conditions change while the drone operates). Cloudy weather reduces sensor reliability and changes lighting/visibility during the mission.

**(c)** Primarily the **environment**: accumulated dirt changes floor friction/condition, slowing the robot. It becomes an **agent** problem only if the robot lacks dirt sensing or a cleaning-mode policy (i.e., the agent fails to adapt to the environmental change).

**Lecture link:** Agents and environments — agent structure, types (simple reflex, model-based, goal-based, utility-based, learning); environment properties (observable, deterministic, episodic, static, discrete).

---

### AI — Mid Term Spring 2026, CSE 421 (page 11)

**Q1(a).** A robot vacuum cleaner repeatedly cleans already clean spots. Analyze the agent type and why it behaves this way. [10]

**Q1(b).** A futuristic AI traffic light works like traffic police. Identify and classify the environment characteristics. [10]

**Q1(c) (OR).** A goal-based warehouse robot completes delivery early but skips an item. Examine how goal-based logic caused this error. [10]

**Answer.**

**Marking:** agent-type diagnosis (4) + missing mechanism + fix (3) + five environment characteristics with classification (5) + goal-formulation flaw + fix (3) + example (3).

**(a)** The vacuum behaves like a **simple reflex or model-based agent without a visited-set**: it reacts to “dirt detected” but does not record which spots have been cleaned, so it revisits them.
**Fix:** Add a cleaned-spots map (visited-set over locations) and reformulate the goal as “clean every dirty spot exactly once.” This turns it into a goal-based agent with state memory.

**(b)** Environment characteristics:
1. **Partially observable** — cannot see all vehicles/pedestrians at once.
2. **Dynamic** — traffic density changes continuously while the light operates.
3. **Sequential** — each signal decision affects later states (queues build/dissipate over time).
4. **Multi-agent** — drivers, cyclists, and pedestrians are other agents whose actions affect outcomes.
5. **Stochastic / continuous** — vehicle arrival times are uncertain and positions are continuous.

**(c)** The goal was formulated only as “complete delivery early,” omitting the constraint “deliver every item.” A goal-based agent pursues the stated goal literally, so finishing early (skipping an item) satisfies the incomplete goal but fails the real task.
**Fix:** Make the goal conjunctive — “deliver all assigned items AND minimize time” — or add an item-check/pickup precondition before ending the task.

**Lecture link:** Agents and environments — agent types; environment properties; problem formulation (states, initial state, actions, goal test, path cost).

## Exam tips

- For complexity questions, always define `b`, `d`, and `m`.
- For repeated states, mention both cycles and transpositions.
- For DFS, mention the stack, backtracking, infinite depth, and the fixes.
- For hill climbing, draw a small state-value diagram showing local maximum/plateau.
- For minimax, show bottom-up propagation on a small tree.
- For agent questions, name the environment properties first, then match agent type.
