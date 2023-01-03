---
title: "Programming Elixir Ch 5-X Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-10T01:10:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook, Python]
---

1) Unlike Python lambda functions, Elixir anonymous functions can be arbitrarily complex
(though I guess there is a limit to what is practicable from a maintainability point of view).

2) Anonymous functions are basic types and can be bound to a variable.

3) Named functions are scoped to a module, anonymous functions are not.
Still trying to fully understand this scoping.

4) The three-value FizzBuzz task was such fun that I did a more traditional FizzBuzz example.
I think this can be simplified.
    ```
    fizzbuzz = fn (value) ->
      cond do
        rem(value, 3) == 0 and rem(value, 5) == 0 -> "FizzBuzz"
        rem(value, 3) == 0 -> "Fizz"
        rem(value, 5) == 0 -> "Buzz"
        true -> value
      end
    end

    for x <- Enum.to_list(1..100) do
      fizzbuzz.(x)
    end

    [1, 2, "Fizz", 4, "Buzz", "Fizz", 7, 8, "Fizz", "Buzz", 11, "Fizz", 13, 14, "FizzBuzz", 16, 17,
    "Fizz", 19, "Buzz", "Fizz", 22, 23, "Fizz", "Buzz", 26, "Fizz", 28, 29, "FizzBuzz", 31, 32, "Fizz",
    34, "Buzz", "Fizz", 37, 38, "Fizz", "Buzz", 41, "Fizz", 43, 44, "FizzBuzz", 46, 47, "Fizz", 49,
    "Buzz", ...]
    ```

5) In the Greeter example, if you want the output, "I don't know you Dave", you need to match on `name` vs. `_`.

6) Lists and tuples can be turned into functions.
   ```
   divrem = &{ div(&1,%2), rem($1,$2)}
   ```


