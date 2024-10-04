---
title: "Generic Server Processes"
subtitle: "Elixir in Action: Chapter 6"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-04T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

Start by building a simple version of GenServer that supports both synchronous and asynchronous functionality.

A GenServer can maintain a state.

A GenServer has three types of "handles":
- `handle_call`: synchronous message handling
- `handle_cast`: asynchronous message handling
- `handle_info`: non-GenServer-specific message


The chapter provides a periodic clean-up timer as an example.

On to the GenServer-powered go-do server exercise.

## Notable Notes and Quotes

<!--more-->

- The code `Module.__info__(:functions)` returns a list of public module functions and their arity.
- “It’s a good practice to always specify the @impl attribute for every callback function you define in your modules.”
- If you are going to have only a single instance of a GenServer, you should register the name.
  This allows you to refer to the process by name vs pid.
  See `key_value_gen_server_named.ex` in My Github under Chapter 6.




My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
