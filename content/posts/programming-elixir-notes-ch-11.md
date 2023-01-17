---
title: "Programming Elixir Chapter 11 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-17T01:00:00-05:00
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

1. Double quotes declare strings, which are binary lists.
   Single quotes declare character lists.
   Vastly different in the Elixir world.

1. Elixir prints a list of integers as a string if each number in the list is a printable `codepoint`, or character.
   For example:
   - `[6]` displays as `[6]` but `[8]` displays as '\b' (bell).
   - `[126]` displays as `~` but `[127]` displays as `[127]`.

1. The `next_codepoint` example shows how to create a byte list iterator.

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
- created an anonymous function to perform the math;
- used `div` for integer division.

### StringsAndBinaries-5
Write a function that takes a list of double-quoted strings and prints each on a separate line, centered in a column that has the width of the longest string.
Make sure it works with UTF characters.
{{< highlight elixir >}}
defmodule Ch11 do
  defp _longest([], length) do
    length
  end
  defp _longest([head | tail], length) do
    if String.length(head) > length do
      _longest(tail, String.length(head))
    else
      _longest(tail, length)
    end
  end
  defp _centered([], _) do

  end
  defp _centered([head | tail], padding) do
    head_length = div(String.length(head), 2)
    base = String.duplicate(" ", padding - head_length)
    IO.puts(base <> head)
    _centered(tail, padding)
  end
  def center(list) do
    longest = _longest(list, 0)
    IO.puts("Maximum string length: #{longest}.")
    # Want 1/2 of numbers up front.
    _centered(list, div(longest, 2))
  end
end

Ch11.center(["cat", "zebra", "elephant"])
{{< /highlight >}}

#### Compared to Dave's
- used a pipe'd approach
- created a tuple of string and string's length so as to not calculate length twice.
- my approach is still to Python'ish. Need to start using piping more.


### StringsAndBinaries-6
Write a function to capitalize the sentences in a string.
{{< highlight elixir >}}
defmodule Ch11 do
  defp until_period(<< head :: utf8, tail :: binary >>, agg) when head == ?. do
    capitalize(tail, [head | agg])
  end
  defp until_period(<< head :: utf8, tail :: binary >>, agg) do
    until_period(tail, [ head |agg ])
  end
  defp capitalize(<<>>, agg) do
    :string.reverse(agg)
  end
  defp capitalize(<< head :: utf8, tail :: binary >>, agg) when head == 32 do
    capitalize(tail, [:string.to_upper(head) | agg])
  end
  defp capitalize(<< head :: utf8, tail :: binary >>, agg) do
    until_period(tail, [:string.to_upper(head) | agg])
  end
  def capitalize_sentences(sentences) when is_binary(sentences) do
    # First character is start of sentence.
    # Ignore leading spaces as it is not in the problem definition.
    capitalize(sentences, <<>>)
  end
end

Ch11.capitalize_sentences("oh. a dog. woof.")
{{< /highlight >}}

#### Compared to Dave's
- I'm writing much more code;
- done again with pipe and using `String.split`;
- I interpreted problem as working with bytes. Dave uses String module.

### StringsAndBinaries-7
Add tax to orders loaded from a file.

{{< highlight elixir >}}
defmodule Ch11 do
  def calculate_tax(path, tax_rates) do
    read_orders(path)
    |> Enum.map(fn order -> apply_tax(order, tax_rates) end )
  end

  def read_orders(path) do
    file = File.open!(path)
    [header | lines] = Enum.map(IO.stream(file, :line), &String.trim(&1))
    header = String.split(header, ",")
    header = Enum.map(header, &String.to_atom(&1))
    Enum.map(lines, fn line -> parse_order(String.split(line, ","), header) end )
  end

  def parse_order(line, header) do
    line = Enum.zip(header, line)
    id = Keyword.get(line, :id)
    line = Keyword.replace(line, :id, String.to_integer(id))
    net_amount = Keyword.get(line, :net_amount)
    line = Keyword.replace(line, :net_amount, String.to_float(net_amount))
    ship_to = Keyword.get(line, :ship_to)
    Keyword.replace(line, :ship_to, String.to_atom(ship_to))
  end

  def apply_tax(order, tax_rates) do
    net_amount = Keyword.get(order, :net_amount)
    ship_to = Keyword.get(order, :ship_to)
    tax = Keyword.get(tax_rates, ship_to, 0)
    Keyword.put(order, :total_amount, net_amount + (tax * net_amount))
  end
end

tax_rates = [ NC: 0.075, TX: 0.08 ]

orders = Ch11.calculate_tax("orders.csv", tax_rates)
IO.inspect(orders)
{{< /highlight >}}

#### Compared to Dave's
- didn't use stream, so not as efficient for large order files

_All notes and comments are my own opinion._
