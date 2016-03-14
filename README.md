# cubix

A 2D esoteric language wrapped around the faces of a cube.

## Basics

More spec here soon.

## Commands

Unless specified otherwise, operators do not pop their operands from the stack.

\* designates not implemented yet.

### I/O

- `i` - input the next char.
- `I` - scan through the input until an integer (signed or unsigned) is found, and push that integer.
- `o` - output the current top-of-stack as a char code.
- `O` - output the current top-of-stack as a number.

### Arithmetic

- `(` - decrement the top item.
- `)` - increment the top item.
- `+` - add the top two items.
- `-` - subtract the top two items.
- `*` - multiply the top two items.
- `,` - integer divide the top two items, rounding toward negative infinity.
- `%` - take modulo of the top two items.
- `&` - take top item, and add the next item * 10.

### Literals

- `0-9` - push that digit.
- `'` - push the char code of the next char.
- `"` - starts/ends a string literal, performing `'` on each item until the next `"`.
- `N` - pushes a newline, or 10.
- `S` - pushes a space, or 32.
- `Q` - pushes a quote, or 34.

### Control flow

- `.` - no-op.
- `/` - flip the IP diagonally. `E -> N; N -> E; S -> W; W -> S` 
- `\` - flip the IP diagonally. `W -> N; N -> W; S -> E; E -> S` 
- `|` - flip the IP horizontally. `E -> W; W -> E`
- `_` - flip the IP vertically. `N -> S; S -> N`
- `>` - point the IP east.
- `v` - point the IP south.
- `<` - point the IP west.
- `^` - point the IP north.
- `W` - turn the IP left, then left again before executing the next instruction.
- `w` - turn the IP right, then right again before executing the next instruction.
- `?` - if the top item is less than zero, turn left; if it's more than zero, turn right; otherwise, continue straight.
- `@` - end the program.

More spec coming soon.

### Stack manipulation

- `:` - duplicate the top item.
- `;` - pop/discard the top item.
