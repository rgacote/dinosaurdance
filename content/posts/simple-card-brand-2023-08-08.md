---
title: "Better Error Reasons"
subtitle: "Dropping Work in Progress"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-07T01:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

[SimpleCardBrand version 0.3.0](https://github.com/rgacote/SimpleCardBrand/tree/0.3.0)
changes the :error reason from a String.t to a tuple: {:atom, String.t}.
This allows simple programmatic decision making based off the atom along with detailed error messages.
Example:

```elixir
{:error, {:pan_too_short,"Minimum PAN length is 12, found 10."}}
{:error, {:pan_unknown,"Unknown card brand."}}
{:error, {:pan_too_long, "Maximum PAN length is 19, found 20."}}
```

Added a (**NOT PCI COMPLIANT**) command-line interface.
Use only with test credit card account numbers.

```bash
$ ./simplecardbrand 4111111111111111
PAN: 4111111111111111 -> Brand: visa
```

<!--more-->

Dropped the "Work in Progress" flag after adding:

- README.md and CHANGELOG.md to the Hex documentation
- pre-commit tasks


## Next Steps

1. Add CLI for `card_brand/2`.

1. GitHub CI.

1. Publish.
