---
title: "Convert SimpleCardBrand To A mix Project"
# subtitle: "and more card brands"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-06T01:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

Added guards to `card_brand` that check for String and Integer parameters then
moved the single file into a [mix project](https://github.com/rgacote/SimpleCardBrand/tree/v0.1.0).

Every card brand now has its own test file.
The tests validate against the information on the [Wikipedia](https://en.wikipedia.org/wiki/Payment_card_number) page.

Each brand is tested for each documented prefix for each documented account number length.

As suspected, there were a few lurking bugs which have now been corrected.

<!--more-->

## Next Steps

1. Run credo for static analysis.

1. Implement git pre-commit tasks.

1. Implement documentation.

1. More brands.

1. Implement failing tests.

1. Publish(?)
