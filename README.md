# Jormungandr

**Jormungandr (Jorm)** is an esoteric programming language based on Brainfuck, but memory is a resizable, cyclic tape.

You can try it out here: https://typhe.dev/jormungandr


## Overview

Memory is a ring that begins with one cell. Moving the pointer past either end wraps to the other. Incrementing a cell past 255 wraps to 0, and decrementing a cell past 0 wraps to 255 (modulo 256).

## Commands

| Command | Description |
| --- | --- |
| `>` | Move the pointer to the right |
| `>n` | Move the pointer to the right by n cells |
| `<` | Move the pointer to the left |
| `<n` | Move the pointer to the left by n cells |
| `+` | Increment the memory cell at the pointer |
| `+n` | Increment the memory cell at the pointer n times |
| `-` | Decrement the memory cell at the pointer |
| `-n` | Decrement the memory cell at the pointer n times |
| `.` | Output the character signified by the cell at the pointer |
| `,` | Input a character and store it in the cell at the pointer |
| `[` | Jump past the matching `]` if the cell at the pointer is 0 |
| `]` | Jump back to the matching `[` if the cell at the pointer is nonzero |
| `^` | Insert a new memory cell at the pointer |
| `^n` | Insert a new memory cell at the pointer n times |
| `=` | Duplicate the memory cell at the pointer |
| `=n` | Duplicate the memory cell at the pointer n times |
| `X` | Delete the memory cell at the pointer |
| `Xn` | Delete the memory cell at the pointer n times |
| `Z` | Set the memory cell at the pointer to 0 |
| `?` | Compare the cell at the pointer to the following cell and insert the result after both: 1 if they match, 0 if they do not. |

Using `X`, `Xn`, or `?` on a ring with only one cell is an error.

Insertions, deletions, duplications, and comparisons do not move the pointer.

Insertions, comparisons, and duplications shift the cells at and to the right of the insertion point to the right. Deletions shift the cells to the right of the deletion point to the left.

`ring:  [6, 8, 1, 7]      pointer at index 1 (the 8)
^  ->  [6, 0, 8, 1, 7]     pointer still at index 1, which is now 0
?  ->  [6, 0, 8, 0, 1, 7]    pointer still at index 1
X  ->  [6, 8, 0, 1, 7]         pointer still at index 1, which is 8 again
=2 ->  [6, 8, 8, 8, 0, 1, 7]     pointer still at index 1`

Commands also wrap at the edges, as if there were no edges at all.

If running `X` at the highest index, the pointer wraps to cell 0.

## Trivia
- Jormungandr was originally named [Ouroboros](https://esolangs.org/wiki/Ouroboros), but that name is taken, so it was renamed to the Norse equivalent.
- Jörmungandr is an incorrect spelling.  The correct letter is `o`, not `ö`.
