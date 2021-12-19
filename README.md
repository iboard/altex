# Altex


_Altex_ is a bunch of independent _mix-projects_ which works together to support
a clean architecture in your application.

This repository, "altex" contains scripts to test, build, and deploy all of the
mix-projects. Something like a mix-ubrella project but without the umbrella ;-)

## Projects

- [`axentity`](https://github.com/iboard/axentity) ... `Altex.Entity` to wrap any kind 
  of data (think Ecto)
- [`axrepo`](https://github.com/iboard/axrepo) ... `Altex.Repo` to  store entities in
  memory, to disk, or where not.
- [`ax_webclient`](https://github.com/iboard/ax_webclient) ... `Altex.WebClient` is a
  simple blog implementation, using 
  [NimblePublisher][] and the Altex-tools as dependencies for a _Phoenix_-website.

|mix project|CI|documentation|
|-----------|--|-------------|
| [axentity][] | [![CIB axentity][]](https://github.com/iboard/axentity/actions/workflows/elixir.yml) | [![DB axentity][]](https://hexdocs.pm/axentity) |
| [axrepo][] | [![CIB axrepo][]](https://github.com/iboard/axrepo/actions/workflows/elixir.yml) | [![DB axrepo][]](https://hexdocs.pm/axrepo) |
| [ax_webclient][] | [![CIB ax_webclient][]](https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml) | [![DB ax_webclient][]](https://hexdocs.pm/ax_webclient) |

## Blog

See [Altex' Blog][] to see `ax_webclient` in action.



[axentity]: https://github.com/iboard/axentity
[CIB axentity]: https://github.com/iboard/axentity/actions/workflows/elixir.yml/badge.svg
[DB axentity]: https://img.shields.io/badge/docs-hexpm-blue.svg

[axrepo]: https://github.com/iboard/axrepo
[CIB axrepo]: https://github.com/iboard/axrepo/actions/workflows/elixir.yml/badge.svg
[DB axrepo]: https://img.shields.io/badge/docs-hexpm-blue.svg

[ax_webclient]: https://github.com/iboard/ax_webclient
[CIB ax_webclient]: https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml/badge.svg
[DB ax_webclient]: https://img.shields.io/badge/docs-hexpm-blue.svg

[NimblePublisher]: https://github.com/dashbitco/nimble_publisher
[Altex' Blog]: https://altex.iboard.cc
