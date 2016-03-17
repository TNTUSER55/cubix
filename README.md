# cubix

A 2D esoteric language wrapped around the faces of a cube. [Temporary online interpreter](https://jsfiddle.net/vvc4dgvq/10/), [Code design helper](https://jsfiddle.net/vihanb/w5p8p2ms/26/embedded/result/)

## Basics

More spec here soon.

## Commands

Unless specified otherwise, operators do not pop their operands from the stack.

\* designates not implemented yet.

### I/O

- `i` - input the next char.
- `I` - scan through the input until an integer (signed or unsigned) is found, and push that integer.
- `A` - input all remaining char codes. The first one will end up on top.
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
- `&` - pop two integers, concatenate their digits, and push the result as an int.

### Literals

- `0-9` - push that digit.
- `'` - push the char code of the next char.
- `"` - start/end a string literal, performing `'` on each item until the next `"`.
- `N` - push a newline, or 10.
- `S` - push a space, or 32.
- `Q` - push a quote, or 34.

### Control flow

- `.` - no-op.
- `/` - flip the IP diagonally. `E -> N; N -> E; S -> W; W -> S` 
- `\` - flip the IP diagonally. `W -> N; N -> W; S -> E; E -> S` 
- `|` - flip the IP horizontally. `E -> W; W -> E`
- `_` - flip the IP vertically. `N -> S; S -> N`
- `T`* - turn the IP around. `N -> S; S -> N; E -> W; W -> E`
- `>` - point the IP east.
- `v` - point the IP south.
- `<` - point the IP west.
- `^` - point the IP north.
- `L`* - turn the IP left.
- `R`* - turn the IP right.
- `U` - turn the IP left, then left again before executing the next instruction.
- `u` - turn the IP right, then right again before executing the next instruction.
- `W` - turn the IP left, then right before executing the next instruction.
- `w` - turn the IP right, then left before executing the next instruction.
- `$` - skip the next instruction.
- `!` - if the top item is truthy, skip the next instruction.
- `?` - if the top item is less than zero, turn left; if it's more than zero, turn right; otherwise, continue straight.
- `@` - end the program.

More spec coming soon.

### Stack manipulation

- `:` - duplicate the top item.
- `;` - pop/discard the top item.
- `#` - push the stack length.
- `s`* - swap the top two items. `[... 1 2] => [... 2 1]`
- `r`* - rotate the top three items. `[... 0 1 2] => [... 2 0 1]`
- `q`* - send the top item to the bottom.
- `t`* - pop X, bring the Xth item to the top.
