---
title: "Programming Elixir Chapter 10 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-21T01:00:00-05:00
subtitle: "Processing Collections–Enum and Stream"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

## Enums
1) Earlier chapters focused on list processing via recursion.
Now we're getting into the more familiar iterables.

1) Stream is similar to the Python Generator; calculate next value as needed.

1) `Enum.at` uses a zero-based index.
   `Enum.att(10..20, 0)` is `10`.

1) After working through the first set of exercises, the need to use recursion vs. iteration became clearer.


## Exercise: Lists and Recursions 5

### all?
Apply a function to the collection.
Return true if all evaluations are true, else false.

We've not yet discussed how to break out of iterations.
Solution is inefficient for large lists.
{{< highlight elixir >}}
defmodule Ch10 do
  def all?([], _) do
    false
  end

  def all?(lst, func) do
    Enum.reduce(Enum.map(lst, func), true, &(&1 and &2))
  end
end

Ch10.all?([], &(&1 > 5))
Ch10.all?([8, 9, 10],  &(&1 > 5))
Ch10.all?([8,3,21],  &(&1 > 5))

{{< /highlight >}}

### each
Invoke the given func for each element in the enumerable and return :ok.
The Elixir documentation example shows using it with IO.puts.

{{< highlight elixir >}}
defmodule Ch10 do

  def each(lst, func) do
    for el <- lst do
      func.(el)
    end
  :ok
  end
end

Ch10.each([1, 3, 5], &(IO.puts(&1)))
{{< /highlight >}}

## filter
{{< highlight elixir >}}
defmodule Ch10 do

  # filter
  #  Return only those elements for which func returns a truthy value.
  #  Finally gave up and looked up the official implementation.
  #  I'm still thinking in too much Python.
  #  List generation is different in Elixir.
  #  (This is not the official implementation.)
  defp filter_list([], _) do
    []
  end

  defp filter_list([head | tail], func) do
    if func.(head) do
      [head | filter_list(tail, func)]
    else
      filter_list(tail, func)
    end
  end

  def filter(lst, func) do
    filter_list(lst, func)
  end
end

Ch10.filter([1, 2, 3], fn x -> rem(x, 2) == 0 end)
{{< /highlight >}}


### split
Splits the enumerable into two enumerables, leaving the count elements in the first one.
If count is a negative number, it starts counting from the back to the beginning of the enumerable.

Ended up looking up this code as well as I could not figure out how to return the tuple.
I now understand that pattern matching and guards can be used to return the final value that is different from what the recursion returns.

The recursion is building an accumulator and what is left of the list.
After recursing through the `count` number of elements, return the accumulated elements and the list remnant in the tuple.

The accumulated element list must be reversed because the iteration prepends.

### take
Returns an amount of elements from the beginning (positive amount) or end (negative amount) of the enumerable.

I could simply call split and return first element of the tuple but I implemented it long-form using what I learned about split.
{{< highlight elixir >}}
defmodule Ch10 do
  defp take_up_to(_, 0, acc)  do
    :lists.reverse(acc)
  end

  defp take_up_to([], _, acc) do
    :lists.reverse(acc)
  end

  defp take_up_to([head | tail], count, acc) do
    take_up_to(tail, count - 1, [head | acc])
  end

  def take([], _) do
    []
  end

  def take(lst, count) when count < 0 do
    :lists.reverse(take_up_to(:lists.reverse(lst), abs(count), []))
  end
  def take(lst, count) do
    take_up_to(lst, count, [])
  end
end

Ch10.take([1,2,3], -2)

{{< /highlight >}}

## Exercise: Lists and Recursions 6 -- First Attempt
Write a flatten(list).
The exercise is marked as hard and notes I may need to call Enum.reverse.
Did not find it difficult and did not need to reverse list.
Obviously not approaching it properly.
It was also inefficient as appending two lists requires a list copy.
{{< highlight elixir >}}
defmodule Ch10 do
  defp flatten_it([]) do
    []
  end

  defp flatten_it([head | tail]) when is_list(head) do
    # Head is a list.
    IO.inspect head, label: "sublist"
    flatten_it(head) ++ flatten_it(tail)
  end

  defp flatten_it([head | tail]) do
    # Head is not a list.
    IO.inspect head, label: "element"
    [head | flatten_it(tail)]
  end

  def flatten(lst) do
    flatten_it(lst)
  end
end

Ch10.flatten([ 1, [ 2, 3, [4] ], 5, [[[6]]]])

{{< /highlight >}}

## Exercise: Lists and Recursions 6 -- Recursively
Re-solved the problem with recursion.

{{< highlight elixir >}}
defmodule Ch10 do
  defp flatten_it([], acc) do
    acc
  end

  defp flatten_it([head | tail], acc) when is_list(head) do
    # Head is a list.
    IO.inspect head, label: "sublist"
    flatten_it(tail, flatten_it(head, acc))
  end

  defp flatten_it([head | tail], acc) do
    # Head is not a list.
    IO.inspect head, label: "element"
    flatten_it(tail, [head | acc])
  end

  def flatten(lst) do
    Enum.reverse(flatten_it(lst, []))
  end
end

Ch10.flatten([ 1, [ 2, 3, [4] ], 5, [[[6]]]])
{{< /highlight >}}

_All notes and comments are my own opinion._
