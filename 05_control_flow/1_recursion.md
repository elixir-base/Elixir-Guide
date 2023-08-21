# Recursion
`Recursion - It's a method of dividing complex problems into smaller ones which are more easily managed.`

This Function defenition calls itself repeatedly in order to computeds return value. It only stops when retreat is 0, in wich case it returns the value 1. This kind of arangement constitutes a recursive call. 


```elixir
def fact(0) do
  1
end

def fact(n) do
  n * fact(n - 1)
end
```

## Count nodes
#### Base case
- Nodes with no childrens yild count 1
```elixir
def count(%{children: []}) do
  1
end
```

#### General function
- Count the nodes of the first child and add them to the 
count of the nodes of the rest of the children

```elixir
def count(%{children: children}) do
  [first|rest] = children
  count(first) + count(%{children: rest})
end
```

#### Module
```elixir
graph = %{
  children: [
    %{children: []},
    %{children: []},
    %{children: [
      %{children: []},
      %{children: []}
    ]},
    %{children: []}
  ]
}
```
```elixir
defmodule Graph do
  def count(%{children: []}), do: 1
  
  def count(%{children: children}) do
    [first|rest] = children
    count(first) + count(%{children: rest})
  end
end

iex()> graph |> Graph.count()
7
```

