---
title: "Programming Elixir Chapter 20 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-22T01:00:00-05:00
subtitle: "OTP: Applications"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

Ran into significant issues between outdated `Distillery` information and incompatibility with `OTP 25`.

<!--more-->

1. Need to use the `~S` sigil when writing a DocTest for the `Stack.Stash.update` function
because I need to maintain state across two statements.

    {{< highlight elixir >}}
    @doc ~S"""
    Replace the current stashed value with new stack.

    ## Examples
      iex> Stack.Stash.update([42,24])
      ...> Stack.Stash.get()
      [42, 24]
    """
    {{< /highlight >}}

    Without the sigil, `Stack.Stash.get()` returns `[1, 2, 3]` and the test fails.
    With the sigil, we get the expected `[42, 24]` returned.
    This is not mentioned in the ExUnit documentation.

## Releasing
The book is significantly out of date.
Refer to the online [documentation](https://hexdocs.pm/distillery/home.html).

1. Install [Distillery](https://hex.pm/packages/distillery).

1. Create release information in the `./rel` directory:
    {{< highlight bash >}}
    mix distillery.init
    {{< /highlight >}}

1. Make release configuration changes if necessary.
   No changes necessary for our build.

1. Create a release:
    {{< highlight bash >}}
    # Development
    mix distillery.release

    # Production
    MIX_ENV=prod mix distillery.release
    {{< /highlight >}}

1. Production release fails with latest OTP 25.
   A [known problem](https://github.com/bitwalker/distillery/issues/744) being addressed.

## OTP-Applications-1
Turn the stack server into an OTP application.
[Source](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Applications-1/stack)

## OTP-Applications-2
Wrote DocTests for Stack.Impl and Stack.Stash.
[Source](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Applications-2/stack)

## OTP-Applications-3
Package the release and make a change to the sequence application.
[Source](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Applications-3/stack) for my stack application.

I've not been keeping the sequence application up to date so skipped the versioning wo[Source](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Applications-3/stack)

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
