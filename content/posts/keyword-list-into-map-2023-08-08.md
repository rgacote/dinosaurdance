---
title: "Convert Keyword List into Map"
# subtitle: "OptionParser"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-08T02:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, OptionParser]
#LearningElixir #Elixir #OptionParser
---

I found a [gentle](https://clairettran.medium.com/elixir-beginner-ii-tutorial-ab219ba6f4cd)
and an [in-depth](https://inquisitivedeveloper.com/learn-with-me-elixir-elixirlargesort-intgen-project-part-2-77/)
article about [OptionParser](https://hexdocs.pm/elixir/1.15.4/OptionParser.html).
Neither quite matched my specific use case of pattern matching options at the function level.

The key is converting the `opts` keyword list into a map.

<!--more-->

```elixir
defmodule Simple do
  def test(commandline) do
    {opts, _argv, _errors} = OptionParser.parse(commandline, switches: [pan_length: :integer])

    opts
    |> Enum.into(%{})
    |> doit()
  end

  def doit(%{pan_length: matches}) do
    IO.puts("PAN length is #{matches}")
  end

  def doit(%{}) do
    IO.puts("No PAN length given.")
  end
end

Simple.test(["--pan-length", "12"])
Simple.test([])
Simple.test(["--some-other-flag"])
```
