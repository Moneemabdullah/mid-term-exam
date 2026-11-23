---
type: lecture-summary
subject: Artificial Intelligence
last_updated: 2026-11-23
---

# Artificial Intelligence — Lecture Summary

> [!info] Scope
> Based on the three provided AI lecture PDFs and the AI pages of the cross-subject handwritten notebook. The official syllabus was not provided; this is a concise exam-focused summary, not a substitute for the slides.

## Source map

| Source | Topics |
|---|---|
| `Study Materials/PDFs/Introduction, Foundation, History, Application of AI.pdf` | AI definition, foundations, history, applications |
| `Study Materials/PDFs/Agents and Environments.pdf` | Agents, structure, types, environments |
| `Study Materials/PDFs/State Space Search (uninformed and Informed Search).pdf` | Problem formulation, uninformed and informed search |
| `Shared Materials/Handwritten Notebook/Scanned_20261117-0943.pdf` pp. 1–3, 9–12, 20–22, 28, 31–32, 35 | A*, heuristics, agents, hill climbing |

## 1. Introduction to AI

- **Video for this topic:** [The Foundations of Artificial Intelligence](https://www.youtube.com/watch?v=K5IgvclblDg) — D Sumathi.
- **AI** is the study of agents that perceive the environment and take actions to achieve goals.
- Foundations include philosophy, mathematics, economics, neuroscience, psychology, computer engineering, control theory, and linguistics.
- Historical phases: early enthusiasm, knowledge-based systems, machine learning, deep learning, and modern generative AI.
- **Applications:** robotics, games, natural language processing, computer vision, expert systems, recommendation systems, autonomous vehicles, healthcare, finance.
- **Pros:** automation, adaptability, pattern recognition, decision support.
- **Cons:** cost, bias, safety, privacy, explainability, job displacement.

## 2. Agents and environments

- **Video for this topic:** [Introduction to Intelligent Agents and their types](https://www.youtube.com/watch?v=BkedAnQfJ_U) — Gate Smashers.
- **Agent:** anything that perceives its environment through sensors and acts through actuators to achieve goals.
- **Agent structure:** environment → sensors → percepts → agent function/program → actions → actuators/effectors → environment.
- **Agent function** is the abstract mapping from percept sequence to action; the **agent program** is its implementation.
- **Agent types:**
  1. Simple reflex agent — reacts to current percept only.
  2. Model-based reflex agent — keeps internal state for partial observability.
  3. Goal-based agent — chooses actions to reach a goal.
  4. Utility-based agent — maximizes a utility function.
  5. Learning agent — improves with experience.
- **Environment properties:**
  - Fully observable vs partially observable
  - Deterministic vs stochastic
  - Episodic vs sequential
  - Static vs dynamic
  - Discrete vs continuous
- **Examples:** chess is fully observable and deterministic; self-driving car is partially observable, dynamic, and continuous; spam filter is partially observable, stochastic, and sequential.

## 3. State space search

- **Video for this topic:** [Uninformed vs Informed Search](https://www.youtube.com/watch?v=gZpUcsB9TFc) — Gate Smashers.
- **Video for uninformed search:** [Breadth First Search with example](https://www.youtube.com/watch?v=qul0f79gxGs) — Gate Smashers.

### Problem formulation

A search problem has:

- A set of states
- An initial state
- A set of actions/operators
- A goal test
- A path cost function

A **search strategy** chooses the order of node expansion. It is evaluated by:

- **Completeness:** finds a solution if one exists
- **Optimality:** finds a least-cost solution
- **Time complexity:** number of nodes generated
- **Space complexity:** maximum nodes kept in memory

Complexity is written in terms of `b` (branching factor), `d` (depth of the least-cost solution), and `m` (maximum depth).

### Uninformed search

| Strategy | Idea | Complete? | Optimal? | Time | Space |
|---|---|---|---|---|---|
| BFS | Explore level by level | Yes (finite) | Yes if uniform cost | `O(b^d)` | `O(b^d)` |
| DFS | Explore one branch deeply | No (infinite spaces) | No | `O(b^m)` | `O(bm)` |
| UCS | Expand lowest path cost | Yes | Yes | `O(b^d)` worst | `O(b^d)` |
| DLS | DFS with depth limit | No (depends on limit) | No | `O(b^l)` | `O(bl)` |
| IDDFS | Repeated DLS with increasing limit | Yes | Yes if uniform cost | `O(b^d)` | `O(bd)` |
| BDS | Search from start and goal | Yes (under conditions) | Yes if uniform cost | `O(b^(d/2))` | `O(b^(d/2))` |

**Key points:**

- BFS uses a queue (FIFO); DFS uses a stack (LIFO).
- DFS may get stuck in an infinite path; use a depth limit, visited set, or IDDFS.
- UCS is BFS for weighted graphs; use a priority queue ordered by `g(n)`.
- Repeated states cause duplicate work; a visited/closed set prevents cycles.

### Informed search

- **Video for this topic:** [A* Search solved example](https://www.youtube.com/watch?v=lusRf5v-TI0) — Mahesh Huddar.
- **Greedy best-first search** expands the node with the lowest heuristic `h(n)`. It is fast but not optimal and not complete in infinite spaces.
- **A*** expands the node with the lowest
  \[
  f(n) = g(n) + h(n)
  \]
  where `g(n)` is the cost from the start and `h(n)` is the estimated cost to the goal.
- **Admissible heuristic:** never overestimates the true cost, `h(n) <= h*(n)`. It guarantees A* optimality.
- **Consistent heuristic:** for every node `n` and successor `n'` with step cost `c(n,n')`,
  \[
  h(n) <= c(n,n') + h(n')
  \]
  It guarantees optimality and avoids reopening nodes.
- All consistent heuristics are admissible, but not all admissible heuristics are consistent.
- **Manhattan distance** is a common heuristic for the 8-puzzle when moves are horizontal/vertical.

## 4. Scanned notebook supplement

- **Video for hill climbing:** [Hill Climbing Algorithm](https://www.youtube.com/watch?v=3SiWtAnUROs) — Gate Smashers.
- A* worked example and heuristic comparison, pp. 1–3.
- Agents, percepts, and utility, pp. 9–12 and 20–22.
- Hill climbing and local search, pp. 28 and 31–32.
- Agent applications, p. 35.
- OCR is noisy; verify formulas against the page images.

## Quick revision sheet

- Agent = sensors + program + actuators.
- Search problem = states + initial state + actions + goal test + path cost.
- BFS: queue, complete, optimal for uniform cost, high memory.
- DFS: stack, low memory, incomplete, not optimal.
- UCS: priority queue by `g(n)`, complete and optimal.
- IDDFS: BFS completeness with DFS memory.
- A*: priority queue by `f = g + h`; optimal with admissible `h`.
- Repeated states: use visited/closed set; watch memory and reopening.
- Branching factor `b` drives exponential growth.

## Gaps

- Official syllabus not provided.
- AI lab manual not provided.
- Local search/hill climbing may be supplementary; confirm with teacher.
