---
title: "Programming Elixir Chapter 13 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-12-30T01:00:00-05:00
subtitle: "Organizing a Project"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---



1. `mix new` did not create the ./config directory.

1. `elem` accesses a tuple by index.

1. Elixir [builtins](http://elixir-lang.org/docs.html)
1. Erlang [documentation](http://erlang.org/doc/) _Application Group_ sidebar.
1. Elixir [hex](https://hex.pm)

1. Version control the mix.lock for applications. Review when building a public library.

1. Mix.Config is deprecated. Use [Config](https://hexdocs.pm/elixir/1.14.3/Config.html)

## Exercises

### OrganizingAProject-1
Copied the project as recommended.

### OrganizingAProject-2
Added dependency as directed.

### OrganizingAProject-3
Sort of duplicated the code.
In playing around with the `Poison` module I accidentally used `encode!` instead of `parse!`,
which led me down a rabbit hole of learning how to debug in IEx.
Useful exercise overall.

_All notes and comments are my own opinion._
