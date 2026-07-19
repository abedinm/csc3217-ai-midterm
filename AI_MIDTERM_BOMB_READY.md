# AI Midterm: 2-Hour Bomb-Ready Pack

Built from every file in `D:\Downloads\AI`: 6 PDFs (171 pages), 5 decks (185 slides), and 14 images. OCR was used for scanned pages.

## What the papers predict

| Priority | Recurring question | What you must show |
|---|---|---|
| S | BFS / DFS simulation | Frontier after each expansion, explored set, expanded tree, final path, path cost |
| S | UCS simulation | Priority frontier ordered by cumulative `g`, replacement of expensive duplicate paths, expansion order, least-cost path |
| S | A* / GBFS | Calculate `h`; show `g,h,f`; ordered frontier; expansion order; final path and cost |
| S | 8-puzzle | Well-defined formulation; misplaced-tile and Manhattan heuristics; often GBFS tree/path |
| A | Alpha-beta pruning | Left-to-right minimax, every alpha/beta update, cut condition, crossed-out pruned branches, root decision |
| A | PEAS + environment | Four-column PEAS; classify observability, agents, determinism, episodic/sequential, static/dynamic, discrete/continuous, known/unknown |
| B | Short theory | Four AI approaches, rational agent, agent types, completeness/optimality, tree vs graph search, minimax |

Past-paper signal: Fall 2024-25 used UCS, alpha-beta, 8-puzzle formulation, PEAS, BFS/DFS, A*, and GBFS. Fall 2025-26 again used BFS/DFS, state-space formulation, environment classification, UCS, 8-puzzle heuristics/GBFS, and A*. Treat these as the core, not optional revision.

## Your 120-minute route

1. **0-12 min:** Memorize the formula/table sheet below.
2. **12-37 min:** Do Drill 1 (BFS/DFS) and Drill 2 (UCS) on paper.
3. **37-65 min:** Do Drill 3 (A*/GBFS) and Drill 4 (8-puzzle).
4. **65-85 min:** Do Drill 5 (alpha-beta).
5. **85-100 min:** Recite PEAS, environment classes, well-defined problem, and agent types.
6. **100-115 min:** Take the mini mock without notes.
7. **115-120 min:** Check errors; memorize the exam-writing templates.

## One-page memory sheet

### Selection rules

- **BFS:** pop shallowest; FIFO queue; goal at shallowest depth.
- **DFS:** pop deepest; LIFO stack. With “alphabetical order,” ensure the alphabetically first successor is popped first (push reverse-alphabetically if using a stack).
- **UCS:** pop lowest `g(n)` where `g` is cumulative path cost.
- **GBFS:** pop lowest `f(n)=h(n)`; ignores cost already paid.
- **A\*:** pop lowest `f(n)=g(n)+h(n)`.
- **Minimax:** MAX takes maximum; MIN takes minimum.
- **Alpha-beta:** alpha is MAX’s best guaranteed value; beta is MIN’s best guaranteed value; prune when `alpha >= beta`.

### Search properties

Let `b` = branching factor, `d` = shallowest solution depth, `m` = maximum depth, `l` = depth limit, `C*` = optimal solution cost, and `epsilon` = minimum positive step cost.

| Method | Complete? | Cost-optimal? | Time | Space |
|---|---|---|---|---|
| BFS | Yes if `b` finite | Yes only for equal/unit step costs | `O(b^(d+1))` | `O(b^(d+1))` (some slides write `O(b^d)`) |
| DFS | No in infinite/looping spaces; yes finite graph with repeated-state check | No | `O(b^m)` | `O(bm)` |
| DLS | Only if solution within `l` | No | `O(b^l)` | `O(bl)` |
| IDS | Yes if `b` finite | Yes for equal/unit step costs | `O(b^d)` | `O(bd)` |
| UCS | Yes if every cost >= `epsilon > 0` | Yes | `O(b^(1+floor(C*/epsilon)))` | Same order |
| GBFS | Generally no for tree search; graph search is complete only in finite spaces | No | worst `O(b^m)` | worst `O(b^m)` |
| A* | Yes under standard positive-cost conditions | Tree: admissible `h`; graph: consistent `h` | exponential worst case | exponential worst case |

**Admissible:** `0 <= h(n) <= h*(n)` (never overestimates true remaining cost).  
**Consistent:** for every edge `(n,n')`, `h(n) <= c(n,n') + h(n')`, and `h(goal)=0`. Consistency implies admissibility.

### Heuristics

- Manhattan distance: `|x_goal-x| + |y_goal-y|`.
- Euclidean distance: `sqrt((x_goal-x)^2 + (y_goal-y)^2)`.
- 8-puzzle `h1`: number of misplaced numbered tiles; do **not** count blank.
- 8-puzzle `h2`: sum of Manhattan distances of numbered tiles; do **not** count blank.
- Usually `h2 >= h1` and `h2` dominates `h1` while both remain admissible.
- Weighted evaluation from a past paper: `f=(2-w)g+wh` gives UCS at `w=0` (scaled `2g`), A* at `w=1`, and GBFS at `w=2` (scaled `2h`). Positive scaling does not change ordering.

## The examiner-friendly simulation format

Use this table for every graph search. A node is normally added to explored when it is **popped/expanded**, not when generated.

| Step | Pop/expand | Frontier after adding successors | Explored | Parent/cost update |
|---:|---|---|---|---|
| 0 | - | `[S]` | `{}` | `g(S)=0` |
| 1 | S | ... | `{S}` | ... |

Rules that save marks:

- State your tie-break: “ascending alphabetic order.”
- Show whole paths in a UCS/A* frontier if duplicate states could occur: `S-A-D:7`.
- If a cheaper route reaches a frontier state, replace its cost and parent.
- In graph search, do not re-expand explored states unless the stated A* variant reopens a state after a lower `g`.
- Stop when the goal is **popped**, not merely generated, for UCS and A*. For BFS classroom conventions, follow the lecturer’s stated goal-test timing and say which convention you use.
- Reconstruct final path from parent links; path cost is the sum of edge costs, never `h` or `f`.

## Drill 1 — BFS and DFS

Undirected/unweighted graph, neighbors considered alphabetically:

`S:{A,B,C}; A:{D,E}; B:{E}; C:{F}; D:{G}; E:{G}; F:{G}`. Goal `G`. Every edge costs 1.

### BFS answer

Queue trace (duplicates already in frontier/explored are ignored):

| Pop | Frontier afterward | Explored |
|---|---|---|
| S | `[A,B,C]` | `S` |
| A | `[B,C,D,E]` | `S,A` |
| B | `[C,D,E]` | `S,A,B` |
| C | `[D,E,F]` | `S,A,B,C` |
| D | `[E,F,G]` | `S,A,B,C,D` |
| E | `[F,G]` | `S,A,B,C,D,E` |
| F | `[G]` | `S,A,B,C,D,E,F` |
| G | goal | `S,A,B,C,D,E,F,G` |

Path `S-A-D-G`, cost 3. BFS is optimal here because all edge costs are equal.

### DFS answer

Alphabetically first child is visited first: `S -> A -> D -> G`. Stack implementation pushes `C,B,A`, then `E,D`. Path cost 3. DFS happens to find an optimal path here, but DFS is **not guaranteed** optimal.

## Drill 2 — UCS

Directed weighted graph:

`S->A(2), S->B(5), S->C(9), A->B(1), A->D(4), B->D(1), B->G(8), D->G(3), C->G(1)`.

| Pop | Ordered frontier after expansion | Important update |
|---|---|---|
| S:0 | `A:2, B:5, C:9` | - |
| A:2 | `B:3, D:6, C:9` | replace `B:5` by `B:3` |
| B:3 | `D:4, C:9, G:11` | replace `D:6` by `D:4` |
| D:4 | `G:7, C:9` | replace `G:11` by `G:7` |
| G:7 | goal | stop |

Expansion order: `S,A,B,D,G`. Solution `S-A-B-D-G`; cost `2+1+1+3=7`.

## Drill 3 — A* versus GBFS

Use the same edges as Drill 2 and heuristics: `h(S)=6, h(A)=5, h(B)=4, h(C)=1, h(D)=3, h(G)=0`.

### A* answer

- From S: `A(g2,h5,f7)`, `B(5,4,9)`, `C(9,1,10)`; pop A.
- From A: improve B to `(3,4,7)`; add D `(6,3,9)`; pop B.
- From B: improve D to `(4,3,7)`; add G `(11,0,11)`; pop D.
- From D: improve G to `(7,0,7)`; pop G.
- Path `S-A-B-D-G`, cost 7.

### GBFS answer

- From S, smallest `h` is C (`h=1`), then C generates G (`h=0`).
- Path `S-C-G`, actual cost `9+1=10`.
- Lesson: GBFS can be faster but non-optimal because it ignores `g`.

## Drill 4 — 8-puzzle

Initial:

```text
2 8 3
1 6 4
7 _ 5
```

Goal:

```text
1 2 3
8 _ 4
7 6 5
```

- Misplaced tiles: `1,2,6,8` -> `h1=4`.
- Manhattan: tile 1 = 1, tile 2 = 1, tile 6 = 1, tile 8 = 2; others 0 -> `h2=5`.
- Blank is excluded.

For a GBFS tree: generate each legal blank move, compute `h` for every child, choose the lowest `h`, apply the stated tie-break, and continue. Label each state with `h`; show parent arrows and the final move sequence.

### Well-defined 8-puzzle formulation

- **Initial state:** the stated arrangement of eight tiles and blank.
- **Actions:** move blank Up/Down/Left/Right when legal (equivalently slide an adjacent tile into blank).
- **Transition model:** returns the board after swapping blank with the selected adjacent tile.
- **Goal test:** current board equals target arrangement.
- **Path cost:** usually 1 per move; total number of moves.
- State space reachable from one configuration is `9!/2 = 181,440`; action branching factor is 2 at corners, 3 at edges, 4 at center (average below 3).

## Drill 5 — minimax with alpha-beta

Search left-to-right. Root MAX has MIN children A, B, C. Their MAX grandchildren have leaves:

- A: `A1=[3,5]`, `A2=[6,9]`
- B: `B1=[1,2]`, `B2=[0,-1]`
- C: `C1=[7,4]`, `C2=[5,8]`

Answer:

1. A1 returns max(3,5)=5. At A(MIN), beta=5. A2 sees 6 first; at A2(MAX), alpha becomes 6, so `alpha 6 >= beta 5`: prune leaf 9. A returns 5. Root alpha=5.
2. At B(MIN), B1 returns 2, so beta=2. Since root alpha 5 >= beta 2, prune all of B2. B returns 2. Root remains 5.
3. C1 returns 7, so C beta=7. C2 evaluates both leaves and returns 8; C returns min(7,8)=7.
4. Root returns max(5,2,7)=7 and chooses C.

Always write starting bounds at the root: `alpha=-infinity, beta=+infinity`. MAX updates alpha; MIN updates beta. Alpha-beta gives the same move/value as minimax; ordering only changes how much it prunes.

## PEAS and agent theory

### PEAS template

| P — Performance | E — Environment | A — Actuators | S — Sensors |
|---|---|---|---|
| correctness, speed, safety, low cost/waste, user satisfaction | objects, workspace, people, obstacles, lighting/weather | motors, arms, grippers, wheels, displays, speakers, valves | camera, proximity, touch, weight, color, GPS, microphone, chemical sensors |

Candy/apple sorting robot example:

- **P:** correct classification/bin, high throughput, no damage, low contamination/energy, safety.
- **E:** conveyor, mixed items, bins/jars, workspace, workers, lighting.
- **A:** conveyor control, robotic arm, gripper, diverter, alarm.
- **S:** RGB/depth camera, color/shape/weight sensor, proximity/position sensor, bin-level sensor.

### Environment classification sentence

Write all dimensions with one-line reasons: “It is **single-agent** (no strategic opponent), **partially observable** if hidden dirt/internal state cannot be sensed, **stochastic** if sensing/action outcomes are uncertain, **sequential** because an action changes later choices, **dynamic** if the world can change while deliberating, **discrete** for finite locations/actions, and **known** if transition effects/costs are supplied.” Classification depends on the assumptions—state them.

### Agent types

- Simple reflex: current percept -> condition-action rule; no memory.
- Model-based reflex: internal state/model handles partial observability.
- Goal-based: chooses actions that reach a goal; requires search/planning.
- Utility-based: maximizes expected utility; trades off competing outcomes and uncertainty.
- Learning agent: performance element acts; learning element improves it; critic supplies feedback; problem generator encourages exploration.

### Four views of AI

- Acting humanly: Turing Test.
- Thinking humanly: cognitive modeling.
- Thinking rationally: laws of thought.
- Acting rationally: rational-agent approach.

Standard Turing Test needs natural-language processing, knowledge representation, automated reasoning, and machine learning. The total/extended test also needs computer vision and robotics.

### Tree search versus graph search

Tree search may generate the same state many times and can loop; it stores the frontier but no explored set. Graph search stores an explored/closed set, avoids repeated expansion/cycles, and usually costs more memory.

## 15-minute mini mock

Do not read the key until finished.

1. Why can BFS return a higher-cost path than UCS? (2)
2. In A*, a frontier contains `A(g=5,h=4)`, `B(6,1)`, `C(3,5)`. What is popped, assuming lowest `f`, then alphabetic tie-break? (2)
3. Give the consistency test for edge `X->Y` with cost 3 if `h(X)=8`, `h(Y)=4`. (2)
4. For 8-puzzle, should blank count in misplaced tiles or Manhattan distance? (1)
5. A MIN node currently has beta=6. Its MAX child, called with alpha=7, is about to be searched. Can it be pruned? Why? (2)
6. Give PEAS for a water-purifying agent: at least two items per category. (4)
7. State when UCS is complete and optimal. (2)
8. Formulate a three-room vacuum problem as initial state, actions, transition, goal test, and path cost. (5)

### Key

1. BFS minimizes depth/number of edges, not cumulative cost; UCS orders by `g`.
2. `f(A)=9`, `f(B)=7`, `f(C)=8`; pop B.
3. Consistency requires `8 <= 3+4`; false, so the heuristic is inconsistent on this edge.
4. No; exclude blank.
5. Yes. `alpha=7 >= beta=6`, so the branch cannot improve the ancestor’s choice.
6. P: purity, throughput, safety, low energy/waste. E: raw water, tank/pipes, contaminants, users. A: pumps, valves, heater/filter/backwash/alarm. S: turbidity, pH, TDS/conductivity, flow/pressure/level sensors.
7. Complete if step costs are bounded below by positive epsilon; cost-optimal under nonnegative/positive stated costs with the goal accepted when popped.
8. State `(robot_position, left_clean?, middle_clean?, right_clean?)`; actions Left/Right/Clean where legal; transition moves robot or marks current room clean; goal all rooms clean; path cost sum of action costs.

## Exam execution checklist

- Circle the start and goal; copy every edge cost and heuristic before simulating.
- Write the evaluation rule (`g`, `h`, or `g+h`) at the top.
- Declare successor/tie order.
- Use one row per expansion; never jump straight to a path.
- For A*, keep `g`, `h`, and `f` separate. For GBFS, report actual path cost even though selection used only `h`.
- For alpha-beta, mark MAX/MIN levels and carry `(alpha,beta)` to every visited node.
- For theory, definition first, condition/caveat second, tiny example last.
- If graph details are ambiguous, explicitly state your convention. Correct, consistent simulation earns marks.
