# Standart IO
#### Input/Output

If no device is specified that device is assumed to be the standard IO instead of dealing with raw binary data there are two friendlier versions of these functions we can use in our program that deal specifically with string data.
> read/2 write/2

Gets reads a full string from the keyboard until the user presses a termination key like enter and puts which writes a full string with a newline character to the terminal screen.
> gets/2 puts/2
>
The EIEIO that gets function to write a string to the screen and wait indefinitely for the user inputs.
```elixir
iex(1)> IO.gets("What is your name?: ")
What is your name?: John
"John\n"

iex(2)> IO.puts("Hello!")
Hello!
:ok

```
#
## ANSI Formatting

Having written it into the terminal if we want to do some fancy formatting on our outputs, elixir provides DJO that ANSI module. This module contains some functions that outputs special and C characters.
These characters are interpreted by some terminals to change the aspect of text, such as its color size and formats.
### IO.ANSI

||||
| :-----: | :------: | :------: |
| red/0   | white/0  | blue/0   |
| bold/0  | italic/0 | format/0 |

```elixir
iex(3)> IO.puts([IO.ANSI.red, "Eli", IO.ANSI.blue, "xir"])
$${\color{red}Eli\color{blue}xir}$$
:ok

iex(5)> IO.ANSI.format([:red, "Eli", :blue, "xir"]) |> IO.puts
$${\color{red}Eli\color{blue}xir}$$
:ok

```