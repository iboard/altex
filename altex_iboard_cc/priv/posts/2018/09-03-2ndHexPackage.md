%{ 
  title: "Datasource, my 2nd Hex-Package",
  date: "Mon Sep  3 11:55:22 CEST 2018",
  tags: ["andi", "2018", "elixir", "hex", "project", "datasource"]
}
---
After publishing [Bucketier]({{ site.baseurl }}{% post_url 2018-07-21-Bucketier %}),
a simple KV store for [Elixir][] as a [Hex-package][] about a month ago, today
let me announce [Datasource][].

  * [Source on Github][]
  * [Hex-package][]

_Datasource_ is a side project used in my [Raspberry Experiments][] and as
a handler of client-activities in my work-project.

## A continues stream of data from any source

The `Datasource` is a straightforward module providing one
function `next()` which returns the next value from a given source.

Sources can be from simple "endless counters" to "clocks,"
"files," but also sensors and triggers in a [Nerves]-project.

Datasource also provides a module `Datasource.DataStage` which
can be used as [GenStage producer][], reading data from a `Datasource` on demand.

```elixir
# Rememnber consumed events in state
defmodule ConsumerSpy do
  use GenStage

  def start_link(), do: GenStage.start_link(ConsumerSpy, [])
  def init(state), do: {:consumer, state}

  def handle_events(events, _from, state) do
    # Simulate load
    Process.sleep(10)
    {:noreply, [], [events | state]}
  end

  def handle_call(:get, _from, state) do
    {:reply, Enum.flat_map(state, & &1), [], state}
  end
end

{:ok, datasource} = Datasource.start_link( 0, fn(state) -> { state, state + 1 } end)
{:ok, producer} = Datasource.DataStage.start_link(datasource)
{:ok, consumer} = ConsumerSpy.start_link()

GenStage.sync_subscribe(consumer, to: producer, max_demand: 1)
Process.sleep(100)

ConsumerSpy.call(consumer, :get)
# => [0,1,2,3,...10]
```


[Elixir]: https://elixir-lang.org/
[Hex-package]: https://hex.pm/packages/bucketier
[Datasource]: https://hex.pm/packages/data_source
[Nerves]: https://nerves-project.org/
[GenStage producer]: https://github.com/elixir-lang/gen_stage
[Source on Github]: https://github.com/iboard/data_source
[Hex-package]: https://hex.pm/packages/data_source
[Raspberry Experiments]: /posts/2018/08-26-NervesRpi3

