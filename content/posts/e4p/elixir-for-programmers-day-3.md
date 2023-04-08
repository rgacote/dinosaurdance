---
title: "Pattern Matching"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-14T00:00:01-05:00
subtitle: "Elixir for Programmers, Second Edition"
image: ""
tags: [LearningElixir, Elixir, IEx, ElixirForProgrammers]
---

Creating a function that declares a parameter twice in order to check if two different passed-in parameters are identical is not something I would have thought of.

Drives home the point that pattern matching within a function is the same pattern matching used to select the function to run.


<!--more-->

## Notes

1. All values on the left-hand side of a pattern match are unbound before the match is made.

1. Avoid this by using the pin (`^`) operator.


## Exercises
1. Write a function that takes a two-element tuple parameter and uses pattern matching to return a two-element tuple with the elements swapped.
    {{< highlight elixir >}}
    defmodule Patterns do
      def swap({a, b}) do
        {b, a}
      end
    end

    Patterns.swap({1, 2})

    {2, 1}
    {{< /highlight >}}

1. Write a function that takes two parameters and returns `true` if they are the same.
   Use pattern matching and not conditional logic.
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
