---
title: "Things are Starting to Click!"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-01T01:00:00-05:00
subtitle: "OrganizingAProject-4"
image: ""
tags: [LearningElixir, Elixir, Python]
---

Back in college I struggled with Calculus; had a hard time grasping the concept of the day.
After a semester break, I'd ace the test reviewing previous topics.
Just took awhile for the concepts to settle into my brain.

I'm experiencing a similar effect with Elixir.
Came back after a few days and was able to make significant progress on Chapter 13's _Formatting a Table_ exercise.

Things are starting to click.

1. There's always a function for it.
   * Use `[element | _]`, not `list[0]`.
   * Use `Map.fetch(map, key)`, not `map["key"]`.
   * Use `elem(tuple, 0)`, not `tuple[0]`

1. Every block is a local scope.
   {{< highlight elixir >}}
   # Doesn't work
   row = []
   for header <- headers do
     row = [function(data) | row]
   end
   # row is still []

   # Works
   row = for header <- headers do
     function(data)
   end
   {{< /highlight >}}

1. Enum.map and Enum.zip are your friends.

1. `dbg` and `Next`, though limited, are invaluable.

1. Breakpoints are set by arity.

1. Tests are easier to write on small functions.
   In Python I'd end up building more complex functions as it felt reasonable to do 'one more thing' in a function.
   Smaller functions feel natural in Elixir.

