---
title: "Programming Elixir Chapter 14 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-03T01:00:00-05:00
subtitle: "Tooling"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

## Debugging
1. Use the new `dbg` instead of the `IEx.pry` as shown to trigger a debug.

1. You can only `break!` on public functions.

1. You also can only `next` on public functions.

1. Dave's note is that he tends to raise an Exception to see what's going on when he's debugging.

## Testing
1. I've been annoyed that VSCode's does code hinting in comments.
   Now I see why, DocTest.

1. Adding DocTest to the TableFormatter caused me to change `print_header` and `print_separator`
   to `table_header` and `table_separator` and print after call.
   Further promotes the 'do one thing' idiom and simplifies testing.

1. I can see doing regular DocTests.

1. DocTests are good for demonstrating usage and do not replace UnitTests.

1. Added some fixtures to TableFormatter tests.
   Had been using `@values`.

1. `fixture` is just a name, could be anything, but `fixture` is descriptive.

1. `setup` can declare a tuple or a function returning a tuple.

1. Add an `on_exit` section to the `setup` block to do any cleanup.

1. Will need to read [ExUnitProperties](https://hexdocs.pm/stream_data/ExUnitProperties.html)
   and dig into examples.

1. Added [ExCoveralls](https://hex.pm/packages/excoveralls) to `issues` project.

## Code Dependencies
{{< highlight bash >}}
mix xref unreachable
mix xref warnings
mix xref callers [Module or function]

mix xref graph --format dot
dot -Grankdir=LR -Epenwidth=2 -Tpng -Ecolor=#a0a0a0 -o xref_graph.png xref_graph.dot
{{< /highlight >}}

## Server Monitoring
{{< highlight elixir >}}
iex> :observer.start()
{{< /highlight >}}

## Source Code Formatting
I'm letting the IDE do the work.

{{< highlight bash >}}
mix format
{{< /highlight >}}
