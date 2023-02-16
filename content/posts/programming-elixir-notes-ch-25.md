---
title: "Programming Elixir Chapter 25 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-03-03T01:00:00-05:00
subtitle: "More Cool Stuff"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

Protocols remind me of Python's duck typing.

<!--more-->

## Writing Your Own Sigils

1. Lowercase sigils interpolate their parameters, uppercase sigils do not.

1. User-defined sigils are not globally available. Need to be imported.
Reduces the risk of running into a system-defined sigil.

## Multi-app Umbrella Projects
There seems to be some community disagreement about umbrella projects.
My basic understanding is that it is likely not something I should consider except for
extremely large and/or complex projects.

## MoreCoolStuff-1
Write a `~v` sigil that parses multiple lines of csv data.
Return a list of lists.

{{< highlight elixir >}}
defmodule CsvSigil do
  @doc """
  Implement the `~v` sigil to parse rows of comma-separated data into a list of lists.
  Ignore any spaces before commas and trailing commas.
  Allows interpolation.

  ## Example usage
      iex> import CsvSigil
      iex> ~v"""
      ...>1,2,#{3}
      ...>cat,dog
      ...>"""
      [["1","2","3"], ["cat","dog"]]
  """

  def sigil_v(lines, _opts) do
    lines
    |> String.trim_trailing
    |> String.split("\n")
    |> Enum.map(fn x -> String.split(x, ",") end)
  end
end

{{< /highlight >}}
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
