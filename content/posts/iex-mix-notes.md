---
title: "IEx and Mix Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-31T01:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir, IEx, mix, pry, dbg]
---
Further side-quest to become comfortable with IEx/mex/dbg/pry.
Learning commandline debugging since I've not been able to figure out how to launch a debuggable commandline program from VSCode.

## IEx

A quick introduction to IEx functionality: [8 + 1 things...](https://nts.strzibny.name/elixir-interactive-shell-iex/).

{{< highlight bash >}}
# Start and run the mix script:
iex -S mix

# Run specific function
iex -S mix run -e "Issues.CLI.run(['arg1', 'arg2'])"

# Recompile changed mix project files.
recompile
{{< /highlight >}}

## Mix
{{< highlight bash >}}
# Create new project tree
mix new project_name

mix test

# Show dependencies
mix deps

# Fetch dependencies
mix deps.get

# Run Chapter 13 exercise:
mix run -e 'Issues.CLI.run(["rgacote", "ProgrammingElixirExercises"])'

{{< /highlight >}}

# Debugging
1. Use the Elixir `dbg()` statement.
1. IEx drops you into [pry](https://hexdocs.pm/iex/1.13/IEx.Pry.html).

    {{< highlight elixir >}}
    # See variable bindings
    binding()

    # Execution stack
    whereami()

    {{< /highlight >}}

1. Cannot continue after a piped `dbg()` because it returns ``:ok`.

1. Use `break!` from IEx.
    {{< highlight elixir >}}
    break! Issues.CLI.run/1
    {{< /highlight >}}

1. Pry is not a debugger. You can only examine local information.

# Creating a CLI
Builds the commandline interface in the home directory.

1. Add a `main(argv)` function to the CLI module.
1. Add line to mix.exs `def project` section:
    {{< highlight text >}}
    escript: [main_module: Issues.CLI],
    {{< /highlight >}}

1. Build:
    {{< highlight bash >}}
    mix escript.build
    {{< /highlight >}}


_All notes and comments are my own opinion._
