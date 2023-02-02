---
title: "Programming Elixir Chapter 5 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-05T01:00:00-05:00
subtitle: "Anonymous Functions"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

1) Unlike Python lambda functions, Elixir anonymous functions can be arbitrarily complex
(though I guess there is a limit to what is practicable from a maintainability point of view).

2) Anonymous functions are basic types and can be bound to a variable.

3) Named functions are scoped to a module, anonymous functions are not.
Still trying to fully understand this scoping.

4) Anonymous functions remember the values of variables in the outer scope.
This can be both powerful and confusing.


4) The three-value FizzBuzz task was such fun that I looked ahead a little and did a more traditional FizzBuzz example.
    {{< highlight elixir >}}
    fizzbuzz = fn
      value when rem(value, 3) == 0 and rem(value, 5) == 0 -> "FizzBuzz"
      value when rem(value, 3) == 0 -> "Fizz"
      value when rem(value, 5) == 0 -> "Buzz"
      value -> value
    end

    for x <- Enum.to_list(1..100) do
      fizzbuzz.(x)
    end

    [1, 2, "Fizz", 4, "Buzz", "Fizz", 7, 8, "Fizz", "Buzz", 11, "Fizz", 13, 14, "FizzBuzz", 16, 17,
    "Fizz", 19, "Buzz", "Fizz", 22, 23, "Fizz", "Buzz", 26, "Fizz", 28, 29, "FizzBuzz", 31, 32, "Fizz",
    34, "Buzz", "Fizz", 37, 38, "Fizz", "Buzz", 41, "Fizz", 43, 44, "FizzBuzz", 46, 47, "Fizz", 49,
    "Buzz", ...]

    {{< /highlight >}}

1) `_ -> value` does not work in the above FizzBuzz since the passed parameter is not captured.
   `_ -> "Hello"` would work since we arent' using the passed parameter.

5) It is going to take my Python fingers some time to stop typing `for x in`.

6) In the Greeter example, if you want the output, "I don't know you Dave", you need to match on `name` vs. `_`.
   `_`, `^varname`, and `varname` in an anonymous function match statement match anything, the original value of the varname, and the varname.

7) The `&` shortcut to anonymous functions reminds me of the Python lambda function.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
