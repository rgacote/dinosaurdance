---
title: "Things I'm starting to Get!"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-01T01:00:00-05:00
subtitle: "OrganizingAProject-4"
image: ""
tags: [LearningElixir, Elixir, Python]
---

1. There's always a function for it.
   * Use `[element | _]`, not `list[0]`.
   * Use `Map.fetch(map, key)`, not `map["key"]`.
   * Use `elem(tuple, 0)`, not `tuple[0]`

1. Every block is a local scope.
   ```
   # Doesn't work
   row = []
   for header <- headers do
     row = [function(data) | row]
   end

   # Works
   row = for header <- headers do
     [function(data)]
   end

   ```

1. Enum.map and Enum.zip are your friends.

1. `dbg` and `Next`, though limited, are invaluable.

1. Breakpoints are set by arity.

1. Tests are easier to write on small functions.
   In Python I'd usually build more complex functions.
   Smaller functions feel more natural in Elixir.

