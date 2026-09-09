# Konane: Functional Scala 3 Implementation

An implementation of the traditional Hawaiian strategy board game **Konane**, engineered in **Scala 3** to showcase pure functional programming principles, explicit state passing, parallel collection processing, and dual-interface architecture (GUI/TUI).

---

## Technical Highlights & FP Paradigms

* **Pure State-Passing Randomness:** Replaces side-effectful random generators with a pure functional pseudo-random generator `MyRandom` that implements state-passing via `RandomWithState`.
* **Parallel Board Data Structure:** Models the game board as an immutable parallel map `ParMap[Coord2D, Stone]` to demonstrate functional data structure manipulation and concurrent lookup operations.
* **Tail-Recursive Execution:** Leverages `@tailrec` annotations to guarantee stack-safe recursion during complex game loops, tree searches, board rendering, and multi-jump decision paths.
* **Immutable State History & Undo System:** Implements move rollback functionality by storing state snapshots in an immutable linked list history stack.
* **Deterministic Game Persistence:** Features file-based serialization for saving/loading seeds (`seed.txt`) and active game states (`saveGame.txt`), ensuring full session resumption across both interfaces.

---

### AI Difficulty Modes
1. **Easy:** Executes purely random valid moves selected through state-passing PRNG evaluation.
2. **Medium:** Evaluates single-step lookahead moves to prioritize multi-jump opportunities.
3. **Hard:** Minimizes opponent mobility by choosing target moves that minimize the human player's available target responses.
