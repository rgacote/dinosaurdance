---
title: "Programming Elixir Chapter 16 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-14T01:00:00-05:00
subtitle: "Nodes-The Key to Distributing Services"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

Atoms can be registered globally across all nodes.
This allows us to, for example, find the one generator in a set of nodes.

One globally registered atom is the group leader.
All IO is done through the group leader.
Exercise #4 demonstrates how the group leader can be managed.

<!--more-->

1. Inter-node security is determined by passing a cookie.

1. By default, all nodes on a single machine are given access to each other.

1. Cookies are transmitted in plaintext.

1. Ticker.ex [source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/nodes/ticker.ex).

## Nodes-1
Run a directory listing from two nodes.


## Nodes-2
Why is the tick "about" every 2 seconds vs precisely every two seconds?

### Answer
These are software timers, not hardware timers.
Systems may have a lot of processes running which cause some small timer jitter.

## Nodes-3
Alter the code so that successive ticks are sent to each registered client.
I modified the exercise to include the parent on one of the ticks.

### Answer
[Source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/nodes/nodes03.ex) source code.

## Nodes-4
Reimplement as a ring of clients.

### Answer
Ended up using the [example](https://github.com/pcewing/programming-elixir-exercises/blob/master/ch15/Nodes-4/ticker.exs) from [Paul Ewing](https://github.com/pcewing)

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
