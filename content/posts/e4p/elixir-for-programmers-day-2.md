---
title: "A Mad Dash Through Elixir Types"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-13T00:00:01-05:00
subtitle: "Elixir for Programmers, Second Edition"
image: ""
tags: [LearningElixir, Elixir, IEx, ElixirForProgrammers]
---

## Notes

1. `?≠` returns  a codepoint: `8800`.

1. Dividing two integers returns a float. Use `div` and `trunc` to get integer results.

1. In Elixir, `nil` is `false`.

1. Regular expressions are based on PCRE (Perl lives on!).

1. `=~` performs a regular expression match
   {{< highlight elixir >}}
   iex> str = "once upon a time"
   iex> str =~ ~r/u..n/
   true
   {{< /highlight >}}

1. `=~` also accepts a string as its right hand argument,
   in which case it returns true if the left string contains the right.

1. Lists are not arrays. You cannot calculate an offset to a specific element.

1. `map[:missingKey]` returns `nil`. `map.missingKey` raises an exception.

<!--more-->

## Exercises

### Strings
* Interpolate current date/time using double-quoted string and a sigil.
  {{< highlight elixir >}}
  iex> now = Time.utc_now

  iex> "The time is approximately #{now.hour}:#{now.minute} UTC."
  "The time is approximately 13:34 UTC."

  iex> ~s/The time is approximately #{now.hour}:#{now.minute} UTC./
  "The time is approximately 13:34 UTC."
  {{< /highlight >}}

* Use IO.puts to output: `1 + 2 = #{ 1 + 2 }`
  {{< highlight elixir >}}
  iex> IO.puts(~S"1 + 2 = #{ 1 + 2 }")
  1 + 2 = #{ 1 + 2 }
  :ok
  {{< /highlight >}}

* Convert string into a list of words.
    {{< highlight elixir >}}
    iex> ~w/now is the time/
    ["now", "is", "the", "time"]
    {{< /highlight >}}

### Regular Expressions
* Return `true` if string contains an `a`, followed by any single character, followed by a `c`.
    {{< highlight elixir >}}
    iex> str =~ ~r/a.c/
    true
    {{< /highlight >}}

* Replace every occurrence of `cat with `dog`.
    {{< highlight elixir >}}
    iex>  Regex.replace(~r/cat/, "double cat cats", "dog")
    "double dog dogs"
    {{< /highlight >}}

* Replace only the first occurrence:
    {{< highlight elixir >}}
    iex>  Regex.replace(~r/cat/, "double cat cats", "dog", global: false)
    "double dog cats"
    {{< /highlight >}}



_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
