%{
  title: "Elixir script the shell",
  date: "Wed Oct 17 09:38:19 CEST 2018",
  author: "Andi",
  tags: ["andi", "2018", "elixir", "dev", "shell"]
}
---
### I'm using Elixir as a scripting language for the shell

And it's that easy ...

Write a file, `hello.exs` for example.

```elixir
#!/usr/bin/env elixir
defmodule Greeter do
  def hello(name), do: IO.puts "Hello, #{name}!"
end

# Main
Greeter.hello( hd(System.argv() )
```

Don't forget to `chmod +x hello.exs` and then use the script from
the terminal with

    $ ./hello World
    Hello, World!

For more complex scenarios you can use [Elixir][]'s [OptionParser][] and all the sugar 
that comes with that beautiful language.

[Elixir]: https://elixir-lang.org
[OptionParser]: https://hexdocs.pm/elixir/OptionParser.html
