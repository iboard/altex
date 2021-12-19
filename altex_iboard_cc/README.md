# WebClient for Altex

A basic web client for the Altex applications. This is a Phoenix application
excluding ecto nut using Altex-modules by referencing them as a path-dependency
until we have a releas where we have published each single Altex-project as a
Hex package.

## Altex Mix projects

- `../axentity` A general "Entity" protocol. Entities are wrapper around any
   valid term and makes it possible to store those data in a "Repository".

- `../axrepo` A general "Data repository" to persist and load `Entities` from
  somewhere. Axrepo provides an In-Memory and a On-Disk implementation. If
  you think an application without a SQL-database isn't a real application,
  its up to you to just implement a SQL-implementation.


|mix project|CI|documentation|
|-----------|--|-------------|
| [axentity][] | [![CIB axentity][]](https://github.com/iboard/axentity/actions/workflows/elixir.yml) | [![DB axentity][]](https://hexdocs.pm/axentity) |
| [axrepo][] | [![CIB axrepo][]](https://github.com/iboard/axrepo/actions/workflows/elixir.yml) | [![DB axrepo][]](https://hexdocs.pm/axrepo) |
| [ax_webclient][] | [![CIB ax_webclient][]](https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml) | [![DB ax_webclient][]](https://hexdocs.pm/ax_webclient) |



[axentity]: https://github.com/iboard/axentity
[CIB axentity]: https://github.com/iboard/axentity/actions/workflows/elixir.yml/badge.svg
[DB axentity]: https://img.shields.io/badge/docs-hexpm-blue.svg

[axrepo]: https://github.com/iboard/axrepo
[CIB axrepo]: https://github.com/iboard/axrepo/actions/workflows/elixir.yml/badge.svg
[DB axrepo]: https://img.shields.io/badge/docs-hexpm-blue.svg

[ax_webclient]: https://github.com/iboard/ax_webclient
[CIB ax_webclient]: https://github.com/iboard/ax_webclient/actions/workflows/elixir.yml/badge.svg
[DB ax_webclient]: https://img.shields.io/badge/docs-hexpm-blue.svg
