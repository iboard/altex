%{
  title: "Learn Elixir With The Coding Gnome",
  author: "Andi",
  tags: ~w/2022 elixir learning video/
}
---
# Learn Elixir, Phoenix, and LiveView with Dave Thomas

**[Elixir for Programmers, 2nd edition](https://pragdave.me/)**

It is worth buying this amazing online course, by one of the
best teachers you may find out there, Dave Thomas, The Coding Gnome.

At [e-matrix](https://e-matrix.at) we bought this excelent course
twice because we think it is worth for every programmer to have this it
their own shelf.

## Extract the business logic

We like Dave's approach to first implement a _mix-project_ for the business-logic
and then use this project as an dependency in an extra _phoenix-application_, 
instead of implementing the business logic within the phoenix-project.

## Altex, a POC of this approach

You're reading this post from a Phoenix-application. This simple
blog is implemented from different mix-projects, working together as
[altex](https://github.com/iboard/altex).
