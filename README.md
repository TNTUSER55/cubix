# cubix

A 2D esoteric language wrapped around the faces of a cube. [Online interpreter](https://ethproductions.github.io/cubix), [Code design helper](https://jsfiddle.net/vihanb/w5p8p2ms/26/embedded/result/)

## Basics

The first thing the interpreter does is remove whitespace, then figure out the smallest cube that the code will fit onto. The code is then padded with no-ops until all six sides are filled. That means that this "Hello, World!" program:

    ./v.o;@?/"!dlroW"S',u/"Hello"

is exactly the same as this one:

          . / v
          . o ;
          @ ? /
    " ! d l r o W " S ' , u
    / " H e l l o " . . . .
    . . . . . . . . . . . .
          . . .
          . . .
          . . .

Then the code is run like a 2-dimensional language, except that the IP (instruction pointer) wraps around like the code is on a cube.

## Commands

Unless specified otherwise (with "pop" or "in place"), operators do not remove their operands from the stack.

\* designates not implemented yet.

### I/O

- `i` - input the next char code. If none are left, pushes -1.
- `I` - scan through the input until the first match of `/-?\d+/` is found, and push that integer. If none are left, pushes 0.
- `A` - input all remaining char codes. The first one will end up on top. EOF is marked as -1.
- `o` - output the current top-of-stack as a char code.
- `O` - output the current top-of-stack as a number.

### Arithmetic

- `(` - decrement the top item in place.
- `)` - increment the top item in place.
- `+` - add the top two items.
- `-` - subtract the top two items.
- `*` - multiply the top two items.
- `,` - integer divide the top two items, rounding toward negative infinity.
- `%` - take modulo of the top two items.
- `&` - pop two integers, concatenate their digits, and push the result as an int.
- `n` - negate the top item in place.
- `~` - take bitwise NOT of the top item in place.
- `a` - take bitwise AND of the top two items.
- `b` - take bitwise OR of the top two items.
- `c` - take bitwise XOR of the top two items.

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
- `T` - turn the IP around. `N -> S; S -> N; E -> W; W -> E`
- `>` - point the IP east.
- `v` - point the IP south.
- `<` - point the IP west.
- `^` - point the IP north.
- `L` - turn the IP left.
- `R` - turn the IP right.
- `U` - turn the IP left, then left again before executing the next instruction.
- `u` - turn the IP right, then right again before executing the next instruction.
- `W` - turn the IP left, then right before executing the next instruction.
- `w` - turn the IP right, then left before executing the next instruction.
- `$` - skip the next instruction.
- `!` - if the top item is truthy, skip the next instruction.
- `?` - if the top item is less than zero, turn left; if it's more than zero, turn right; otherwise, continue straight.
- `@` - end the program.

### Stack manipulation

- `:` - duplicate the top item.
- `;` - pop/discard the top item.
- `#` - push the stack length.
- `s` - swap the top two items. `[... 1 2] => [... 2 1]`
- `r` - rotate the top three items. `[... 0 1 2] => [... 2 0 1]`
- `q` - send the top item to the bottom.
- `t` - pop X, bring the Xth item to the top.
