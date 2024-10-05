---
title: "Building a Concurrent System"
subtitle: "Elixir in Action: Chapter 7"
author: "ray.cote@mac.com"
type: ""
date: 2024-10-06T00:01:00-05:00
image: ""
tags: [MyElixirStatus, ElixirInAction]
---

The GenServer `handle_call` function returns state to the GenServer, which messages it back to the caller.
You can also spawn a worker process, return state to the GenServer instructing it _not_ to message back to the caller, then send a message directly from the spawned worker function.

Example provided in the chapter:

``` elixir
def handle_call({:get, key}, caller, state) do
  spawn(fn ->
    data = case File.read(file_name(key)) do
      {:ok, contents} -> :erlang.binary_to_term(contents)
      _ -> nil
    end

    GenServer.reply(caller, data)
  end)

  {:noreply, state}
end
```



## Notable Notes and Quotes

<!--more-->

- Use the `handle_continue` function to implement a slow GenServer initialization process.
- Downside: you won't know if it succeeded.
- _Tests are broken as they do not clear the ./persist/ directory between runs._

My Github [repository](https://github.com/rgacote/ElixirInAction3rdEdition).
Book samples Github [code samples](https://github.com/sasa1977/elixir-in-action).

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
