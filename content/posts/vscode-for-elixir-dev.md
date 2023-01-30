---
title: "Setting up VSCode for Elixir Development"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-30T01:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir, VSCode]
---

Setting up a VSCode environment before tackling the Chapter 13 exercises.

A side-foray into tooling after being away for a few days.



## Basic Installation
- [Basic Installation](https://code.visualstudio.com/docs/setup/mac) from Microsoft.
- Fly.io recommended [configuration](https://fly.io/phoenix-files/setup-vscode-for-elixir-development/).
- Thinking Elixir [quick start](https://thinkingelixir.com/elixir-in-vs-code/) and troubleshooting.

## Useful videos:
- Quick ElixirLS highlights [tour](https://www.youtube.com/watch?v=IudRI7SlULg).

## Notes
- If VSCode Intellisense stops,
  1. Close VSCode
  1. `rm -rf .elixir_ls` from project directory.
  1. Restart VSCode and wait for ElixirLS to run.
- There was apparently a fork of ElixirLS which has now un-forked.
  Use the one in the VSCode [marketplace](https://marketplace.visualstudio.com/items?itemName=JakeBecker.elixir-ls).

## User settings.json

{{< highlight json >}}

{
    "editor.formatOnSave": true,

    "emmet.includeLanguages": {
        "phoenix-heex": "html"
    },

    "tailwindCSS.includeLanguages": {
        "elixir": "html",
        "phoenix-heex": "html"
    }
}
{{< /highlight >}}

_All notes and comments are my own opinion._
