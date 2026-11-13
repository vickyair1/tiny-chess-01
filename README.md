# tiny-chess-01 entry

A compact chess engine in a single `main.py` (packed with `makefun compress`
from the readable source; see the submission's transcript bundle for it).

- 10x12 mailbox board, negamax + alpha-beta with iterative deepening
- Fixed 50,000-node budget per move (deterministic: no clock, no randomness)
- Quiescence over captures/promotions, with full check-evasion search
- Transposition table, MVV-LVA + killer move ordering
- Material + piece-square evaluation, repetition-aware (draw = 0)

`main.py` speaks the competition env protocol (`MAKEFUN_ENV_URL`) and nothing
else. No model calls, no network beyond the env.
