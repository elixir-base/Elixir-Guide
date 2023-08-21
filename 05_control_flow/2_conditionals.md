# Conditionals
> Multiple Paths = Pattern Matching
#### Classifying a list according to it's size
In this example we did find a group of three functions that classify a list according to its morphology.
```elixir
def classify([]), do: :empty
def classify([_]), do: :single
def classify([_|_]), do: :multi
```

## Age Discounts
In this example for a ticket office we apply a different discount to a ticket value according to the age range of the ticket holder for a child classified with an age of 12.

|               | Child | Normal      | Senior |
|:--------------|-------|-------------|--------|
|Age range      | < 12  | >= 12, < 65 | >= 65  |
|Discount       | 60%   | 0%          | 40%    |

We can express multiple outcomes for a computation using the current expression current evaluates the list of supplied expressions and executes the corresponding body, when the expression evaluates to true.


> When an expression evaluates to true, the body is executed

It only does this for the first expression that is true though so there is no falling through to other expressions.

#### Cond expression
```elixir
cond do
  expression -> body
  expression -> body
  ...
end
```


```elixir
def discount(age) do
  cond do
    age < 12  -> 0.6
    age >= 64 -> 0.4
    true      -> 0.0
  end
end
```
```elixir
defmodule Age do
  def categorize(age\\21) do
    cond do
      age < 12                -> :child
      age > 12 and age < 20   -> :teen
      age >= 64 and age < 110 -> :senior
      age >= 110              -> :corpse
      true                    -> :normal
    end
  end
end

iex(1)> Age.categorize(11) 
:child

iex(2)> Age.categorize(13)
:teen

iex(3)> Age.categorize(21)
:normal

iex(4)> Age.categorize(65)
:senior

iex(5)> Age.categorize(110)
:corpse
```

```elixir
defmodule Sale do
  def categorize(age\\21) do
    cond do
      age < 12                -> :child
      age > 12 and age < 20   -> :teen
      age >= 64 and age < 110 -> :senior
      age >= 110              -> :too_old
      true                    -> :normal
    end
  end

  def discount(category) do
    cond do
      category == :child  -> 0.6
      category == :senior -> 0.4
      true                -> 0.0
    end
  end
end

iex(1)> age = 11
11

iex(2)> age |> Sale.categorize
:child

iex(3)> age |> Sale.categorize |> Sale.discount
0.6
```


#### Case
> When a pattern matches the value of the expression, the body is executed
```elixir
case expression do
  pattern -> body
  pattern -> body
  ...
end
```
Just like with `Cond` - only the fist successful match is taking

```elixir

age = 11
defmodule Sale do
  def categorize(age\\11) do
    cond do
      age < 12                -> :child
      age > 12 and age < 20   -> :teen
      age >= 64 and age < 110 -> :senior
      age >= 110              -> :too_old
      true                    -> :normal
    end
  end

  def discount(category) do
    case category do
      :child  -> 0.6
      :teen   -> 0.5
      :senior -> 0.4
      _       -> 0.0
    end
  end
end

iex()> age |> Sale.categorize |> Sale.discount
0.6

```

#### If / Else
> When an expression evaluates to true, the body if_body is executed, otherwise the else_body is executed (if present)

```elixir
defmodule Sale do
  if expression do
    if_body
  else
    else_body
  end
end
```
> When an expression evaluates to false, the unless_body is executed

```elixir
unless expression do
  unless_body
end
```
#### Changed requirenments
```elixir
def show_price(name, price) do
  disount = name
  |> Customer.find
  |> Customer.categorize
  |> Pricing.discount

  price * (1.0 - discount)
end
```

#### Bad approach, mess, difficult to read
```elixir
def show_price(name, price) do
  case Customer.find(name) do
    {:ok, person} ->
      case Customer.categorize(person) do
        {:ok, category} ->
          case Pricing.discount(category) do
            {:ok, discount} ->
              {:ok, price * (1.0 - discount)}
            error -> error
          end
        error -> error
      end
    error -> error
  end
end
```


#### With
> If all patterns match, body is executed

> When a expression doesn't match, its value is returned

```elixir
with 
  pattern <- expression
  pattern <- expression
  ...
do
  body
end
```
> Good approach. Much cleaner
```elixir
def show_price(name, price) do
  with
    {:ok, person}   <- Customer.find(name),
    {:ok, category} <- Customer.categorize(person),
    {:ok, discount} <- Pricing.discount(category)
  do
    {:ok, price * (1.0 - discount)}
  end
end
```