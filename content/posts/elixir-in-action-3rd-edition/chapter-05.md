---
title: "Concurrency Primitives"
subtitle: "Elixir in Action: Chapter 5"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-02T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

Though primarily about processes, messages, and servers, another thing I found significant in this chapter is the liberal use of lambda functions.
Many places where I would tend to create a new function and then call it are replaced with lambda functions.
Need to become more comfortable with this.


## Notable Notes and Quotes

<!--more-->

- “To make a process run forever, you must use endless tail recursion.”
- “A server process can be considered a synchronization point.”
- “You can refactor this _(loops)_ by relying on pattern matching and moving the message handling to a separate multiclause function. This keeps the code of the loop function very simple”


My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
