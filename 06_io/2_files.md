# Files

#### The File Module
The File module this module contains functions to open files.
We can write to them and manipulate directories.
> Most of these functions are the same as the commands we'd use on a *NIX command line

| File |||
| :------ | :-------- | :------ |
| open/2  | read/1    | write/3 |
| cd/1    | ls/0      | mkdir/1 |
| cp/3    | exists?/1 | touch/2 |


## Creating a Directory
```elixir
File.mkdir("notes/today")

File.write("notes/today/one.txt", "Hello")

File.read("notes/today/one.txt")
{:ok, "Hello"}

File.rm("notes/today/one.txt")
```


## Open / Close
> Use this principle when doing a lot of IO operations on a file

```elixir
defmodule Notes do
  def write_list(path, list) do
    with {:ok, file} <- File.open(path, [:write, :utf8]) do
    list
    |> Enum.each(fn(line) -> IO.write(file, line) end)

    File.close(file)
  end
end
```