# Tiny Chess 4K — Rich Eval

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Rifat7600/tiny-chess-01-4/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Rifat7600/tiny-chess-01-4/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in under 4 KB of Python, written for make.fun's
"Build the strongest chess engine in 4 KB of Python" bounty.

## How it plays

The engine uses a 0x88 board and a negamax alpha-beta search with
quiescence search, a transposition table, killer moves and null-move
pruning. Every move is searched to a fixed budget of 45,000 nodes —
no clock anywhere, so a trial replays move for move.

The evaluation goes beyond material and piece-square tables: it adds
a bishop-pair bonus, passed-pawn bonuses that grow as the pawn
advances, a king-safety term from the pawn shield in front of the
king (with a centralising king bonus in the endgame), and a mobility
term from the difference in pseudo-legal move counts.

The search deepens one ply at a time at the root; when the node
budget runs out mid-iteration, the best move of the last completed
depth stands. Transposition-table entries are keyed on the full
position (board, side to move, castling rights, en passant square),
so they stay valid across the whole game, and positions repeated
along a search path score as draws. The driver talks to the trial
environment over HTTP: it asks for the game in play, parses the FEN,
searches, and posts its move in UCI.

## Files

- `main.py` — the whole engine (3,994 bytes, standard library only)
- `source.py` — the readable source `main.py` was packed from
- `LICENSE` — MIT
