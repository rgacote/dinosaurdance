---
title: "Programming Elixir Chapter 7 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-10T01:00:00-05:00
subtitle: "Lists and Recursions"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

Making the best of recursion.

<!--more-->

1) Chapter 7 uses recursion where I would use iteration or list comprehension in Python.

1) Exercises 1 thru 4 solved:
    {{< highlight elixir >}}
    defmodule MyList do

      # ListsAndRecursions-1
      def mapper([], _func), do: []

      def mapper([head | tail], func), do: [func.(head) | mapper(tail, func)]

      def reduce([], value, _func), do: value

      def reduce([head | tail], value, func) do
        reduce(tail, func.(head, value), func)
      end

      def mapsum(lst, func) do
        # Map the function.
        reduce(mapper(lst, func), 0, &(&1 + &2))
      end


      # ListsAndRecursions-2
      defp maximum([], maxie), do: maxie

      defp maximum([head | tail], maxie) when head <= maxie do
        maximum(tail, maxie)
      end

      defp maximum([head | tail], maxie) when head > maxie do
        maximum(tail, head)
      end

      def max([]), do: []

      def max([head | tail]) do
        maximum([head | tail], head)
      end

       @lower_a 97
       @lower_z 122

      # ListsAndRecursions-3
      defp caesar_wrap(val, offset) do
        # Caesar works on only one case.
        # Exercise is assuming lowercase letters.
        new_val = val + offset

        cond do
          new_val > @lower_z ->  @lower_a + (new_val - @lower_z)
          true -> new_val
        end
      end

      def caesar([], _offset), do: []

      def caesar(lst, offset) do
        mapper(lst, &caesar_wrap(&1, offset))
      end

    end

    # ListsAndRecursions-4
    def span(from, to) when from==to, do: [to]

    def span(from, to) do
      [from | span(from+1, to)]
    end
    {{< /highlight >}}

    {{< highlight elixir>}}
    # ListsAndRecursions-1
    MyList.mapsum([1, 2, 3], &(&1 * &1))
    14

    # ListsAndRecursions-2
    MyList.max([1, 10, 3, 5, 88, -1])
    88

    # ListsAndRecursions-3
    MyList.caesar('abcxyz', 13)
    'noplmn'

    # ListsAndRecursions-4
    MyList.span(1,10)
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    {{< /highlight >}}


_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
