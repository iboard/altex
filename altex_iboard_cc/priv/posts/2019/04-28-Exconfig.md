%{
  title: "Exconfig -- Configuration Cache For Elixir",
  author: "Andi",
  tags: ["2019", "dev", "obsolete", "andi", "elixir", "project", "exconfig", "hex"]
}
---
<p class="alert alert-danger">OBSOLETE! Today there are better ways to deal with your config.</p>

Today, I wrote my fourth HEX-package and published it on "hex.pm".

  * [Exconfig at hex.pm](https://hex.pm/packages/exconfig)
  * [Exconfig at Github](https://github.com/iboard/exconfig)

When deploying via Docker-images I had some issues because the docker-image
was compiled with System-ENVs which was used at compile-time and so was active
when using the image for other customers.

I used `System.get_env` to set a configuration in `config/prod.exs`.

To safe me from this error in the future, I decided to use my own package
to deal with configuration. Other than this, I want System-ENVs to overwrite
any other configuration in any case.

To achieve this, I repaced all calls to `System.get_env` and `Application.get_env`
with calls to `Exconfig.get`.

Because the `Exconfig.Cache`-server will not be running at compile-time, your
app will not compile if you use settings meant to be valid at runtime.

## Usage

```elixir

Exconfig.get(:myapp, :key, "default value")

```

The function tries to read the given key (`{:myapp, :key}`) from the Cache.
If it is not stored yet, it will try to read from `Application.get_env/2`,
followed by `System.get_env/2` and stores the value in the cache.

## Use it in your mix-project

add it to your dependencies in `mix.exs` and run `mix deps.get`.

```elixir
def deps do
  [
    {:exconfig, "~> 0.1.0"}
  ]
end
```
