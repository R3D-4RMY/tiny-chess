# Tiny Chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/R3D-4RMY/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/R3D-4RMY/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original Python chess engine for [make.fun](https://make.fun/bounty/tiny-chess-01)'s tiny-chess-01 bounty ($500).

## Engine

`main.py` is the entrypoint (a packed build of `engine.py`, the readable
source, via the kit's `makefun compress`). It is an original 0x88-board
engine: alpha-beta search with PVS, a transposition table, killer moves,
MVV-LVA capture ordering, null-move and late-move-reduction pruning,
quiescence over captures/promotions/check evasions, and a material +
piece-square evaluation (Michniewski tables) with a bishop-pair bonus
(60), a +15 tempo bonus for the side to move, and an endgame king
piece-square weight of 8. Tuned v3 (round 2): practice Elo mean 1,453
over 3 trials (1,545 / 1,451 / 1,364), up from the 1,367 baseline
(tempo 15, bishop pair 60, endgame king PST weight 8; king-safety and
rook-open-file variants tested worse and were discarded).
Search is deterministic: a fixed node budget per move (80,000 nodes early,
50,000 mid-game, 25,000 late), never a clock, no unseeded randomness.

## Run a practice trial

From the kit directory (`~/workspace/makefun/tiny-chess-01-kit-v20/tiny-chess-01-kit/`), start the
env and point the bot at `main.py`:

```sh
# env on port 18080, trial 0 (see program/env/server.mjs)
MAKEFUN_ENV_DATA_DIR=~/workspace/makefun/tiny-chess-01-kit/practice/trial-0/input/env \
MAKEFUN_STATE_DIR=/tmp/chess-state MAKEFUN_ENV_PORT=18080 \
node program/env/server.mjs &
MAKEFUN_ENV_URL=http://127.0.0.1:18080 python3 main.py
```

Or use the kit CLI: `node cli/makefun.mjs check` (from the kit dir) and
`node cli/makefun.mjs grade-local` (needs Docker for the Python sandbox).

## License

MIT. See LICENSE.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
