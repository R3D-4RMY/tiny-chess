# Tiny Chess

An original Python chess engine for make.fun's tiny-chess-01 bounty ($500).

## Engine

`main.py` is the entrypoint (a packed build of `engine.py`, the readable
source, via the kit's `makefun compress`). It is an original 0x88-board
engine: alpha-beta search with PVS, a transposition table, killer moves,
MVV-LVA capture ordering, null-move and late-move-reduction pruning,
quiescence over captures/promotions/check evasions, and a material +
piece-square evaluation (Michniewski tables) with a bishop-pair bonus
(50) and a +10 tempo bonus for the side to move. Tuned v2: practice Elo
mean 1,367 over 3 trials (1,364 / 1,191 / 1,545), up from the 1,276
baseline (tempo + bishop-pair change; search and pawn-structure variants
tested worse and were discarded).
Search is deterministic: a fixed node budget per move (80,000 nodes early,
50,000 mid-game, 25,000 late), never a clock, no unseeded randomness.

## Run a practice trial

From the kit directory (`~/workspace/makefun/tiny-chess-01-kit/`), start the
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
