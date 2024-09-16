---
title: "Data Abstractions"
subtitle: "Elixir in Action: Chapter 4"
author: "ray.cote@mac.com"
type: ""
date: 2024-09-18T00:01:00-05:00
image: ""
tags: [Beginner, MyElixirStatus, ElixirInAction]
---

Building higher-level data structures.

The chapter states that modifier functions (functions that transform the data), such as `String.upcase` return data of the same type.
What seems to be missing from the chapter is a discussion of _conversion_ functions, functions that change the data into a different type.
For example, `Money.to_string`.

If found that typing and testing all the small code snippets added to my Elixir "muscle memory" and seeing what standard practices look like.
For example, when updating todo list example, I would not have thought of passing a lambda function for the update vs. just passing new data.
The lambda function provides much more flexibility at the cost of some slight complexity increase (at least I'm still seeing it as a complexity increase at this stage).

I need to get more comfortable with updating structures.
Spending a lot of time staring at this code before comprehending it.

``` elixir
def delete_entry(todo_list, entry_id) do
    %TodoList{todo_list | entries: Map.delete(todo_list.entries, entry_id)}
  end
```

## CSV Import Exercise

My solution was functionally identical to Saša's except I tried to do everything inline in a single pipe.
Saša broke out the pipelined actions into two functions (`read_lines` and `create_entries`).
Also used a multi-step anonymous function in a `Stream.map`.
I need to remember that anonymous functions don't need to be simple one-liners.

## Notable Notes and Quotes

<!--more-->

- “abstractions are implemented with pure, stateless modules.”
- Use maps vs complex function parameter lists. Encapsulates the data and increases ability to add parameters.
- “A struct may exist only in a module, and a single module can define only one struct.”
- A struct pattern can't match a map, but a map pattern can match a struct.
- A protocol is a module in which you declare functions without implementing them.

Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
