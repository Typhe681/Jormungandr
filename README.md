# Jormungandr

**Jormungandr (Jorm)** is an esoteric programming language based on Brainfuck, but memory is a resizable, cyclic tape.

The main premise of Jorm is that memory is not a fixed linear structure. Commands like <code>^</code>, <code>X</code>, <code>=</code>, and <code>?</code> modify the tape by inserting or deleting cells.

Moving the pointer in either direction eventually returns it to the same cells, forming a continuous ring. The ring starts with one cell. Incrementing a cell past 255 wraps to 0, and decrementing a cell past 0 wraps to 255 (modulo 256).

Most commands are inherited from Brainfuck (<code>&gt;&lt;+-.,[]</code>), but there are a few that are unique to Jormungandr. Many commands also support numerical suffixes that act as repeat modifiers.

You can try it out here: https://typhe.dev/jormungandr

## Commands

| Command | Description |
| --- | --- |
| `>` | Move the pointer to the right |
| `>n` | Move the pointer to the right by n cells |
| `<` | Move the pointer to the left |
| `<n` | Move the pointer to the left by n cells |
| `+` | Increment the cell at the pointer |
| `+n` | Increment the cell at the pointer n times |
| `-` | Decrement the cell at the pointer |
| `-n` | Decrement the cell at the pointer n times |
| `.` | Output the character signified by the cell at the pointer |
| `,` | Input a character and store it in the cell at the pointer |
| `[` | Jump past the matching `]` if the cell at the pointer is 0 |
| `]` | Jump back to the matching `[` if the cell at the pointer is nonzero |
| `^` | Insert a new cell, initially containing 0, between the cell at the pointer and the previous cell, then move the pointer to that new cell |
| `^n` | Insert n new cells, initially containing 0, between the cell at the pointer and the previous cell, then move the pointer to the first new cell |
| `=` | Insert a new cell, containing the same value as the cell at the pointer, between the cell at the pointer and the previous cell, then move the pointer to that new cell |
| `=n` | Insert n new cells, each containing the same value as the cell at the pointer, between the cell at the pointer and the previous cell, then move the pointer to the first new cell |
| `X` | Delete the cell at the pointer, then move the pointer to the cell to the right of the deleted cell |
| `Xn` | Delete n cells starting at the pointer, then move the pointer to the cell to the right of the deleted cells |
| `Z` | Set the cell at the pointer to 0 |
| `?` | Compare the cell at the pointer to the following cell and insert the result between the cell at the pointer and the previous cell, then move the pointer to the new cell. The result is 1 if they match and 0 if they do not |

Commands do not move the pointer around the ring unless explicitly stated.

Here is an example of various commands:

`
ring:  [6, 8, 1, 7]       pointer at 8
^  ->  [6, 0, 8, 1, 7]     pointer at 0
+3 ->  [6, 3, 8, 1, 7]      pointer at 3
?  ->  [6, 0, 3, 8, 1, 7]    pointer at 0
X  ->  [6, 3, 8, 1, 7]        pointer at 3
=2 ->  [6, 3, 3, 3, 8, 1, 7]   pointer at the first 3
<4 ->  [6, 3, 3, 3, 8, 1, 7]    pointer at 8
`

Using `X`, `Xn`, or `?` on a ring with only one cell is an error. Unmatched `[` and `]` commands are also errors.

## Trivia
- Jormungandr was originally named [Ouroboros](https://esolangs.org/wiki/Ouroboros), but that name is taken, so it was renamed to the Norse equivalent.
- Jörmungandr is an incorrect spelling.  The correct letter is `o`, not `ö`.
