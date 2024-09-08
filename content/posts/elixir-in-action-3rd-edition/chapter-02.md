---
title: "Building Blocks"
subtitle: "Elixir in Action: Chapter 2"
author: "ray.cote@mac.com"
type: ""
date: 2024-09-10T00:01:00-05:00
image: ""
tags: [LearningElixir, Elixir, ElixirInAction]
---

The nitty gritty of getting started:
- IEx
- Variables
- Code Organization
- Data types
- Operators, and
- Runtime

I finally clicked on the use of `&` in lambdas.
The syntax always looked foreign to me.
The following are equivalent:

``` elixir
lambda = fn a, b, x -> a + b - c
lambda = &(&1 + &2 - &3)
```

## Notable Notes and Quotes

<!--more-->

- When composing a multi-line expression in IEx, typing `#iex:break` on a line breaks out to the base prompt.
- Add the application or library name to the start of module names to ensure they are distinct across modules/projects.
- “A function must always be a part of a module.”
- “Because arity distinguishes multiple functions of the same name, it’s not possible to have a function accept a variable number of arguments”
- The only booleans are `:true` and `:false` (syntactic sugar `true` and `false`).
- `nil` and `false` are _falsy_ values, everything else is _truthy_.
- Lists are linked lists, not arrays. Accessing an element requires traversing the links.
- `Enum.each` iterates without producing a new value. Example is typically `IO.puts`. To change value, use `Enum.map`.
- “A closure always captures a specific memory location. Rebinding a variable doesn’t affect the previously defined lambda that references the same symbolic name”
- Use `apply` to dynamically call functions.


_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
