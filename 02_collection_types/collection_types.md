# Collection Types

## Lists
Lists are ordered sequensetional collection types.

Define List - []
```elixir
[:hello, "hey", 4]
```
Head and Tail `["Head", :tail, "tail"]`
```elixir
iex(1)> a = ["Head", :tail, 4]
["Head", :tail, 4]

iex(2)> hd(a)
"Head"

iex(3)> tl(a)
[:tail, 4]

iex(4)> hd([])
** (ArgumentError) errors were found at the given arguments:
  * 1st argument: not a nonempty list :erlang.hd([])

```


## Lists - Cons Cell
```elixir
iex(1)> [:hello|[]]
[:hello]
```
`:hello -> ["hey"] -> [4,[]]`
```elixir
iex(1)> [:hello|["hey"|[4|[]]]]
[:hello, "hey", 4]
```

## Lists - Operations
Concatinations `++`

Substruction `--`
```elixir
iex(1)> [:hello, "hey", 4] ++ [0.5]
[:hello, "hey", 4, 0.5]

iex(2)> [:hello, "hey", 4] -- ["hey"]
[:hello, 4]
```


## Tuples
`{:hello, "hey",4}`


## Tuple Functions
Index - elem/2

Size - tuple_size/1

Replacement - put_elem/3
```elixir
iex(1)>tuple = {:hello, "hey", 4}
{:hello, "hey", 4}

iex(2)> elem(tuple, 1)
"hey"
```

## Lists vs Tuples
|                | List            | Tuple |
|:---------------|-----------------|--------|
|Structure       | Linked list     | Contiguous memory |
|Insertion       | Fast(prepending)| Expensive         |
|Size            | Slow            | Fast              |
|Fetch by index  | Slow            | Fast              |
|Fetch first     | Fast            | Fast              |


## Keyword Lists
A list of tuples with 2 elements, the first being an atom
```elixir
iex(1)> [{:red,2},{:green,4},{:blue,3}] = [red: 2, green: 4, blue: 3]
[red: 2, green: 4, blue: 3]

```


## Keyword Lists - Indexing
```elixir
iex(1)> list = [red: 2, green: 4, blue: 3]
[red: 2, green: 4, blue: 3]

iex(2)> list[:red]
2

iex(3)> list[:yellow]
nil
```
Still lists: Indexing slow, Ordered


## Maps
A unordered collection of values indexed by keys
```elixir
iex(1)> %{:red=>2, :green=>4}
%{green: 4, red: 2}
```
If keys are atoms, short notation can be use
```elixir
iex(1)> %{red: 2, green: 4}
%{green: 4, red: 2}
```
* `map[key]` - Works with any type of key
* `map.key` - Works only on keys that are atoms

```elixir
iex(1)> map = %{:x => 1, "y" => 2}
%{:x => 1, "y" => 2}

iex(2)> map.x
1

iex(3)> map["y"]
2

iex(4)> map."y"
** (KeyError) key :y not found in: %{:x => 1, "y" => 2}

```

* `%{map|key=>value}` - Works with any type of key
* `%{map|key: value}` - Works only on keys that are atoms


## Imutability
Collections are Imutable

Any modification on collection returns a new collection
```elixir
iex(1)> %{map|x: 4}
%{:x => 4, "y" => 2}

iex(2)> map.x
1
```


## Composition
```elixir
%{
    "John" => [
        %{red: 2, green: 4}
    ],
    "Mary" => [
        %{red: 2, green: 4}, %{yellow: 5}, %{red: 7, blue: 2}
    ],
    "Jeff" => [
        %{violet: 7, blue: 2}
    ],
    "Paul" => [
        %{red: 4, blue: 3, yellow: 7}, %{blue: 5, cyan: 3}
    ]
}
```


## Conclusion
Literal types in Elixir
- Numbers
- Strings
- Atoms

Collection types in Elixir
- Lists  (Ruby: Array)
- Tuples (Ruby: Key:Value Array)
- Maps   (Ruby: Hash)
