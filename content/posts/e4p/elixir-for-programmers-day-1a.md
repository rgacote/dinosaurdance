---
title: "String Splitting and Trimming"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-11T00:00:01-05:00
subtitle: "Elixir for Programmers, Second Edition"
image: ""
tags: [LearningElixir, Elixir, ElixirForProgrammers]
---

I had some confusion with the `String.split` function in yesterday's exercises.
The [documentation](https://hexdocs.pm/elixir/1.14/String.html) says that the `trim: true` option removes empty strings from the resulting list.

The important term here is "empty", not "blank" or "whitespace".
My Python-brain was still thinking of trim (or strip) options meaning whitespace is stripped from start/end of the source string.


For example:

<!--more-->
{{< highlight  elixir >}}
iex(1)> "  bobby  jones  " |> String.split("", trim: true)
[" ", " ", "b", "o", "b", "b", "y", " ", " ", "j", "o", "n", "e", "s", " ", " "]
{{< /highlight>}}

What I found more confusing, is the behavior when the `trim: true` option is not used when splitting a string into graphemes:
{{< highlight  elixir >}}
iex(2)> "  bobby  jones  " |> String.split("")
["", " ", " ", "b", "o", "b", "b", "y", " ", " ", "j", "o", "n", "e", "s", " ",
 " ", ""]

iex(3)> "" |> String.split("")
["", ""]
{{< /highlight>}}

Splitting an empty string into graphemes returns two empty strings.

I found a [discussion](https://elixirforum.com/t/why-does-string-split-2-return-empty-strings-at-beginning-and-end/52959)
on Elixir Forum where @sergio asked this question and @whatyouhide from the Elixir core team answered:

"You can think of it as there’s an empty string between every pair of graphemes in a string.
There’s also an empty string between the start of the string and the first grapheme, sort of.
It also helps with having some properties that hold true for String.split/2."

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
