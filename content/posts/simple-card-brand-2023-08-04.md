---
title: "SimpleCardBrand"
subtitle: "Macros already?"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-04T01:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

The [first code](https://github.com/rgacote/SimpleCardBrand/blob/v0.0.2/SimpleCardBrand.exs)
runs nicely as a Livebook (v0.10.0) page.
It recognizes American Express, Discover, Mastercard, and Visa payment card account numbers (PANs).

After being away from Elixir for a few weeks I thought it would take awhile to get back into the functional mindset,
but I found it took less than an hour to start writing reasonable (I hope) code.

<!--more-->

1. Pattern matching drives everything.
It accounts for well over 90% of the code.
A significant departure from the implementations I've done in Python, Go, Javascript, Delphi, Visual Basic, etc.
I thought less about algorithms and more about the shape of the data.

1. The first step converts the string (PAN) into a list.
I started by using String matching to distinguish card brands but found that approach led to more String handling in the private functions.
Doing the conversion up front led to some wordy pattern matches, but less code.

1. I'm amused to have already written a `defguard` macro.
I've considered macros a fairly advanced topic and have just skimmed those chapters.

    The macro simplified an otherwise wordy guard.

## Next Steps

1. Change the `pan_range` parameter order to put `pan_length` first.

1. Add guards to `card_brand` to check for String and Integer.

1. Add China UnionPay, Diners, JCB, Maestro, and Visa Electron.

1. Package structure.

1. Tests.

1. Publish(?)

_Yes, I changed SimpleCardBin to SimpleCardBrand, much better name._

