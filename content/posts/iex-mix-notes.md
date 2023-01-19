---
title: "IEx and Mix Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-19T01:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir]
---

## IEx
{{< highlight bash >}}
# Start and run the mix script:
iex -S mix

# Reload a file:
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

# Creating a CLI
Builds the commandline interface in the home directory.

1. Add a `main(argv)` function to the CLI module.
1. Add line to mix.exs `def project` section:
    ```
    escript: [main_module: Issues.CLI],
    ```
1. Build:
    ```
    mix escript.build
    ```


_All notes and comments are my own opinion._
