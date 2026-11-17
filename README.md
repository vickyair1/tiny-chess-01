# tiny-chess-01 entry

A compact chess engine in a single `main.py` (packed with `makefun compress`
from the readable source; see the submission's transcript bundle for it).

- 10x12 mailbox board, negamax + alpha-beta with iterative deepening
- Fixed 75,000-node budget per move (deterministic: no clock, no randomness)
- Quiescence over captures/promotions, with full check-evasion search
  (delta pruning + capture cap at 9 plies)
- Transposition table, MVV-LVA + killer + history move ordering
- LMR + null-move pruning; material + piece-square evaluation with
  passed-pawn and king pawn-shield terms; repetition-aware (draw = 0)
- Check extension in search; rook-on-7th-rank evaluation bonus

`main.py` speaks the competition env protocol (`MAKEFUN_ENV_URL`) and nothing
else. No model calls, no network beyond the env.

## Practice results (local env + scorer)

v10 at 75,000 nodes/move: Elo **1,326** / **1,396** / **1,326** on trials 0/1/2
(3W 1D 4L, 3W 2D 3L, 3W 1D 4L) — **mean 1,349**, above the house
baseline's practice mean (1,325) and the 1,154 practice floor. Beat
nodes-250k (1,497) in 2 of 3 trials; drew nodes-500k once and nodes-1M once.

v9 at 75,000 nodes/move: Elo **1,396** / **1,326** / **1,253** on trials 0/1/2
(4W 0D 4L, 3W 1D 4L, 2W 2D 4L) — **mean 1,325**, exactly the house
baseline's practice mean, above the 1,154 practice floor.

v3 at 50,000 nodes/move: Elo **1,087** on trial-0 (1W 2D 5L) — below the
floor; superseded by v9, then v10.
