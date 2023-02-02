---
title: "It's All About the Memory"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-02T08:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Erlang]
---

One minute into the [Programming Elixir](https://pragprog.com/titles/elixir16/programming-elixir-1-6/)
book's foreward and the focus is unlike any other programming book I've read.

The foreward by José Valim spotlights the historic necessity of keeping, mutating,
and freeing single piece of memory memory-limited computers.

Computers are no longer getting significantly quicker.
We now get more compute power through multiple CPU cores.
Throughput is parallel.

Managing shared memory across multiple CPU cores is complex and error prone.
A functional language such as Erlang and Elixir removes this complexity.

“As garbage collection once freed developers from the shackles of memory
management, Elixir is here to free you from antiquated concurrency
mechanisms and bring you joy when writing concurrent code.” _José Valim_

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
