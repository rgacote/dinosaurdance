---
title: "Programming Elixir Chapter 13 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-02T01:00:00-05:00
subtitle: "Organizing a Project"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---



1. `mix new` did not create the ./config directory.

1. `elem` accesses a tuple by index.

1. Elixir [builtins](http://elixir-lang.org/docs.html)
1. Erlang [documentation](http://erlang.org/doc/) _Application Group_ sidebar.
1. Elixir [hex](https://hex.pm)

1. Version control the mix.lock for applications. Review when building a public library.

1. Mix.Config is deprecated. Use [Config](https://hexdocs.pm/elixir/1.14.3/Config.html)

1. The configuration sets the minimal log level compiled into the application.
   Code for lower-levels is not even compiled into the application.
   For example, setting it at `:info` means you cannot log `:debug`.

   Set the compile-time logging in issues/config/config.exs:
   {{< highlight elixir >}}
   config :logger,
      compile_time_purge_level: :info
   {{< /highlight >}}

   Already outdated, use:
   {{<highlight elixir >}}
   config :logger,
     compile_time_purge_matching: [
       [lower_level_than: :info]
     ]
   {{< /highlight >}}

1. The string passed to the log function is always evaluated, even if it is never logged.

1. Use the function variant when expensive information may not be logged.
   For example:

   {{< highlight elixir >}}
   Logger.debug fn -> "#{expensive(value)}"
   {{< /highlight >}}

1. The documentation to add `ex_doc` and `earmark` to the `mix.exs` development-only and non-runtime flags:
    {{< highlight elixir >}}
    {:ex_doc, "~> 0.27", only: :dev, runtime: false},
    {:earmark, "~> 1.14", only: :dev, runtime: false},
    {{< /highlight >}}

## Exercises

### OrganizingAProject-1
Copied the project as recommended.

### OrganizingAProject-2
Added dependency as directed.

### OrganizingAProject-3
- Sort of duplicated the code.
- In playing around with the `Poison` module I accidentally used `encode!` instead of `parse!`,
which led me down a rabbit hole of learning how to debug in IEx.

### OrganizingAProject-4
[My Solution](https://github.com/rgacote/ProgrammingElixirExercises/tree/OrganizingAProject-4/issues)
is moderately different from Dave's.
I see where I can improve efficiencies by using map/reduce and doing additional pipelining.

Most importantly, it works!

- Spent a lot of time Googling.
- Wrapping my head around piping and enumeration.
- Testing helps.
- Short snippets in LiveBook helps.
- Practiced documenting.

- Reduce a list of maps into a map:
  {{< highlight elixir >}}
  Enum.reduce(list_of_maps, fn x, y ->
    Map.merge(x, y, fn _k, v1, v2 -> v2 ++ v1 end)
  end)
  {{< /highlight >}}

- Reduce a list of tuples into a map:
  {{< highlight elixir >}}
  Enum.into(list, %{})
  {{< /highlight >}}

### OrganizingAProject-5
[My Solution](https://github.com/rgacote/ProgrammingElixirExercises/tree/main/noaa)
to the NOAA airport weather lookup.

- Needed to add `:httpoison` and `:elixir_xml_to_map` to applications.

_All notes and comments are my own opinion._
