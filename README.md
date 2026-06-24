# Tic-Tac-Toe with AI

An unbeatable Tic-Tac-Toe game featuring an AI opponent powered by the Minimax algorithm.

## How to Run

```bash
python runner.py
```

Requires Python 3 and Pygame.

## Files

- **`tictactoe.py`** — Game logic: board state, win detection, and the Minimax AI.
- **`runner.py`** — Pygame-based GUI. Choose to play as X or O, then click a cell to move.

## Minimax Algorithm

Minimax is a recursive decision-making algorithm used in two-player zero-sum games like Tic-Tac-Toe. The core idea: each player picks the move that gives them the best result assuming the opponent also plays optimally.

### Key Concepts

**State space** — The game board at any point. Each state branches into child states (possible moves).

**Utility function** — Assigns a numeric score to terminal states: `+1` if X wins, `-1` if O wins, `0` for a tie.

**Maximizing player (X)** — Tries to reach states with the highest utility.  
**Minimizing player (O)** — Tries to reach states with the lowest utility.

### How It Works

1. Generate the full game tree from the current board to all terminal states.
2. Score terminal states using the utility function.
3. Propagate scores upward:
   - At a **max** node (X's turn), pick the maximum child score.
   - At a **min** node (O's turn), pick the minimum child score.
4. The root chooses the action leading to the best propagated score.

### Complexity

The branching factor for Tic-Tac-Toe starts at 9 and decreases by 1 each move. The total number of board states is `9! = 362,880` in the worst case — small enough for naive Minimax to run instantly. For larger games like Chess or Go, the state space is astronomically larger, making Minimax impractical without optimisations.

### Alpha-Beta Pruning

A common optimisation that cuts off entire branches of the game tree without exploring them. Two values are tracked:

- **Alpha** — the best score the maximiser can guarantee so far.
- **Beta** — the best score the minimiser can guarantee so far.

If at any node `alpha >= beta`, further exploration is pointless — the opponent will never let the game reach those states. Alpha-beta pruning can double the search depth reachable in the same time.

### Limitations

- Minimax assumes perfect play from both sides — it doesn't model bluffs or probabilistic outcomes.
- Without pruning or depth limits, it's intractable for games with large branching factors.
- It requires a full or deep partial game tree; for stochastic games, expectiminimax is used instead.
