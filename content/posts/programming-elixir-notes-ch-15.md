---
title: "Programming Elixir Chapter 15 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-07T01:00:00-05:00
subtitle: "Working with Multiple Processes"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

Elixir/Erlang processes are not operating system processes.

<!--more-->

1. Spawn a task within a module by passing the function name as an atom, and parameters.
{{< highlight elixir >}}
   spawn("Sample", :hello, ["Ray"])
{{< /highlight >}}

1. You can spawn an anonymous function.

1. `self()` returns the current PID.

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

1. Add `after` to a receiver to go away after `n` seconds of inactivity.

1. Multiple `receive` blocks within the same pid all receive the messages.

1. `receive` blocks can have guard clauses.

1. Elixir has tail-call optimization __if__ the last thing a function does is call itself.
   This means no calculations in the call parameters, for example.

1. Don't run the 400,000 thread example in LiveBook as you'll need to kill it from the commandline.

1. Process limits can be increased with the `--erl "+P 1000000"` command-line parameter.

1. Processes can be linked together to handle process death, for example.
   Better to use OTP Supervisors for this.

1. Elixir docs note you should usually use `spawn_link` and not `spawn`.
   `spawn_link` connects child to parent in way I don't yet fully understand.
   Initial understanding is that backtraces (exits and exceptions) show parent in the backtrace.

1. `spawn_monitor` is more understandable to me.
   The parent receives exit message from the child.
   Tried working through how to catch exceptions but have not gotten the pattern matching right yet.

1. The _Parallel Map_ section answers the question of how to receive messages in order.
   Use the original pid (`^pid`) in the map.
   - Also shows how the messages hang around even when you're not listening.
     This is listening, in order, for messages from a specific PID.

1. Tested this by rewriting the spawned anonymous function to sleep a random amount of time
    {{< highlight elixir >}}
    Parallel.pmap 1..10, fn(number) ->
      random_seconds = Enum.random(0..10) * 1000
      IO.puts("#{random_seconds}")
      :timer.sleep(random_seconds)
    number * number
    end
    {{< /highlight >}}

1. Actors wrap processes with state.

## WorkingWithMultipleProcesses-1
Ran on my machine.

## WorkingWithMultipleProcesses-2
Write a program that spans two processes and then passes each a unique token (:fred and :betty).
Have them send the tokens back.
- Is the order in which replies are received deterministic in theory? In practice?
- If either answer is no, how would you make it so?

### Answers
- [Source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/WorkingWithMultipleProcesses-2.exs)
- Not deterministic, though in practice I'd be surprised to see them return out of order (surprise is the operant term).
- My understanding is that not being deterministic is a feature.
  I'd possibly go to a queue?
  - Further reading, look for the responses by `^pid`, in order.

## WorkingWithMultipleProcesses-3
Use `spawn_link` to start a process.
Have that process send a message to the parent and exit immediately.
Have parent sleep for 1000ms then receive as many messages as are waiting.

### Answers
- [Source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/WorkingWithMultipleProcesses-3.exs)
- Do not need to be waiting for messages before they are sent.
- Not sure how to do the tracing as all the examples I find are for within a mix environment and not an isolated script.

## WorkingWithMultipleProcesses-4
Do the same, but have the child raise an exception.
What differences to you see?

### Answers
- Stack traces are different.

## WorkingWithMultipleProcesses-5
Change `spawn_link` to `spawn_monitor`.

## Answers
- [Source code](https://github.com/rgacote/ProgrammingElixirExercises/blob/main/WorkingWithMultipleProcesses-5.exs)
- Was able to catch the exit.
- Need to figure out how to catch exceptions.

## WorkingWithMultipleProcesses-6
Why assign `self()` to `me` in the `Parallel` example?

### Answers
- Spawning occurs before function executes.
- The `self()` in the anonymous function is the pid of the spawned function.

## WorkingWithMultipleProcesses-7
Change `^pid` (and `pid`) to `_pid`.
Any difference in output.

### Answers
- No.
- Yes, when I add the random sleep.
- A nice little race condition.

## WorkingWithMultipleProcesses-8
Ran and played with several variations of the Fibonacci code.

## WorkingWithMultipleProcesses-9
- Punted on this exercise as I realize I'm likely to use GenServer in any production code.
- After just writing the above, I read an article warning against the [overuse](https://learn-elixir.dev/blogs/dangers-of-genservers) of GenServers.
  The caution is that GenServers become a bottlenecks because they handle one process message at a time.
  My comment about using GenServer for this exercise stands, because it would be feeding one
  filename at a time to multiple processes.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
