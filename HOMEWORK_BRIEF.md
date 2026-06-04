# Weekly Coding #9: Midnight Monster Delivery

## Due

**Sun 2026-05-17 23:59**

## Topic

Shortest paths with **Dijkstra's algorithm** using a heap-based priority queue.

## Story

The city gets weird after midnight.

Your delivery company serves supernatural customers: vampires, werewolves, ghosts, goblins, swamp creatures, and other night-shift problems. Each delivery location is connected by haunted roads. Every road has a travel cost based on danger, distance, fog, traffic, and general monster nonsense.

Your job is to build a route planner that finds the cheapest safe delivery route.

You will receive a weighted graph where:

- each key is a location
- each value is a dictionary of neighboring locations
- each neighbor has a travel cost

Your program must calculate the cheapest delivery route using **Dijkstra's algorithm**.

---

## Repo Structure

```text
src/challenges.py
tests/test_challenges.py
README.md
.github/workflows/tests.yml
```

Only `src/challenges.py`, `tests/test_challenges.py`, and `README.md` are graded.

---

## Required Functions

Implement all three required functions in `src/challenges.py`.

### 1. `validate_haunted_map`

```python
def validate_haunted_map(graph: dict[str, dict[str, int]]) -> None:
    """Raise ValueError if the haunted map is invalid."""
```

A valid haunted map:

- is a dictionary
- each node points to a dictionary of neighbors
- every neighbor is also listed as a node in the graph
- every edge weight is positive
- no zero weights
- no negative weights

If the graph is invalid, raise `ValueError`.

---

### 2. `monster_delivery_costs`

```python
def monster_delivery_costs(
    graph: dict[str, dict[str, int]],
    start: str,
) -> dict[str, float]:
    """Return the cheapest delivery cost from start to every location."""
```

Rules:

- Use Dijkstra's algorithm.
- Use `heapq` for the priority queue.
- If `start` is missing, raise `ValueError`.
- Unreachable locations should stay as `math.inf`.

---

### 3. `shortest_monster_delivery`

```python
def shortest_monster_delivery(
    graph: dict[str, dict[str, int]],
    start: str,
    target: str,
) -> tuple[float, list[str]]:
    """Return the cheapest cost and path from start to target."""
```

Rules:

- Use Dijkstra's algorithm.
- Use `heapq` for the priority queue.
- Reconstruct the path using a `previous` map.
- If `start` or `target` is missing, return `(math.inf, [])`.
- If `target` is unreachable, return `(math.inf, [])`.
- If `start == target`, return `(0, [start])`.

---

## Stretch Function

This is optional. It is not required for Meets, but it can provide Exceeds-level evidence if implemented well.

### `best_next_monster_stop`

```python
def best_next_monster_stop(
    graph: dict[str, dict[str, int]],
    start: str,
    targets: list[str],
) -> tuple[str, float]:
    """Return the reachable target with the cheapest delivery cost."""
```

Story version:

Three monsters placed orders at the same time. Which delivery should the driver make first?

Rules:

- Ignore unreachable targets.
- If no target is reachable, return `("", math.inf)`.
- If there is a tie, return the target that appears first in the `targets` list.

---

## Example Graph

```python
HAUNTED_CITY = {
    "Crypt Kitchen": {
        "Fog Alley": 2,
        "Bone Bridge": 5,
    },
    "Fog Alley": {
        "Moon Bridge": 1,
        "Goblin Market": 6,
    },
    "Bone Bridge": {
        "Goblin Market": 2,
    },
    "Moon Bridge": {
        "Werewolf Den": 5,
        "Goblin Market": 3,
    },
    "Goblin Market": {
        "Vampire Tower": 5,
    },
    "Werewolf Den": {
        "Vampire Tower": 2,
    },
    "Vampire Tower": {},
}
```

Expected shortest path:

```python
shortest_monster_delivery(
    HAUNTED_CITY,
    "Crypt Kitchen",
    "Vampire Tower",
)
```

Returns:

```python
(
    10,
    ["Crypt Kitchen", "Fog Alley", "Moon Bridge", "Werewolf Den", "Vampire Tower"],
)
```

---

## Complexity Requirement

In your README, explain the complexity of your Dijkstra functions.

Expected explanation:

```text
Time complexity: O((V + E) log V)
Space complexity: O(V) extra space, or O(V + E) including graph storage
```

Where:

- `V` = number of locations/nodes
- `E` = number of roads/edges

---

## Edge Cases to Handle

Your code and/or tests should consider:

- start equals target
- target is unreachable
- start node is missing
- target node is missing
- node has no outgoing edges
- graph contains cycles
- tied shortest paths
- negative edge weight
- zero edge weight
- neighbor not listed as a graph node

---

## Standards Evidence

This assignment primarily provides evidence for:

- **S12 — Graphs + BFS/DFS + Dijkstra**
- **S11 — Heaps + Priority Queue**
- **S3 — Big-O Reasoning**

---

## Submission Checklist

Before submitting:

- [ ] `pytest -q` passes
- [ ] `src/challenges.py` contains your implementation
- [ ] `tests/test_challenges.py` includes any extra tests you added
- [ ] `README.md` is complete
- [ ] README includes complexity reasoning
- [ ] README includes an edge-case checklist
- [ ] README includes Assistance & Sources
- [ ] Code uses Python 3.11+
- [ ] Code uses only the standard library
