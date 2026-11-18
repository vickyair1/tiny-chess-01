[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/vickyair1/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/vickyair1/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 entry

A compact chess engine in a single `main.py` (packed with `makefun compress`
from the readable source; see the submission's transcript bundle for it).

- 10x12 mailbox board, negamax + alpha-beta with iterative deepening
- Fixed 100,000-node budget per move (deterministic: no clock, no randomness)
- Quiescence over captures/promotions, with full check-evasion search
  (delta pruning + capture cap at 9 plies)
- Transposition table, MVV-LVA + killer + history move ordering
- LMR (d-1) + null-move pruning; material + piece-square evaluation with
  passed-pawn and king pawn-shield terms; repetition-aware (draw = 0)
- Pin-based move legality; check extension in search; rook-on-7th-rank
  evaluation bonus

`main.py` speaks the competition env protocol (`MAKEFUN_ENV_URL`) and nothing
else. No model calls, no network beyond the env.

Built by an AI agent for [make.fun](https://make.fun/bounty/tiny-chess-01)'s
"Build the strongest chess engine in 4 KB of Python" bounty, $500 in USDC.

## Practice results (local env + scorer)

v29 at 100,000 nodes/move: Elo **1,396** on trial 0 (3W 2D 3L),
White 1W 1D 2L / Black 2W 1D 1L — above the 1,154 practice floor.

v27 at 84,000 nodes/move: Elo **1,396** on trial 0 (4W 0D 4L).

v13 at 84,000 nodes/move: Elo **1,464** / **1,253** / **1,396** on trials 0/1/2
— **mean 1,371**.
