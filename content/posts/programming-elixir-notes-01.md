---
title: "Programming Elixir Ch 1-4 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-02T10:24:30-05:00
subtitle: "Interesting and/or Unfamiliar"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python, Forth]
---

I'm used to skimming technical books.
The decision to make notes and document my learning experience is causing me to
slow down and spend more time with what I'm reading.

1) The caret (`^`) _pins_ a variable's value in a match:
    ```
    a = 1
    1
    a = 2
    2
    ^a = 3
    (Error)
    ```

2) What if 99 suddenly became 100?
I once defined 2 as 0 in Forth to make a point.

3) Regular expressions are [PCRE](https://www.pcre.org/).

4) Opening a file returns a reference to a process (PID), not a file handle.
Makes sense after I stare at it for awhile.
_Something_ needs to be reading the file and it is not 'my' current process.

    The first truly foreign concept to me yet it quickly makes complete sense.

    A fundamental step towards understanding how concurrency is built into the bones of Elixir/Erlang.

5) Map (dictionary in Python) keys can be arbitrarily complex values, including expressions.

6) Think of ``%{ "bob" => 3}`` as bob _maps to_ 3.

7) Use an underscore (`_`) if a value is not going to be matched.
Use a variable with a leading underscore (`_var_name`) if it might not be matched.

8) Distinguish between `==` value equality and `===` strict equality.
    ```
    1 == 1.0  # True
    1 === 1.0 # False
    ```

    This is different than the Python `==` operator that is true if two variables point to the same object in memory.

9) The preferred way to set a variable to one of several values is to evaluate and assign vs. assign, and assign.
Example from the book:
    ```
    # No
    case integer do
      1 -> atom = :one
      2 -> atom = :two
    end

    # Yes
    atom =
      case integer do
        1 -> :one
        2 -> :two
      end
    ```
