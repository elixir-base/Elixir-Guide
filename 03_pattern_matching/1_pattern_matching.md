# Pattern Matching versus Assignment

Valid expressions
```elixir
x = 1
1 = x
1 = 1
x = y
```
#### Left Hand Side: x
#### Match operator: =
#### Right Hand Side: y
```elixir
iex(1)> x = [1,2,3,4,5]
[1, 2, 3, 4, 5]
iex(2)> x = [1,2,3,4,5] = x
[1, 2, 3, 4, 5]
iex(3)> x = 3
3
iex(4)>x
3
iex(5)> [1,2,3,4,5] = x
** (MatchError) no match of right hand side value: 3
```

#
### If we dont want to be re-assigned variable - we have to us Pin operator: ^x = y

Strict check for a match, no binding of variables
```elixir
iex(1)> x = "hello"
"hello"
iex(2)> x = "hey"
"hey"
iex(3)> ^x = "oi"
** (MatchError) no match of right hand side value: "oi"
iex(4)> ^x = "hey"
"hey"
```