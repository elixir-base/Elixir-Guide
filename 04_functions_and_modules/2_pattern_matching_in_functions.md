# Pattern Matching in Functions

#### Order of functions are important as far, as last function accept all of values
```elixir
defmodule ComplexMath do
  def fact(0) do
    1
  end

  def fact(n) when is_integer(n) do
    n * fact(n - 1)
  end
end

iex(1)> ComplexMath.fact(0)
1

iex(2)> ComplexMath.fact(5)
120
```

## Guard Clauses
#### To frevent passing negative value to function factorial, uses condition of argument

```elixir
defmodule ComplexMath do
  def fact(0) do
    1
  end
  
  def fact(n) when is_integer(n) and n > 0 do
    n * fact(n - 1)
  end
end

iex(1)> ComplexMath.fact(0)
1
iex(2)> ComplexMath.fact(5)
120
iex(3)> ComplexMath.fact(-5)
** (FunctionClauseError) no function clause matching in ComplexMath.fact/1
```


## Pattern Matching with Guard Functions
```elixir
defmodule ThatMath do
  def process({:ok, result}) do
    result
  end

  def process({:error, _}) do
    :failure
  end

  def process(_) do
    :unknown
  end
end

iex(1)> ThatMath.process({:ok,"Ping"})          
"Ping"

iex(2)> ThatMath.process({:error, "some error"})
:failure

iex(3)> ThatMath.process({})                    
:unknown

```

## The Final Factorial Function with Guard

```elixir
defmodule ComplexMath do
  def fact(0) do
    1
  end

  def fact(n) when is_integer(n) and n > 0 do
    n * fact(n - 1)
  end

  def fact(_) do
   0
  end
end

iex(1)> ComplexMath.fact(0)
1
iex(2)> ComplexMath.fact(5)
120
iex(3)> ComplexMath.fact(-5)
0
iex(4)> ComplexMath.fact("1")
0
```