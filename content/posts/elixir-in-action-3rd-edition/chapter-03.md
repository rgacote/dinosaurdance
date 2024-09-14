---
title: "Control Flow"
subtitle: "Elixir in Action: Chapter 3"
author: "ray.cote@mac.com"
type: ""
date: 2024-09-16T00:01:00-05:00
image: ""
tags: [Beginner, MyElixirStatus, ElixirInAction]
---

Chapter 3 opens with an introduction to pattern matching,
with details on tuples, lists, maps, bitstrings, binaries, and of course functions,
then delves into function guards to implement extended pattern matching in functions.

Multi-clause anonymous functions were new to me:

``` elixir
test_num =
          fn
            x when is_number(x) and x < 0 -> :negative
            x when x == 0 -> :zero
            x when is_number(x) and x > 0 -> :positive
          end
```

In Elixir, recursion is efficient.
Nothing is pushed on the stack when the last thing a function does is call another function, or itself.
This is called _tail call optimization_.

## Notable Notes and Quotes

<!--more-->

### Pattern Matching

- Tuple matching of a typical `:ok` vs `:error` response.
- Partial matches to capture only a portion of a function's return value.
- “A variable can be referenced _[matched]_ multiple times in the same pattern.”
- Use the _pin operator_ (`^`) to match against the contents of a variable.
- “Patterns can be arbitrarily nested”
- “match expressions can be chained”, `a = (b = 1 + 3)`
- “the = operator is right-associative”
- “ the result of a pattern match is always the result of the term being matched”
- “If an error is raised from inside the guard, it won’t be propagated, and the guard expression will return false. The corresponding clause won’t match, but some other clause might.”

### Loops and Iterations

- “The principal looping tool in Elixir is _recursion_”
- “Although recursion is the basic building block of any kind of looping, most production Elixir code uses it sparingly. That’s because there are many higher-level abstractions that hide the recursion details.”


### 3.4.2 Practice

My practice code is much like the given examples, with the following exceptions:

1. For the range, I recognized I needed to ensure the `to` and `from` values were in the proper order, but did not think about always generating the list in `from` `to` order so the final `reverse` is unnecessary.

2. I note that the author put the accumulator as the third element of the recursions instead of the first.
I've been putting it first in previous sample code.

On starting Section 3.4.3 I quickly see why last is best as `Enum.reduce` wants the collector as the last parameter.

### Comprehensions

Comprehensions can collect data into a map:

``` elixir
iex(4)> multiplication_table =
          for x <- 1..9,
              y <- 1..9,
              into: %{} do
            {{x, y}, x*y}
          end

iex(5)> Map.get(multiplication_table, {7, 6})
42
```

### Streams

I've mostly relied on the `Enum` vs. the `Stream` module.
Exercises took a bit of working through.
Particularly the `longest_line!` function to return the text of the longest line.
I ended up using `Enum.reduce` and accumulating a map containing the largest line length and the associated line.
Presented solution is much simpler.
As always, knowing the library is as important as knowing the language.

_Quotes are excerpts From [Elixir in Action, Third Edition](https://www.manning.com/books/elixir-in-action-third-edition), Sasa Juric._
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
