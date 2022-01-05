%{
  title: "Private Posts",
  author: "Andi",
  tags: ~w/andi 2022 blog altex/
}
---
# New Feature "Private Posts"

Now you can add the tag `private:` as a list of atoms. Each atom
can represent a username. The post will be visible for any user in
this list.

### Example
```elixir
%{
  title: "Private Posts",
  author: "Andi",
  tags: ~w/andi 2022 blog/,
  draft: true,
  private: ~w/admin andi/a
}
```
