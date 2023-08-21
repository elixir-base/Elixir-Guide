# Functions and Modules

### What is a Function?
In simple terms a function is a computational entity that has an optional name, receives a number of arguments and always outputs a return value.
> `f(x) -> y`

In most programming languages functions provide a way for us to reuse computations or commonly used  repeated code.

#### Only the last executed expression and the value will return.


```elixir

defmodule Greet do
  def say_hello() do
    :buy
    :hello
  end
end

iex(1)> Greet.say_hello()
:hello

```


## Default Arguments
#### Two backward slashes divide argument and default value of it
```elixir

defmodule Greet do
  def say_hello(name\\ "Stranger") do
    "Hello #{name}"
  end
end

iex(1)> Greet.say_hello()                    
"Hello Stranger"

```

## Chaining Function Calls
```elixir
defmodule Greet do
  def person do
    %{first_name: "John", last_name: "Doe"}
  end

  def full_name(person) do
      "#{person.first_name} #{person.last_name}"
  end

  def say_hello(name\\"Stranger", from\\ "Greeter") do
    "#{from} says: Hello #{name}"
  end
end

iex(1)> Greet.say_hello()
"Greeter says: Hello Stranger"

iex(2)> Greet.say_hello(Greet.full_name(Greet.person), "Bob")
"Bob says: Hello John Doe"
```

## Pipe Operator |>
#### Injects the value on the left as the first argument of the function on the right.
> `person |> full_name |> say_hello("Bob")`
```elixir
iex(1)> Greet.person |> Greet.full_name |> Greet.say_hello("Bob")
"Bob says: Hello John Doe"
```

## Modules
#### A group of closely related functions
> BasicMath
> - add/2
> - square/1
```elixir
defmodule BasicMath do
  def add(x,y), do: x + y

  def square(x) do
    x * x
  end
end

iex(1)> BasicMath.add(5, 8)  
13

iex(2)> BasicMath.square(5)
25
```


#### Composing Modules
```elixir
defmodule ComplexMath do
  alias BasicMath, as: Math

  def cube(x) do
    BasicMath.square(x) * x
  end
end

iex(1)> ComplexMath.cube(5)
125

```

#### Elixir support to import modules to other modules
```elixir
defmodule ComplexMath do
  import BasicMath
  
  def cube(x) do
    square(x) * x
  end
end

iex(1)> ComplexMath.cube(3)
27
```

#### Limit imported functions from module
```elixir
defmodule ComplexMath do
  import BasicMath, only: [square: 1]
  
  def cube(x) do
    square(x) * x
  end
end

iex(1)> ComplexMath.cube(12)
1728
```

**Alias**: Reference a module by a different name

**Import**: Include the functions of a module


## Private Functions
#### Private functions only visible by functions in the module
Def the private functions can only be used from within the module they were defined modules also allow the definition of constants.

```elixir
defmodule Greet do
  def hello, do: say_hello

  defp say_hello do
    :hello
  end
end

iex(1)> Greet.hello
:hello
```

## Constants
Constants are defined by the symbol before their name.
```elixir
defmodule Greet do
  @foo :hello

  def hello do
    @foo
  end
end

iex(1)> Greet.hello       
:hello
```