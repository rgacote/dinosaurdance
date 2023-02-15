---
title: "Programming Elixir Chapter 21 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-24T01:00:00-05:00
subtitle: "Tasks and Agents"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

Agents are processes that maintain state.
Effectively, this is wrapping the `Stack.Stash` process we've implemented earlier.

<!--more-->

1. An Elixir Task wraps OTP message passing.

1. Instead of calling a process with `start_link` and then waiting for the response with `receive`,
you start the process with `Task.async` and then `Task.await` on the specific pid.

1. Tasks are OTP servers and can be added to the Supervisor tree.

1. `Task.await` cannot be used with tasks started by the Supervisor as we don't know the pid to await.

1. The first Agent example shows passing an initialization function vs. a value.
Need to research if this is mandatory.

1. The phrase `&(&1)` is the _identify function_ and used to retrieve the current state.
    {{<highlight elixir >}}
    {:ok, count } = Agent.start(fn -> 0 end)
    Agent.get(count, &(&1))
    Agent.update(count, &(&1 + 1))
    {{< /highlight >}}


_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
