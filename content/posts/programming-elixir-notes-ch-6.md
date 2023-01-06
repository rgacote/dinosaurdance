---
title: "Programming Elixir Chapter 6 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-15T01:00:00-05:00
subtitle: "Modules and Named Functions"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

1) It takes awhile to get used to not seeing function `return` statements.
Drives home the point that everything is an evaluation.

1) Unlike Python, everything in an Elixir module must be a function (named or anonymous).
Python allows you to run code when a module is loaded but Elixir is compiled, so there's nothing to run.

1) If you define an anonymous function within a module it must either be used or start with the underscore (`_`) character.
    {{< highlight elixir >}}
    defmodule Test do
      hello = fn -> "hello" end
    end

    warning: variable "hello" is unused...prefix it with an underscore
    {{< /highlight >}}

1) Declaring named functions with and without syntactic sugar.
   Chapter 6 tends to use without syntactic sugar for short functions.
    {{< highlight elixir >}}

    # With syntactic sugar
    defmodule Ex do
      def double(n) do
        n * 2
      end

      # Without syntactic sugar
      def treble(n), do: n * 3
    end

    Ex.double 3
    Ex.treble 3
    {{< /highlight >}}

1) Elixir pattern matching is depending on code order, runs from the top down.

1) I seem to have missed the discussion on how to handle list iteration.
   Had to look up how to split list into first/rest. (car/cdr anyone?)
    {{< highlight elixir >}}
    def sumit([first | rest]), do: ...
    {{< /highlight >}}

1) I found the explanation of using a function head and default parameters confusing, but the `Params` example is clarifying.

1) Ranges are maps. There doesn't seem to be a way to check that a map is specifically a range.

1) My solution to the Chopped exercise:
    {{< highlight elixir >}}
    defmodule Chopped do

      def guesser(actual, guessed, _min, _max) when actual == guessed do
        IO.puts("Final Guess: #{guessed}\n\n")
      end

      def guesser(actual, guessed, min, max) when actual > guessed do
        IO.puts("Actual > guessed: #{actual} > #{guessed}")
        guessed = min + div(max - min, 2) + 1
        min = Enum.min([guessed, actual])
        IO.puts("guessed/min/max-> #{guessed}/#{min}/#{max}\n")
        guesser(actual, guessed, min, max)
      end

      def guesser(actual, guessed, min, max) when actual < guessed do
        IO.puts("Actual < guessed: #{actual} < #{guessed}")
        guessed = min + div(max - min, 2) + 1
        max = Enum.max([guessed, actual])
        IO.puts("guessed/min/max-> #{guessed}/#{min}/#{max}\n")
        guesser(actual, guessed, min, max)
      end

      def guess(actual, min..max) when is_integer(actual) and min == actual and max == actual do
        actual
      end

      def guess(actual, min..max) when is_integer(actual) and min <= actual and max >= actual do
        # Make max the first guess.
        IO.puts("First guess: #{max}")
        guesser(actual, max, min, max)
      end

      def guess(actual, min..max) when is_integer(actual) do
        IO.puts("#{actual} is not in the range #{min}..#{max}")
      end
    end

    Chopped.guess(10, 1..88)
    {{< /highlight >}}

    {{< highlight elixir>}}

    Actual > guessed: 10 > 8
    guessed/min/max-> 6/6/10

    Actual > guessed: 10 > 6
    guessed/min/max-> 9/9/10

    Actual > guessed: 10 > 9
    guessed/min/max-> 10/10/10

    Final Guess: 10
    :ok
    {{< /highlight >}}

_All notes and comments are my own opinion._
