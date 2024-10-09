---
title: "Isolating Error Effects"
subtitle: "Elixir in Action: Chapter 9"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-10T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

Use a process registry to track dynamically started and restarted processes by name.
The `via_tuple` function is used to automatically keep track of changing processes pids.

Having multiple Supervisors helps to isolate errors.
One Supervisor child constantly restarting can cause the Supervisor to restart all children.


## Notable Notes and Quotes

<!--more-->

- Supervisors start child processes synchronously, in the order specified.
- Use Supervisors to handle error recovery.


My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
