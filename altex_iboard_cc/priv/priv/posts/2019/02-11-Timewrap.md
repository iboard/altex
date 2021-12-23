%{
  title: "Timewrap",
  date: "Mon Feb 11 10:10:59 CET 2019",
  tags: ["andi", "2019", "elixir", "hex", "project", "timewrap"],
  author: "Andi"
}
---
> ... my 3rd HEX package for Elixir

<img src="/assets/posts/2019/2019-02-11-Timewrap.gif" />
Timewrap is a "Time-Wrapper" through which you can access different
time-sources, Elixir and Erlang offers you. Other than that you 
can implement on your own.

Also, _Timewrap_ can do the time-warp, freeze, and unfreeze a 
`Timewrap.Timer`.

You can instantiate different `Timewrap.Timer`s, registered and
supervised by `:name`.

The `Timewrap.TimeSupervisor` is started with the `Timewrap.Application`
and implicitly starts the default timer `:default_timer`. This
one is used whenever you call Timewrap-functions without a 
timer given as the first argument.

### Resources

  * [Source on Github][]
  * [Hex-package][]
  * [My Hex Project(s)](https://github.com/users/iboard/projects/1)

### Examples:

    use Timewrap # imports some handy Timewrap-functions.

#### With default Timer

    Timewrap.freeze_timer()
    item1 = %{ time: current_time() }
    :timer.sleep(1000)
    item2 = %{ time: current_time() }
    assert item1.time == item2.time


#### Transactions with a given and frozen time

    with_frozen_timer(~N[1964-08-31 06:00:00Z], fn ->
      ... do something while `current_time` will 
      always return the given timestamp within this
      block...
    end )

#### Start several independent timers

    {:ok, today} = new_timer(:today)
    {:ok, next_week} = new_timer(:next_week)
    freeze_time(:today, ~N[2019-02-11 09:00:00])
    freeze_time(:next_week, ~N[2019-02-18 09:00:00])
    ... do something ...
    unfreeze_time(:today)
    unfreeze_time(:next_week)


## Installation

From [available Hex package](https://hex.pm/docs/publish), the package can be installed
by adding `timewrap` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:timewrap, "~> 0.1.0"}
  ]
end
```
  
### Configuration

  `config/config.exs`

      config :timewrap,
        timer: :default,
        unit: :second,
        calendar: Calendar.ISO,
        representation: :unix


[Elixir]: https://elixir-lang.org/
[Hex-package]: https://hex.pm/packages/timewrap
[Source on Github]: https://github.com/iboard/timewrap
[Hex-package]: https://hex.pm/packages/timewrap
[Raspberry Experiments]: {{ site.baseurl }}{% post_url 2018-08-26-NervesRpi3 %}


