# Anonymous Functions

## Anonymous Function Long Notation
#### Anonymous Functions don't need any particular name

#### Long Notation
```elixir
fn (person) ->
  person.age > 18
end
```

#### Short Notation
```elixir
&(&1.age > 18)
```

## Function which validates that a persons age is above 18

#### Basic Validation Function with different condions
```elixir
person = %{name: "John", age: 30}
def validate(person) do
  person.age > 18
end

def validate_strict(person) do
  person.age > 18 and person.age < 60
end
```
We can change the validate function to receive the actual function to apply for the validation of the person.

The validation parameter is supposed to be an a anonymous function.

Calling anonymous function is simple - just place a dot in fronty of them and pass an argument lists.
```elixir
person = %{name: "John", age: 19}
defmodule Validation do
  def validate(person, validation) do
    validation.(person)
  end
end

iex(1)> Validation.validate(person, &(&1.age > 18))
true

iex(1)> Validation.validate(person, &(&1.age > 20 and &1.age < 60))
false
```

```elixir
defmodule Register do
  def person do
    %{name: "John", age: 30}
  end

  def person_age(person) do
    person.age
  end

  def validate(person_age) when is_integer(person_age) and person_age > 18 do
    "Your age valid"
  end
  
  def validate(_) do
    "Your age invalid"
  end
end

iex(1)> Register.person_age(Register.person)
30

iex(2)> Register.validate(Register.person)  
"Your age invalid"

iex(3)> Register.validate(Register.person_age(Register.person))
"Your age valid"

```

## The Enum Module
> each/2 | count/2 | map/2 | reduce/3 | sort/2 | filter/2

#### Take out all the odd numbers, multiply each number by itself and count the ones above 20
```elixir
list = [1,2,3,4,5,6,7,8,9,19]
defmodule BasicMath do
  def add(x,y), do: x + y
  def square(x) do
    x * x
  end
end

defmodule Complex do
  import Integer, only: [is_odd: 1]
  import BasicMath, only: [square: 1]
  
  def process(list) when is_list(list) do
    list
    |> Enum.reject(&(is_odd(&1)))
    |> Enum.map(&square/1)
    |> Enum.count(&(&1 > 20))
  end

  def process(_) do
    "Incorrect list were provided"
  end
end

iex(1)> Complex.process("")
"Incorrect list were provided"

iex(2)> Complex.process(list)
2
```
