---
title: "Reaching a Complexity Limit"
subtitle: "and more card brands"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-05T01:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

After [adding](https://github.com/rgacote/SimpleCardBrand/blob/v0.0.3/SimpleCardBrand.exs)
16 new card brands, I'm finding the single file is getting slightly more complex than I'd like.

There's only about 270 lines of code, but it's difficult to come up with logical arrangement
as many brands have multiple ranges in entirely different areas.

<!--more-->

An approach I'm considering creating a set of `cb_1` thru `cb_9` submodules
and move the logic for each leading digit into the submodule.

Of course, this is not practicable without a proper Mix project, so that's the next major step.

I'll also be introducing tests at that point as I'm not comfortable I've not broken some earlier brands.

## New Card Brands

China UnionPay, China T-Union, Diners Club, Diners Club International,
JCB, Maestro, Maestro UK, Visa Electron,
BORICA, Humo, InstaPayment, InterPayment, Mir, Napas, UATP, UzCard


## Next Steps

1. Add guards to `card_brand` to check for String and Integer.

1. Proper Mix project (including tests).

1. More brands.

1. Publish(?)

_Yes, I changed SimpleCardBin to SimpleCardBrand, much better name._

