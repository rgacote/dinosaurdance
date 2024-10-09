---
title: "Beyond GenServer"
subtitle: "Elixir in Action: Chapter 10"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-11T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

- Tasks are useful for one-off jobs.
- Agents manage state, they are a simplified interface to a subset of GenServer functionality.

The author prefers GenServers over Agents as GenServers support general `handle_info` messages.
The example shown is a cache cleanup based off a timer, something not implementable in an Agent.

ETS tables need to be attached to a process.
You can start up a GenServer process that creates one or more named ETS tables.
Tables can be accessed directly, no need to go through the GenServer (assuming permissions are set appropriately).

## Notable Notes and Quotes

<!--more-->

- An _awaited task_ executes, sends the result back to the 'caller', then terminates.
- Multiple awaited tasks in the same function return in the order in which they are invoked.
  The order is deterministic.


My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
