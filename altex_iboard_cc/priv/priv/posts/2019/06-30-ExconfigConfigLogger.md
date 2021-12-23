%{ 
  title:  "Exconfig ConfigLogger",
  date: "Sun Jun 30 21:01:11 CEST 2019",
  tags: ["2019", "hex", "andi", "exconfig", "elixir"]
}
---
Today I implemented the module "ConfigLogger" for [Exconfig][].
_Exconfig_ is a configuration cache for [Elixir][] and can be used to read
environment vars during runtime.

```elixir
require Exconfig

value = Exconfig.get(:env, :conf_key, "Default Value")
```
`get/3` now is a macro and records it's usage to `configuration.log` during
compile time, in all environments but `:prod`.

In other environments than `:prod` the first usage of the macro starts
a GenServer (`Exconfig.ConfigLogger`) and adds every use of `get/3` to its state.

### Example
```elixir
  require Exconfig
  value = Exconfig.get(:env, :my_key, "My Value")
```
Will write the following line to `configuration.log`
```sh
MY_KEY="My Value"
```
### Do you know what might be configurable in your app?

I use `Exconfig.get(:env,...)` a lot and to be honest, I can't remember what is configurable. Neither I have the discipline to add every new key of my configuration to the documentation immediately. 

That's where `ConfigLogger` can help. After compiling the application, you can find `configuration.log` in your project directory. So, you have a template for a shell script, that can be edited and used to set up the environment before starting the app. Also, no single configuration can be overseen.


[Elixir]: https://elixirlang.org
[Exconfig]: https://github.com/iboard/exconfig
