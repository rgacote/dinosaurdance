---
title: "Programming Elixir Chapter 13 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-20T01:00:00-05:00
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
- Sort of duplicated the code.
- In playing around with the `Poison` module I accidentally used `encode!` instead of `parse!`,
which led me down a rabbit hole of learning how to debug in IEx.

### OrganizingAProject-4
[My Solution](https://github.com/rgacote/ProgrammingElixirExercises/tree/OrganizingAProject-4/issues)
is moderately different from Dave's.
I see where I can improve efficiencies by using map/reduce and doing additional pipelining.

Most importantly, it works!

- Spent a lot of time Googling.
- Wrapping my head around piping and enumeration.
- Testing helps.
- Short snippets in LiveBook helps.
- Practiced documenting.

- Reduce a list of maps into a map:
  {{< highlight elixir >}}
  Enum.reduce(list_of_maps, fn x, y ->
    Map.merge(x, y, fn _k, v1, v2 -> v2 ++ v1 end)
  end)
  {{< /highlight >}}

- Reduce a list of tuples into a map:
  {{< highlight elixir >}}
  Enum.into(list, %{})
  {{< /highlight >}}


_All notes and comments are my own opinion._
