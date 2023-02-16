---
title: "Programming Elixir Chapter 17 Notes"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-16T01:00:00-05:00
subtitle: "OTP: Servers"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

Dave discusses an alternate _component-based_ approach to writing GenServers.
This consists of modules in three files:
- A public API to hide the GenServer complexity.
- The GenServer interface.
- Implementatation.

The public API is just a wrapper to the GenServer functions and the
GenServer functions are just a wrapper to the implementation.
This hides the GenServer call/cast complexity and isolates the implementation.

I like this approach, but think that breaking it into three files is too complex.
If the public API is only a wrapper to the GenServer API and the GenServer API is only
 a wrapper to the implementation, we can easily put them into a single file.

My [approach](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Server-4a/otpservers)
implements the GenServer in two files:
- Public API which calls the GenServer functions.
- Implementation


<!--more-->

_Update 2023-02-16: I'm generally working a bit beyond my postings.
In retrospect, I should have broken the public API and the GenServer interface
into two modules, and kept them in the same file. I may have focused too much on the author
breaking the modules into separate files. Keeping these initial thoughts to reflect my
thinking at the time._

1. An OTP server (GenServer) is a module containing one or more callbacks functions with standard names.

1. Handler functions get passed the current state and return a potentially updated state.

1. The `handle_call` function pattern matches on the message.

1. Use a tuple to one of several identifiers to a server function.

1. Use `debug_trace` to log message activity.
   {{< highlight elixir >}}
   GenServer.start_link(..., [debug: [:trace]])
   {{< /highlight >}}

1. `:statistics` is another useful debug option. Display them as follows:
   {{< highlight elixir >}}
   :sys.statistics pid, :get
   {{< /highlight >}}



## OTP-Servers-1
[Source code](https://github.com/rgacote/ProgrammingElixirExercises/releases/tag/OTP-Servers-01) to create a server that implements a stack and pop.

## OTP-Servers-2
[Source code](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Server-02/otpservers) to implement pop.
Return `nil` when the stack is empty.

## OTP-Servers-3 and OTP-Servers-4
[Source code](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Server-04/otpservers)
to name the server and implement the API in the same file.

[Source code](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Server-4a/otpservers)
for alternate solution with implementation separated out.
I like this approach when the module is complex.

# OTP-Servers-5
[Source code](https://github.com/rgacote/ProgrammingElixirExercises/tree/OTP-Server-05/otpservers) to implement `terminate` callback.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
