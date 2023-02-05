---
title: "Programming Elixir Chapter 12 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-18T01:00:00-05:00
subtitle: "Control Flow"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

Elixir has an `unless` keyword, which I don't recall seeing in any other language I've used.

“Elixir exceptions are intended for things that should never happen in normal operation”

Trailing `!` in a function name is an Elixir convention indicating failure raises an exception.
   We've already seeing this in the `File.open!` call in previous exercises.

<!--more-->

## Exercises

### ControlFlow-1
All my FizzBuzz's in one place.

{{< highlight elixir >}}
defmodule FizzBuzzMatch do

  def fizzbuzz(count) when rem(count, 15) == 0, do: "FizzBuzz"
  def fizzbuzz(count) when rem(count, 3) == 0, do: "Fizz"
  def fizzbuzz(count) when rem(count, 5) == 0, do: "Buzz"
  def fizzbuzz(count), do: count
end

defmodule FizzBuzzCond do
  def fizzbuzz(count) do
    cond do
      rem(count, 15) == 0 -> "FizzBuzz"
      rem(count, 3) == 0 -> "Fizz"
      rem(count, 5) == 0 -> "Buzz"
      true -> count
    end
  end
end

defmodule FizzBuzzCase do
  def fizzbuzz(count) do
    case { rem(count, 3), rem(count, 5) } do
      {0, 0} -> "FizzBuzz"
      {0, _} -> "Fizz"
      {_, 0} -> "Buzz"
      {_, _} -> count
    end
  end
end

defmodule FizzBuzzIfElse do
  def fizzbuzz(count) do
    if rem(count, 15) == 0 do
      "FizzBuzz"
    else if rem(count, 3) == 0 do
      "Fizz"
    else if rem(count, 5) == 0 do
      "Buzz"
    else
      count
    end
    end
    end
  end
end


for count <- 1..25 do
  FizzBuzzMatch.fizzbuzz(count)
  #FizzBuzzCond.fizzbuzz(count)
  #FizzBuzzCase.fizzbuzz(count)
  #FizzBuzzIfElse.fizzbuzz(count)
end
{{< /highlight >}}


### ControlFlow-2
Pattern matching is the most compact and the easiest to read.
Second choice is the `cond` implementation.
I like how it calculates once and then pattern matches against the results.

The least readable/maintainable is the `if/else` approach which I would have previously taken with Python
(at least until Python 3.10 pattern matching).

I find I'm starting to dislike lots of indenting.
Easier to understand and maintain flatter functions.

### ControlFlow-3
Write an `ok!` function.

{{< highlight elixir >}}
defmodule Ch12 do
  def ok!({:ok, data}), do: data
  def ok!({error_type, error_msg}), do: raise "#{error_type}: #{error_msg}"

end

path = Path.expand("~/play/orders.csv")
# file = Ch12.ok! File.open(path)
file = Ch12.ok! File.open("abcd")

{{< /highlight >}}

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
