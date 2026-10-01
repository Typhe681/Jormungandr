# Ouroboros

Ouroboros is an esoteric programming language based on Brainfuck. It keeps Brainfuck's core (pointer, byte cells, bracket loops, and the original commands) but the memory becomes a *ring of cells that can grow and shrink while the program runs.*

You can try it out here: https://typhe.dev/ouroboros

## Memory

- Memory is effectively an infinite ring that starts with one cell.
- Commands that pass through one end wrap to the other end.
- Each cell holds 0-255, which also wraps.
- The ring can grow (`^`, `=`, `?`) and shrink (`X`) as the program runs.

## Commands

Many commands can use an optional number suffix `n` right after it (`+5`, `>3`, `^2`). Without one, `n` is 1.

| Command | Meaning |
| --- | --- |
| `>` / `>n` | Move the pointer right 1 / n cells |
| `<` / `<n` | Move the pointer left 1 / n cells |
| `+` / `+n` | Add 1 / n to the current cell (mod 256) |
| `-` / `-n` | Subtract 1 / n from the current cell (mod 256) |
| `.` | Output the current cell as an ASCII character |
| `,` | Accept one byte of input, overwriting the current cell |
| `[` | If the current cell is 0, jump to the matching `]` |
| `]` | If the current cell is not 0, jump back to the matching `[` |
| `Z` | Set the current cell to 0 |
| `^` / `^n` | Insert 1 / n new zero cells at the pointer |
| `X` / `Xn` | Delete the cell at the pointer, 1 / n times |
| `=` / `=n` | Insert 1 / n copies of the current cell right after it |
| `?` | Compare the current cell to the next one and insert the result (1 if equal, 0 if not) two cells to the right |

Any other character is ignored, so you can use whitespace and comments wherever. Digits only count as a modifier when they follow a command.

### Notes on the new commands

- `^` inserts at the pointer, so the cell the pointer was on (and the following cells) shift right by n. The pointer ends up on the new cell.
- `=` inserts the copy at index + 1 and doesn't move the pointer.
- `?` doesn't move the pointer either. The result is inserted at index + 2, so `?XX` leaves just the result in place of the two compared cells.
- After `X`, if the pointer is now past the end of the ring, it wraps to cell 0.

## Errors

- You can't use `X` on a ring with only one cell.
- You can't use `?` on a ring with only one cell (tf are you comparing to?).

## Differences from Brainfuck

- The tape is a ring instead of a line so moving never hits an end, and cells can be inserted or deleted anywhere in it.
- Number modifiers let you do `+72` instead of 72 plus signs lmao.
- Four extra ways to reshape memory (`^`, `X`, `=`, `?`) and a quick clear (`Z`).

## Why "Ouroboros"?

Because the memory eats its own tail :3
