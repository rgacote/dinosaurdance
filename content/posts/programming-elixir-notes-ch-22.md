---
title: "Programming Elixir Chapter 22 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-27T01:00:00-05:00
subtitle: "Macros and Code Evaluation"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

<!--more-->

1. Never use a macro when you could use a function.
   Macros can make your code harder to understand.

1. Macros are useful when you need to delay parameter evaluation.

1. The `require` call ensures a module is compiled before the current one.
   - Watch for circular references!

1. Macro definitions cannot be used in the file in which they are defined.

1. When you define a new function with a macro, you cannot use that function in the same module.

## MacrosAndCodeEvaluation-1
Write a macro called `myunless` that implements the [standard](https://elixir-lang.org/getting-started/case-cond-and-if.html#if-and-unless) `unless` functionality.

{{< highlight elixir >}}
defmodule My do
  @moduledoc """
  My.unless true do
    "Truth"
  else
    "Falsity"
  end
  """
  defmacro unless(condition, clauses) do
    do_clause = Keyword.get(clauses, :do, nil)
    else_clause = Keyword.get(clauses, :else, nil)
    quote do
      case unquote(condition) do
        val when val in [false, nil] -> unquote(else_clause)
        _ -> unquote(do_clause)
      end
    end
  end
end
{{< /highlight >}}

{{< highlight elixir >}}
require My

My.unless 1==1 do
  "hello"
else
  "goodbye"
end
{{< /highlight >}}

## MacrosAndCodeEvaluation-2
Write a macro `times_n`.
{{< highlight elixir >}}
defmodule Times do
  @moduledoc """
  Times.times_n(3) creates a times_3 function.
  """
  defmacro times_n(n) do
    func = String.to_atom("times_#{n}")
    quote do
      def unquote(func)(value), do: value * unquote(n)
    end
  end
end

defmodule Test do
  require Times
  Times.times_n(3)
  Times.times_n(5)
end

IO.puts Test.times_3(4)
{{< /highlight >}}

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
