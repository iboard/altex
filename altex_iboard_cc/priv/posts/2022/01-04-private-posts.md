%{
  title: "ax -- private posts",
  author: "andi",
  tags: ~w/andi 2022 blog altex ax/
}
---
# new feature "private posts"

now you can add the tag `private:` as a list of atoms. each atom
can represent a username. the post will be visible for any user in
this list.

### example
```elixir
%{
  title: "private posts",
  author: "andi",
  tags: ~w/andi 2022 blog/,
  draft: true,
  private: ~w/admin andi/a
}
```
