---
title: "Fault Tolerance Basics"
subtitle: "Elixir in Action: Chapter 8"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-09T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

A walk through run-time errors and Supervisors.

Three types of run-time errors:
- errors: invalid data operation, missing function, unknown pattern match, or raise your own.
- exits: deliberately terminate a process.
- throw: to catch up the call stack.

The result of a a `try`/`catch`/`after` block is always from either the `try` or `catch` clause, never the `after` clause.

Processes can be linked and monitored.

## Notable Notes and Quotes

<!--more-->

- “Instead of obsessively trying to reduce the number of errors, your priority should be to minimize their effects and recover from them automatically.”
- “_(throw)_ for control flow is hacky and somewhat reminiscent of `goto`, and you should avoid this technique as much as possible.”




My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
