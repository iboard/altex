# Altex


_Altex_ is a bunch of independent _mix-projects_ which works together to support
a clean architecture in your code.

This repository, "altex" contains scripts to test, build, and deploy all of the
mix-projects. Something like a mix-ubrella project but without the umbrella ;-)

## Mix projects

- `../[axentity][]` A general "Entity" protocol. Entities are wrapper around any
   valid term and makes it possible to store those data in a "Repository".

- `../[axrepo][]` A general "Data repository" to persist and load `Entities` from
  somewhere. Axrepo provides an In-Memory and a On-Disk implementation. If
  you think an application without a SQL-database isn't a real application,
  its up to you to just implement a SQL-implementation.

- `../[ax_webclient][]` This package. 
- [See in action at altex.iboarc.cc](https://altex.iboard.cc)
  The web-page made out from path `altex/altex_iboard_cc` in this code repository.
  
- `../[state_server][]` macro-sugar for GenServers. 
  
### Project states

|mix project|CI|documentation|
|-----------|--|-------------|
| [axentity][] | [![CIB axentity][]](https://github.com/iboard/axentity/actions/workflows/elixir.yml) | [![DB axentity][]](https://hexdocs.pm/axentity) |
| [axrepo][] | [![CIB axrepo][]](https://github.com/iboard/axrepo/actions/workflows/elixir.yml) | [![DB axrepo][]](https://hexdocs.pm/axrepo) |
| [ax_webclient][] | [![CIB ax_webclient][]](https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml) | [![DB ax_webclient][]](https://hexdocs.pm/ax_webclient) |
| [ax_stateserver][] | [![CIB ax_stateserver][]](https://github.com/iboard/state_server/actions/workflows/elixir.yml) | [![DB ax_stateserver][]](https://hexdocs.pm/ax_webclient) |

 
## Hex Packages

- [axentity hex.pm][]
- [axrepo hex.pm][]
- [ax_webclient hex.pm][]
- [ax_stateserver hex.pm][]


## Blog

Visit [Altex' Blog][] to see `ax_webclient` in action. The source of the entire blog,
including the posts, can be find here, in `./altex_iboard_cc/` which is just a copy
of `ax_webclient` but with the posts added in `priv/posts/...`.



[axentity]: https://github.com/iboard/axentity
[CIB axentity]: https://github.com/iboard/axentity/actions/workflows/elixir.yml/badge.svg
[DB axentity]: https://img.shields.io/badge/docs-hexpm-blue.svg

[axrepo]: https://github.com/iboard/axrepo
[CIB axrepo]: https://github.com/iboard/axrepo/actions/workflows/elixir.yml/badge.svg
[DB axrepo]: https://img.shields.io/badge/docs-hexpm-blue.svg

[ax_webclient]: https://github.com/iboard/ax_webclient
[CIB ax_webclient]: https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml/badge.svg
[DB ax_webclient]: https://img.shields.io/badge/docs-hexpm-blue.svg

[ax_stateserver]: https://github.com/iboard/state_server
[CIB ax_stateserver]: https://github.com/iboard/state_server/actions/workflows/elixir.yml/badge.svg
[DB ax_stateserver]: https://img.shields.io/badge/docs-hexpm-blue.svg

[NimblePublisher]: https://github.com/dashbitco/nimble_publisher
[Altex' Blog]: https://altex.iboard.cc

[axentity hex.pm]: https://hex.pm/packages/axentity
[axrepo hex.pm]: https://hex.pm/packages/axrepo
[ax_webclient hex.pm]: https://hex.pm/packages/ax_webclient

