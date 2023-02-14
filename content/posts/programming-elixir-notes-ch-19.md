---
title: "Programming Elixir Chapter 19 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-19T01:00:00-05:00
subtitle: "A More Complex Example"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

A day for reading and playing with Dave's code.
I'll be keeping the `duper` source around for future reference to starting multiple servers.

<!--more-->

1. `Map.update/4` is something I wish I'd had in Python.

1. A DynamicSupervisor starts an arbitrary number of workers at runtime.

1. When using DynamicSupervisor, you cannot name the children in the `start_link` function
because the same module is run in multiple child servers.

1. When initializing a server, don't interact with anything that uses the server.

1. Each GenServer call or cast function has a default timeout of five (5) seconds.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
