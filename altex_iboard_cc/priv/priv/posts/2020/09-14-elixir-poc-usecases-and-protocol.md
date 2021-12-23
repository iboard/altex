%{
  title:  "Elixir Protocol For Usecases",
  date: "Mon Sep 14 10:52:23 AM CEST 2020",
  tags: ["2020", "andi", "elixir"]
}
---
I love Elixir and the implementation of protocols. Here is an example of how you
can implement a protocol for a given data type/structure.

What this example shows:

- 1st: There is a protocol named `Usecase.` It declares all functions of the
  implementation of the protocol `Usecase` needs.

So, you can execute it like so:

Define a module for your use case

```elixir

defmodule DateUsecase do
  use Clean  # <= this implements all functions for a Usecase

  # The only function you have to define is `execute`
  def execute(nil), do: NaiveDateTime.utc_now()
  def execute(y: y, m: m, d: d), do: NaiveDateTime.new(y, m, d, 0, 0, 0)
end
```

Now you can use it like so

```elixir
%DateUsecase{}
|> Usecase.request(y: 1964, m: 08, d: 31)
|> Usecase.execute()
|> Usecase.entity()
# ~N[1964-08-31 00:00:00]
```

- 2nd: The 'magic' is stupid simple

It's all about the structure `%YourUsecase{}` which will be injected by the
line `use Clean` and is defined there as

```elixir
defstruct request: nil, errors: [], result: nil, halt: false, client: :system
```

`request` holds the parameter/arguments passed in _Usecase.request(.....)_.

`errors` is just a list where errors being added to during execution.

`result` holds whatever your `execute(...)` function returns. Usually, it is
an ok/error tuple like `{:ok, valid_result}` or `{:error, reason}`.

`halt` is either `false` or `true`. It will initialize with `false`, but any
step previous to `execute` can set it to `false.` Thus the execution function
will not be executed.

`client` defaults to `:system` but is supposed to hold the client-metadata for
which the use case should execute. In web apps, this may be the current user,
the remote_ip, the user-agent,...

By now, there is no `validate` function. But you simply can implement it and
call it just before `execute`. You can add this as homework ;-)

## Full Example

No need to compile this file. Just execute it with

    $ iex poc_usecases.exs

Repo [github.com/iboard/elixir-pocs](https://github.com/iboard/elixir-pocs)

File: `github.com/iboard/elixir-pocs/poc_usecases.exs`
```elixir
defprotocol Usecase do
  def request(usecase, opts \\ [])
  def execute(usecase)
  def args(usecase)
  def result(usecase)
  def errors(usecase)
  def state(usecase)
  def entity(usecase)
  def client(usecase)
end

defmodule Clean do
  defmacro __using__(_opts) do
    quote do
      defstruct request: nil, errors: [], result: nil, halt: false, client: :system

      defimpl Usecase, for: __MODULE__ do
        def request(usecase, ... = opts \\ []) do
          %{usecase | request: opts}
        end

        def execute(args) do
          if !args.halt do
            case args.__struct__.execute(args.request) do
              {:ok, _} = r -> %{args | result: r}
              {:error, error} = e -> %{args | result: e, errors: args.errors ++ [error]}
              result -> %{args | result: result}
            end
          else
            args
          end
        end

        def result(usecase), do: usecase.result
        def client(usecase), do: usecase.client
        def errors(usecase), do: usecase.errors
        def args(usecase), do: usecase.request

        def state(usecase) do
          case usecase.result do
            {:ok, _} -> :ok
            {:error, _} -> :error
            x -> x
          end
        end

        def entity(usecase) do
          case Usecase.state(usecase) do
            :ok -> usecase.result |> elem(1)
            :error -> nil
            x -> x
          end
        end
      end
    end
  end
end

defmodule DateUsecase do
  use Clean
  def execute(nil), do: NaiveDateTime.utc_now()
  def execute(y: y, m: m, d: d), do: NaiveDateTime.new(y, m, d, 0, 0, 0)
end

defmodule FizzbarUsecase do
  use Clean
  def execute(_params), do: "Fizzefazze!"
end

defmodule MyApp do
  def run() do
    ## Usecase without params, no request() neccessary
    %DateUsecase{}
    |> Usecase.execute()
    |> IO.inspect(label: "result")

    IO.puts("")

    ## Same usecase but with input parameters
    uc =
      %DateUsecase{}
      |> Usecase.request(y: 1964, m: 08, d: 31)
      |> Usecase.execute()

    uc
    |> Usecase.args()
    |> IO.inspect(label: "args")

    uc
    |> Usecase.client()
    |> IO.inspect(label: "client")

    uc
    |> Usecase.result()
    |> IO.inspect(label: "result")

    uc
    |> Usecase.errors()
    |> IO.inspect(label: "errors")

    uc
    |> Usecase.state()
    |> IO.inspect(label: "state")

    uc
    |> Usecase.entity()
    |> IO.inspect(label: "entity")

    IO.puts("")

    ## Same usecase but with invalid input
    uc =
      %DateUsecase{}
      |> Usecase.request(y: 1964, m: 2, d: 30)
      |> Usecase.execute()

    uc
    |> Usecase.args()
    |> IO.inspect(label: "args")

    uc
    |> Usecase.result()
    |> IO.inspect(label: "result")

    uc
    |> Usecase.errors()
    |> IO.inspect(label: "errors")

    uc
    |> Usecase.state()
    |> IO.inspect(label: "state")

    uc
    |> Usecase.entity()
    |> IO.inspect(label: "entity")

    IO.puts("")

    %FizzbarUsecase{}
    |> Usecase.execute()
    |> Usecase.result()
    |> IO.inspect(label: "result")

    IO.puts("")

    %DateUsecase{}
    |> Usecase.execute()
    |> Usecase.entity()
    |> IO.inspect(label: "Today is")
  end
end

MyApp.run()
```

Output

```elixir
result: %DateUsecase{
  client: :system,
  errors: [],
  halt: false,
  request: nil,
  result: ~N[2020-09-14 09:54:03.409234]
}

args: [y: 1964, m: 8, d: 31]
client: :system
result: {:ok, ~N[1964-08-31 00:00:00]}
errors: []
state: :ok
entity: ~N[1964-08-31 00:00:00]

args: [y: 1964, m: 2, d: 30]
result: {:error, :invalid_date}
errors: [:invalid_date]
state: :error
entity: nil

result: "Fizzefazze!"

Today is: ~N[2020-09-14 09:54:03.422391]
```

