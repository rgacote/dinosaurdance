---
title: "Always be Normalizing"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-12T00:00:01-05:00
subtitle: "Elixir for Programmers, Second Edition"
image: ""
tags: [LearningElixir, Elixir, ElixirForProgrammers]
---

I ran into the UTF-8 normalization issue when playing around with the `String.split` exercises.

Some non-ASCII values can be represented by either one or two graphemes.
For example `ô` can be a single grapheme or composed of two graphemes, `o` and `^`.
Always working with normalized UTF-8 strings avoids confusion.

There are four types of UTF normalization which you can read about on the [Unicode.org](https://unicode.org/reports/tr15/) site.
Elixir seems to prefer the Canonical Decomposition (NFD) form as that is what the `String.equivalent?` function uses.

The following examples demonstrate:

<!--more-->

{{< highlight elixir >}}
# Add a diacritical to a base ASCII character
iex(1)> "o\u0302"
"ô"

iex(3)> "o\u0302" == "ô"
false

iex(3)> String.normalize("o\u0302", :nfd) == "ô"
false

iex(4)> String.normalize("o\u0302", :nfd) == String.normalize("ô", :nfd)
true

iex(5)> String.normalize("o\u0302", :nfc) == "ô"
true
{{< /highlight >}}

The non-normalized results may vary based on the platform/shell you use.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
