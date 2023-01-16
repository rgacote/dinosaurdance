---
title: "Programming Elixir Chapter 11 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-22T01:00:00-05:00
subtitle: "Strings and Binaries"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

1. Strings are UTF-8 encoded.

1. Triple-quotes used for _heredocs_ function slightly differently than Python's triple quotes.
   Python keeps the initial linebreak unless the first line has `\`.
   Elixir _heredocs_ never keep the initial linebreak.

1. A magīa of sigils.
   - Case indicates if the text is to be interpolated (uppercase) or not (lowercase).
   - Multiple delimiter choices.
   - Some sigils have optional specifiers.

1. Double quotes declare strings.
   Single quotes declare character lists.
   Vastly different in the Elixir world.

1. Elixir prints a list of integers as a string if each number in the list is a printable `codepoint`, or character.
   For example:
   - `[6]` displays as `[6]` but `[8]` displays as '\b' (bell).
   - `[126]` displays as `~` but `[127]` displays as `[127]`.

## Exercises
### StringsAndBinaries-1
Write a function that returns true if a single-quoted string contains only printable ASCII characters (space through tilde).

{{< highlight elixir >}}
defmodule Ch11 do
  defp is_printable?([], _) do
    true
  end
  defp is_printable?([head | tail], range) do
    if head in range do
      is_printable?(tail, range)
    else
      raise "Not printable '#{head}'."
    end
  end
  def printable?(clist) do
    is_printable?(clist, 32..127)
  end
end

Ch11.printable?('123')
Ch11.printable?('12ô')
{{< /highlight >}}

### StringsAndBinaries-2
Write an `anagram?(word1, word2)` that returns true if its parameters are anagrams.
- I'm assuming this is for character lists, not strings.
- Must have identical collection of characters.

{{< highlight elixir>}}
defmodule Ch11 do
  def anagram?(word1, word2) do
    Enum.sort(word1) == Enum.sort(word2)
  end
end

Ch11.anagram?('abc', 'cba')
{{< /highlight >}}


### StringsAndBinaries-3
Why does IEx print `'cat'` as a string, but `'dog'` as individual numbers?
- Because the head is a character list of printable characters and the entire list is not (since it has a sublist).

### StringsAndBinaries-4
Write a function that takes a single-quoted string of the form `number [+-*/] number` and returns the result of the calculation.
The individual numbers do not have leading plus or minus signs.
- Cannot use `String.split()` with character lists.
- Does not try to identify an invalid equation.
- The reason for `?x` notation makes much more sense after this exercise.
- Use an Erlang module to convert character list to integer.

{{< highlight elixir>}}
defmodule Ch11 do
  defp calc([?+ | tail], agg) do
    { first, _ } = :string.to_integer(Enum.reverse(agg))
    { second, _ } = :string.to_integer(tail)
    IO.inspect(tail)
    first + second
  end
  defp calc([?- | tail], agg) do
    { first, _ } = :string.to_integer(Enum.reverse(agg))
    { second, _ } = :string.to_integer(tail)
    first - second
  end
  defp calc([?* | tail], agg) do
    { first, _ } = :string.to_integer(Enum.reverse(agg))
    { second, _ } = :string.to_integer(tail)
    first * second
  end
  defp calc([?/ | tail], agg) do
    { first, _ } = :string.to_integer(Enum.reverse(agg))
    { second, _ } = :string.to_integer(tail)
    first / second
  end
  defp calc([head | tail], agg) do
    calc(tail, [head | agg])
  end
  def calculate(equation) do
    calc(equation, [])
  end
end

Ch11.calculate('10+3')
{{< /highlight >}}

#### Compared to Dave's
- created number and operator parsers that skipped spaces;
- created an anonymous function to perform the math.


_All notes and comments are my own opinion._
