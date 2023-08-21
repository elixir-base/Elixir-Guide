# Exceptions Handling
### Handle Any Exceptions - Rescue
> Exception handling like this should be used only as last resort and NEVER for control flow
```elixir
defmodule Greeter do
  def yell_at(name) do
    try do
      "Hey #{String.upcase(name)}!!!"
    rescue
      e -> "Hey Stranger!"
    end
  end
end

iex()> Greeter.yell_at("John")
"Hey JOHN!!!"
```

## Raising Exceptions
```elixir
raise "A weird error happened!"
RuntimeError
```
> If you don't want to use RuntimeError, you can define your own Exception Type

```elixir
defmodule MyError do
  defexception message: "Strange error",
                number: 33
end

iex(6)> raise MyError, number: 33
** (MyError) Strange error
```

## Rescuing from Custom Exceptions
```elixir
defmodule MyError do
  defexception message: "Strange error",
                number: 33
end

defmodule Greeter do
  def catch_me() do
    try do
      raise MyError, number: 9023
    rescue
      e in MyError -> e.number
    end
  end
end

iex(1)> Greeter.catch_me
9023
```

> `After` executes after the rescue, useful for tearing down resources
```elixir
defmodule MyError do
  defexception message: "Strange error",
               number: 33
end

defmodule Greeter do
  def catch_me() do
    try do
      raise MyError, number: 9023
    rescue
      e in MyError -> e.number
    after
      IO.puts("I failed here")
    end
  end
end

iex(1)> Greeter.catch_me
9023
```


## Throwing and Catching
> `throw/catch` is far more suited for this purpose
```elixir
defmodule Greeter do
  def catch_me() do
    try do
      throw %{number: 9023}
    catch
      e -> e.number
    end
  end
end

iex(1)> Greeter.catch_me
9023
```
#
#### We should use `raise/rescue` for exceptions cases only. And `throw/catch` for when we want to brake from the flow of execution with the different outcome.