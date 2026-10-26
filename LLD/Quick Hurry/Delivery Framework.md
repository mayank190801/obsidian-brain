
WE NEED TO WRAP UP INTO MORE SHORT NOTES (important) -- first draft basically 
### 1) Requirements (~5 minutes)

- spend around 2-3 minutes around this 
### core themes
- **Primary capabilities** — What operations must this system support?
- **Rules and completion** — What conditions define success, failure, or when the system stops or transitions state?
- **Error handling** — How should the system respond when inputs or actions are invalid?
- **Scope boundaries** — What areas are _in_ scope (core logic, business rules) and what areas are explicitly _out_ (UI, storage, networking, concurrency, extensibility)?

Example 
```
Requirements:
1. Two players alternate placing X and O on a 3x3 grid.
2. A player wins by completing a row, column, or diagonal.
3. The game ends in a draw if all nine cells are filled with no winner.
4. Invalid moves should be rejected (placing on an occupied cell, acting after the game is over).
5. The system should provide a way to query current game state and reset the game.

Out of Scope:
- UI/rendering layer
- AI opponent or move suggestions
- Networked multiplayer
- Variable board sizes (NxN grids)
- Undo/redo functionality
```

### 2) Entities and Relationships (~5 minutes)
#### Identify Entities
- If something maintains changing state or enforces rules, it likely deserves to be its own entity.
- If it’s just information attached to something else, it’s probably just a field on another class.

#### Define Relationships
- Which entity is the orchestrator — the one driving the main workflow?
- Which entities own durable state?
- How do they depend on each other? (has-a, uses, contains)
- Where should specific rules logically live?

Example 
```
Entities:
- Game
- Board
- Player

Relationships:
- Game -> Board
- Game -> Player (2x)
```


### 3) Class Design (~10-15 minutes)

You’ll now go entity by entity, working top-down. Start with the orchestrator (for Tic Tac Toe, this is the Game class), then move down to the supporting entities (Board, Player, etc.).

For each entity, you'll answer two questions:
1. **State** - What does this class need to remember to enforce the requirements?
2. **Behavior** - What does this class need to do, in terms of operations or queries?

Basically connect the requirement to entities and create and attach states to it

Requirements and what state it should have!!
```
"Two players alternate placing X and O on a 3x3 grid."
The two players, whose turn it is, and the Board

"The game ends when a player wins or the board is full."	
Game state (in progress, won, draw) and the winner (if any)
```

```
Game – State:
- board: Board
- playerX: Player
- playerO: Player
- currentPlayer: Player
- state: GameState (IN_PROGRESS, WON, DRAW)
- winner: Player? (null if no winner)
```

After states are derived, move on to behaviours 
```
Need from requirements   	Method on Game
Players need to make moves	makeMove(player, row, col) returns bool
Ask whose turn it is	    getCurrentPlayer() returns Player
Check game state	        getGameState() returns GameState
See who won	                getWinner() returns Player?
Inspect the board	        getBoard() returns Board
```

#### Important
As you work through state and behavior, anchor on one principle: **keep rules with the entity that owns the relevant state**. This is encapsulation, sometimes called "Tell, Don't Ask" - objects should manage their own state and expose behavior, not getters for callers to make decisions. Workflow and lifecycle rules (like "can this operation run right now?") belong in the orchestrator. Data-specific rules (like "is this cell already occupied?") belong in the entity that owns that data. This keeps your APIs small and makes your design predictable—when something breaks, you know exactly which class to check.

Final example (actually beautiful how this is derived!)

```
class Game:
  - board: Board
  - playerX: Player
  - playerO: Player
  - currentPlayer: Player
  - state: GameState (IN_PROGRESS, WON, DRAW)
  - winner: Player? (null if no winner)

  + makeMove(player, row, col) -> bool
  + getCurrentPlayer() -> Player
  + getGameState() -> GameState
  + getWinner() -> Player?
  + getBoard() -> Board
```


Actual UML Diagram not required (simple design works!) 
So don't stress about it brother

### 4) Implementation (~10 minutes)

 ## Important
Different companies expect different levels of detail here, so **always ask your interviewer what they prefer** before you start writing. Most interviews only need pseudo-code for the key methods. Some companies want near-complete code in a specific language. Others just want you to talk through the logic. Focus on the most interesting methods—the ones that truly define system behavior.

- first write the happy path 
- move to edge cases 
- psuedo code, and then be converted to actual code 
- don't include design patterns, and don't forget to include one 
- verify by running the code to test if everything works as expected
- fix the bug on the spot (don't let interviewer find it)

### 5) Extensibility (~5 minutes, if time and level allow)

- how your code handles it without much restructuring 
- you dont need to code this part 
- 






























