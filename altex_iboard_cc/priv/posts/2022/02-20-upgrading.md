%{
title: "Upgrade Elixir, NimblePublisher, and Earmark",
author: "Andi",
tags: ~w/2022 elixir/
}

---

Recently I bumped the version of Elixir for this project to 1.13.2 and faced some issues
with dependencies between [Earmark][1] and [NimblePublisher][2].

Quick answer first, I found no solution by now but a workaround.

### The Problem

By just updating my dependencies in `mix.exs` as intuitively assumed

```elixir
{:earmark, "~> 1.4"},
{:nimble_publisher, "~> 0.1"},
{:makeup_elixir, ">= 0.0.0"},
{:makeup_erlang, ">= 0.0.0"},
```

... didn't work and I got this compile error

```elixir
== Compilation error in file lib/web_client_web/controllers/blog_controller.ex ==
** (FunctionClauseError) no function clause matching in MapSet.union/2

    The following arguments were given to MapSet.union/2:

        # 1
        []

        # 2
        []

    Attempted function clauses (showing 2 out of 2):

        def union(%MapSet{map: map1, version: version} = map_set, %MapSet{map: map2, version: version})
        def union(%MapSet{map: map1}, %MapSet{map: map2})

    (elixir 1.13.2) lib/map_set.ex:372: MapSet.union/2
    (earmark_parser 1.4.19) lib/earmark_parser/context.ex:64: EarmarkParser.Context._merge_messages/2
    (earmark_parser 1.4.19) lib/earmark_parser/context.ex:55: EarmarkParser.Context._merge_contexts/2
    (earmark_parser 1.4.19) lib/earmark_parser/context.ex:36: EarmarkParser.Context.prepend/3
    (earmark_parser 1.4.19) lib/earmark_parser/ast_renderer.ex:24: EarmarkParser.AstRenderer._render/3
    (earmark_parser 1.4.19) lib/earmark_parser.ex:494: EarmarkParser.as_ast/2
    (earmark 1.4.19) lib/earmark/internal.ex:42: Earmark.Internal.as_html/2
    (earmark 1.4.19) lib/earmark/internal.ex:48: Earmark.Internal.as_html!/2
    (nimble_publisher 0.1.2) lib/nimble_publisher.ex:110: NimblePublisher.convert_body/3
    (nimble_publisher 0.1.2) lib/nimble_publisher.ex:48: anonymous fn/5 in NimblePublisher.__extract__/2
    (elixir 1.13.2) lib/enum.ex:2396: Enum."-reduce/3-lists^foldl/2-0-"/3
    (nimble_publisher 0.1.2) lib/nimble_publisher.ex:41: NimblePublisher.__extract__/2
    lib/web_client_web/controllers/blog_controller.ex:14: (module)
    (elixir 1.13.2) lib/kernel/parallel_compiler.ex:346: anonymous fn/5 in Kernel.ParallelCompiler.spawn_workers/7
```

I tried various version combinations of `earmark` and `nimble_publisher`, and even tried to clone everything
to my disc and depend them as `... path: "../earmark"` and so on. I was eager to fix this an do a pull request
on success.

But, everything worked just fine "locally".

So, my quick solution for now is, referencing the master/main from Github directly. Aside from some
warnings this mix dependencies are working fine for me.

```elixir
    {:earmark, git: "git@github.com:pragdave/earmark.git", override: true},
    {:earmark_parser, git: "git@github.com:RobertDober/earmark_parser.git", override: true},
    {:nimble_publisher, git: "git@github.com:dashbitco/nimble_publisher.git", override: true},
    {:makeup_elixir, ">= 0.0.0"},
    {:makeup_erlang, ">= 0.0.0"},
```


[1]: http://orf.at
[2]: http://orf.at
