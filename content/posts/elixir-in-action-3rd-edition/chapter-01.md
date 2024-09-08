---
title: "Overview of Erlang/Benefits of Elixir"
subtitle: "Elixir in Action: Chapter 1"
author: "ray.cote@mac.com"
type: ""
date: 2024-09-09T00:01:00-05:00
image: ""
tags: [LearningElixir, Elixir, ElixirInAction]
---

The book opens with a high level overview the technologies on which Elixir is built: Erlang and the BEAM.

I've always benefitted from being familiar with the level below where I was programming.
In Python, I'd look at the AST and bytecode; in Pascal, the p-code; in C, the assembly code, and in assembly code I had hardware emulators (and Soft-ICE back in the day).

One focus is a review of how you can use the Elixir/Erlang/BEAM environment to create self-contained server-side systems that include web server, background jobs, caches, crash recovery, etc.


## Notable Notes and Quotes



<!--more-->

- “Unless a system is responsive and reliable, it will eventually fail to fulfill its purpose.”
- “Concurrency is at the heart and soul of Erlang systems.”
- “Erlang processes are completely isolated from each other. They share no memory, and a crash of one process doesn’t cause a crash of other processes.”
- “Communication between processes works the same way regardless of whether these processes reside in the same BEAM instance or on two different instances on two separate, remote computers.”
- _[…]_ “BEAM concurrency and microservices complement each other well, and they are often used together, in practice.”
- “Elixir is an alternative language for the Erlang virtual machine that allows you to write cleaner, more compact code that does a better job of revealing your intentions.”


_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
