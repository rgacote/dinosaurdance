---
title: "Programming Elixir Chapter 15 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-21T01:00:00-05:00
subtitle: "Working with Multiple Processes"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

1. Elixir/Erlang processes are not operating system processes.

1. Spawn a task within a module by passing the function name as an atom, and parameters.
{{< highlight elixir >}}
   spawn("Sample", :hello, ["Ray"])
{{< /highlight >}}

1. You can spawn an anonymous function.

1. `self` is the current PID.

1. `receive` is a one-time event. Once event is received, the receiver is gone.
   Address this by recursing into yourself.
{{< highlight elixir >}}
  def greet do
    receive do
      {sender, msg} ->
      send sender, { :ok, "Hello, #{msg}"}
      greet()
    end
  end
{{< /highlight >}}

1. Add `after` to receiver to go away after `n` seconds.

1. Multiple `receive` blocks within the same pid all receive the message.

1. `receive` blocks can have guard clauses.

1. Elixir has tail-call optimization __if__ the last thing a function does is call itself.
   This means no calculations in the call parameters, for example.

1. Don't run the 400,000 thread example in LiveBook as you'll need to kill it from the commandline.

1. Process limits can be increased with the `--erl "+P 1000000"` command-line parameter.

1. Processes can be linked together to handle process death, for example.
   Better to use OTP Supervisors for this.

## WorkingWithMultipleProcesses-1
Ran on my machine.

## WorkingWithMultipleProcesses-2
Write a program that spans two processes and then passes each a unique token ("fred" and "betty").
Have them send the tokens back.
- Is the order in which replies are received deterministic in theory? In practice?
- If either answer is no, how would you make it so?

### Answers
- [Source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/WorkingWithMultipleProcesses-2.exs)
- Not deterministic, though in practice I'd be surprised to see them return out of order (surprise is the operant term).
- My understanding is that not being deterministic is a feature.
  I'd possibly go to a queue?

## WorkingWithMultipleProcesses-3

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
