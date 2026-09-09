# Konane: Functional Scala 3 Implementation

An implementation of the traditional Hawaiian strategy board game **Konane**, engineered in **Scala 3** to showcase pure functional programming principles, explicit state passing, parallel collection processing, and dual-interface architecture (GUI/TUI). Built as a showcase project for enrollment in the **MSc Computer Science** program at the Technical University of Denmark (DTU).

---

## Technical Highlights & FP Paradigms

* **Pure State-Passing Randomness:** Replaces side-effectful random generators with a pure functional pseudo-random generator `MyRandom` that implements state-passing via `RandomWithState`.
* **Parallel Board Data Structure:** Models the game board as an immutable parallel map `ParMap[Coord2D, Stone]` to demonstrate functional data structure manipulation and concurrent lookup operations.
* **Tail-Recursive Execution:** Leverages `@tailrec` annotations to guarantee stack-safe recursion during complex game loops, tree searches, board rendering, and multi-jump decision paths.
* **Immutable State History & Undo System:** Implements move rollback functionality by storing state snapshots in an immutable linked list history stack.
* **Deterministic Game Persistence:** Features file-based serialization for saving/loading seeds (`seed.txt`) and active game states (`saveGame.txt`), ensuring full session resumption across both interfaces.

---

## Game Architecture & AI Strategies

The project separates functional core domain logic from side-effecting UI layers.

| Component | Responsibility | Technical Implementation |
| :--- | :--- | :--- |
| **Engine Core** | Game rules, move generation, parallel board initialization, jump validations. | Immutable data structures, `ParMap`, tail-recursive validation functions. |
| **Pure PRNG** | Seed loading, state-passing random number generation. | Trait `RandomWithState` and class `MyRandom` returning `(Int, RandomWithState)` pairs. |
| **JavaFX GUI** | Graphical user interface with dynamic rendering, board scaling, timers, and animations. | Integrated via ScalaFX/JavaFX FXML controllers (`GameController`, `InitialMenu`). |
| **Terminal UI** | Lightweight CLI interface for pure terminal interaction. | Functional text-builder using recursive folds (`foldRight`) and terminal input loops. |
| **Main Launcher** | Central application entry point providing interface switching. | CLI menu routing user to either GUI or TUI runtime environments. |

### AI Difficulty Modes
1. **Easy:** Executes purely random valid moves selected through state-passing PRNG evaluation.
2. **Medium:** Evaluates single-step lookahead moves to prioritize multi-jump opportunities.
3. **Hard:** Minimizes opponent mobility by choosing target moves that minimize the human player's available target responses.
