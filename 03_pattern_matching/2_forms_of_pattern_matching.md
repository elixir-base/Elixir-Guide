# Forms of Pattern Matching

### Valid pattern matching
```elixir
iex(1)> [1,2,3] = [1,2,3]
[1, 2, 3]

iex(2)> [x,2,3] = [1,2,3]
[1, 2, 3]

```


## Con-cell
### Valid pattern matching
```elixir
iex(1)> [x|[2,3]] = [1,2,3]
[1, 2, 3]

iex(2)> [x|y] = [1,2,3]
[1, 2, 3]
```

### Also be used on Tuples
```elixir
iex(1)> {:ok, result} = {:ok, 10}
{:ok, 10}

iex(2)> {name, age} = {"John", 30}
{"John", 30}
```
### The Underscore matches anything and is an unreadable variable

```elixir
iex(1)> {name, _} = {"John", 30}
{"John", 30}
```


Matches as long as the key is present on the right side
```elixir
{name: name = {name: "John", age: 30}
```

### Binary like Tuples or Lists
Binary list
```elixir
<<1,2,3>>
```
1 - one byte

## Concatination
```elixir
iex(1)> <<1,2,3>> <> <<4>>
<<1, 2, 3, 4>>
```

### When fill-in an a binary, we can specify a size attribute for it's elements
> That value 1 a size of 16 bits, which means its 2 bytes long
```elixir
<<1::size(16)>>
```

### Strings ar also sequnences of bytes, as they are ecoded on UTF-8, and that represented by UTF-8 code points
```elixir
iex(1)> <<65, "broad">>
"Abroad"
```

## Specification for a binary format: FIF Fictitious Image Format
`M | w | h | s | IMAGE DATA`
- **M**: Magic Number (2 byte) 0xCAFE
- **w**: Width (2 byte)
- **h**: Height (2 byte)
- **s**: Size of the Pixel(1 byte)
- **IMAGE DATA**: Image Data(N bytes)

Binary Pattern
```elixir
<<
  0xCAFE::16,
  width:16,
  height: 16,
  pixel_size,
  image_data::binary
>> = <<...>>
```

### Extract data from image - deconstruct complex data structures, even binary
> 0xCAFE::16 - 16 bits