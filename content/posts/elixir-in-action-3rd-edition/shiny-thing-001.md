---
title: "Shiny Thing #001: Macros"
subtitle: "Wherein I'm distracted by Saša Jurić's 2014 Erlangelist Series"
author: "ray.cote@mac.com"
type: ""
date: 2024-09-08T00:01:00-05:00
image: ""
tags: [LearningElixir, Elixir, ElixirInAction]
---

Spent the week reading through Saša Jurić's six-part _Understanding macros_ on [The Erlangelist](https://www.theerlangelist.com/).
I've previously managed to wend my way through a macro in one of the _Programming Elixir_ exercises but didn't really get a handle on it.
Saša's explanation of `quote` and `unquote` was clear and understandable.

## Notable Notes and Quotes

<!--more-->

- "_[Macros keep]_ the language core minimal, and simplifies further extensions to the language."
- "somewhat less known is the possibility to generate functions on the fly"
- "Another way of looking at unquote is to treat it as an analogue to string interpolation (`#{}`)."
- "variables introduced by a macro are its own private affair that won’t interfere with the rest of the code."
- Use the `var!` construct to make a variable visible outside the macro.
- "the `use` mechanism allows us to inject some piece of code into the caller’s context."
- "`use` generates a code that generates a code"
- "proliferation of macros may make your client code extremly cryptic, since it will rely on custom, non-standard idioms"
- "since they run during compilation, macros make it possible to optimize some code by moving calculations to compile-time"
- "Always remember - macros amount to plain composition of AST fragments during expansion phase"

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
