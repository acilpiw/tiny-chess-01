# tiny-chess-01 — 4 KB chess engine

A chess engine in at most 4,096 bytes of Python (`main.py`), built for the
make.fun tiny-chess-01 competition. It plays the full 16-game house gauntlet
through the env at `MAKEFUN_ENV_URL` and exits when the env reports done.

## How it works

- 0x88 board, fully legal move generation (castling, en passant, promotions).
- Negamax alpha-beta search with a fixed node budget (24,000 nodes a move) —
  never a clock, so every trial replays move for move.
- Transposition table (Zobrist), null-move pruning, late-move reductions,
  check extensions, killer-move ordering, MVV-LVA capture ordering.
- Quiescence search over captures and check evasions.
- Evaluation: material plus piece-square tables (middlegame king table
  keeps the king sheltered in the corner).
- `main.py` ships as an lzma payload with its unpacker; the payload and the
  unpacker together stay under the 4,096-byte cap.

## Rules it respects

- Python 3.13, standard library only; reads no other file of the repository.
- No model calls, no network beyond the env, no randomness, no wall clock.

MIT licensed, see LICENSE.
