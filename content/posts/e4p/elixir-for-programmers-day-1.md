---
title: ""
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-07T01:00:00-05:00
subtitle: "Elixir for Programmers, Second Edition"
image: ""
tags: [LearningElixir, Elixir, IEx,ElixirForProgrammers]
---
TODO:
- Review and revise description.
- Figure out why length does not work in a pipe.
- Link to [Our First Project](https://github.com/rgacote/Elixir4Programmers2ndExercises/tree/OurFirstProject)

Separate dictionary project is new to me.
`@`at compile time.

I'm having problems with this:
{{< highlight  elixir >}}
iex(34)> "bobby jones" |> String.split("", trim: true) |> Enum.sort() |> Enum.join()
" bbbejnoosy"
{{< /highlight>}}

From my reading of the documentation, I expect the initial blank to have been removed.
I can't seem to get that to happen.

<!--more-->
## Notes
- Course uses Elixir 1.12.3. I'm using Elixir 1.14.2.
- Set up .iex.exs to match recommendation.
- In IEx:
  - `h IO` shows module-level documentation.
  - `h IO.` shows functions in the module.
- Commandline editing uses EMACS keys.
- `v` evaluates that line number.
  - can be used in expressions:
    ```
    v(1) * 22
    ```
- `iex:break` takes you to top-level of the REPL.
- `mix new xxx` examples not showing a `./config` directory.
   The last book always expected that to be created.
- `mix run -e Dictionary.hello`
- Loading new code:
  - Compile the file: `c "lib/dictionary.ex"`
  - Recompile the module: `r Dictionary`

## Exercises
Bind the string "had we but world enough, and time" to a variable.

Use functions from the String module to:
* Split it into two parts: the stuff before and the stuff after the comma.
* Split it into a list of characters, where each entry in the list is a single character string.
* Split it into a list of characters, where each entry in the list is the integer representation of that character.1
* reverse the string (hmmm... the first two words of the result are interesting)
{{< highlight elixir >}}
iex(1)> world_enough = "had we but world enough, and time"
"had we but world enough, and time"

iex(2)> String.split(world_enough, ~r/,/)
["had we but world enough", " and time"]

# The following could have used String.codepoints.
iex(3)> String.split(world_enough, ~r/.{1}/, include_captures: true, trim: true)
["h", "a", "d", " ", "w", "e", " ", "b", "u", "t", " ", "w", "o", "r", "l", "d",
 " ", "e", "n", "o", "u", "g", "h", ",", " ", "a", "n", "d", " ", "t", "i", "m",
 "e"]

iex(4)> String.to_charlist(world_enough)

iex(5)> String.reverse(world_enough)
"emit dna ,hguone dlrow tub ew dah"

# Does not explicitly state, but I'm assuming this is the Myers Difference.
iex(6)> bacon_enough = "had we but bacon enough, and treacle"
"had we but bacon enough, and treacle"

iex(7)> String.myers_difference(world_enough, bacon_enough)
[
  eq: "had we but ",
  del: "w",
  ins: "bac",
  eq: "o",
  del: "rld",
  ins: "n",
  eq: " enough, and t",
  del: "im",
  ins: "r",
  eq: "e",
  ins: "acle"
]
{{< /highlight >}}

## Review Questions
1. Letters sorted into alphabetical order in "conventional" language.
   {{< highlight  elixir >}}
   # Elixir
   iex(1)> "bobby jones" |> String.codepoints() |> Enum.sort() |> Enum.join()
   " bbbejnoosy"
   {{< /highlight >}}

   {{< highlight python >}}
   # Python
   "".join(sorted([*"bobby jones"]))

2. Some lines of conventional code translated to Elixir.
   {{< highlight  elixir >}}
   # join(sort(split(word)))
    iex(1)> "bobby jones" |> String.codepoints() |> Enum.sort() |> Enum.join()
    " bbbejnoosy"

    # length(split(wordlist, /\n/))
    # Why isn't length working in the pipe? I'm missing something.
    iex(2)> lines = "bobby jones\nsuzie queue" |> String.split("\n")
    iex(3)> length(lines)
    2

    # join(split(string, "\t"), ",")
    iex(4)> "tabbed\twords" |> String.split("\t") |> Enum.join(",")
    "tabbed,words"



   {{< /highlight  >}}

   ' bbbejnoosy'
   {{< /highlight >}}
_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
