# Basic Types and Operators

## Integer Basics  
|Base / Hex       | Example       | Decimal|
|:----------------|:--------------|:-------|
|Hexadecimal(16)  | `0xFE`        | 254    |
|Hexadecimal(16)  | `0x1FB`       | 507    |
|Hexadecimal(16)  | `0xE`         | 14     |
|Octal            |               |        |
|Octal(8)         | `0o376`       | 254    |
|Octal(8)         | `0o773`       | 507    |
|Octal(8)         | `0o16`        | 14     |
|Binary           |               |        |
|Binary(2)        | `0b11111110`  | 254    |
|Binary(2)        | `0b111111011` | 507    |
|Binary(2)        | `0b1110`      | 14     |


## Binary list
```elixir
iex(1)> <<1,2,3>>
<<1, 2, 3>>
```

## Integer - Separator `_`
It do not change integer itself, but increase readability.
```elixir
iex(1)> 43312209
43312209

iex(2)> 43_312_209
43312209
```

## Operators          
|Base           |    | Example  | Decimal |
|:--------------|----|----------|---------|
|Addition       | +  | 1.55 + 9 | 10.5    |
|Subtraction    | -  | 1 - 2    | -1      |
|Multiplication | *  | 9 * 8    | 72      |
|Division       | /  | 10 / 4   | 2.5     |


## Integer Division Functions
|Base            |        | Example   | Decimal |
|:---------------|--------|-----------|---------|
Division         |( div ) | div(9, 7) | 1       |
Modulo/Remainder |( rem ) | rem(9, 7) | 2       |


## Booleans
**True**: everything is not nil is truthy

**False**: nil is falsey

* **Strict** operators: `and`, `or`, `not`

* **Non-strict** operators: `&&`, `||`, `!`
```elixir
iex(1)>true and false
false

iex(2)>true && false
false

iex(3)>3 and true
** (BadBooleanError) expected a boolean on left-side of "and", got: 3

iex(4)>3 && true
true
```

## Booleans - Comparsion Operators
Thise operators always yild boolean outputs - true or false

`>` , `<`, `>=`, `<=`, `!=`, `!==`, `==`, `===`

Not just for numbers

> Multiple types can be compared with one another by this order 
```elixir
number < atom < reference < function < port < pid < tuple < map < list < bitstring
```


## Strings
**String** always in double quotes -> "Hello, world!"

New line special character. -> `\n`

"Hello, \nWorld!"

```bash
iex> IO.puts("Hello\nWorld")
Hello
World
:ok
```
Interpolating expressions into String
```elixir
iex(1)age = 15 * 2
30

iex(2)"I am #{age} years old."
I am 30 years old
```
```elixir
iex(1)String.replace("Hello, World!", "World", "You")
"Hello, You!"
```


## Atoms
The defenition of :atom is a constant whose name is its value
```elixir
iex(1) :hello
:hello

iex(2) :Hey_you
:Hey_you

iex(2) :">_<"
:">_<"
```
In case to use special characters, or starts from the number - we have to use doble-quotes ""

Invalid atom
```elixir
iex(1):4_seasons
** (SyntaxError) iex:4:1: unexpected token ":" (column 1, code pont U+003A)
```

Valid atom
```elixir
iex(1):"4_seasons"
:"4_seasons"
```
