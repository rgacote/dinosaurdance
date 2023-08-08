---
title: "SimpleCardBrand is Feature Complete"
subtitle: "(I think)"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-07T01:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

[SimpleCardBrand](https://github.com/rgacote/SimpleCardBrand/tree/0.2.0) is feature complete.

It supports all the card brands documented on [Wikipedia](https://en.wikipedia.org/wiki/Payment_card_number) as of 2023-08-06.


<!--more-->

Along the way I've:

- Implemented testing
  - Learned about [StreamData Property Testing](https://rgacote.github.io/dinosaurdance/posts/streamdata-property-testing/)
- Corrected a few minor, and one major, bug.
- Generated Hex documentation.
- Delved a bit into the Kernel module while writing `defguard` guard functions.
- Made new friends.

## Next Steps

I'd like to remove the "Work in Progress" warning from the next release,
and I've decided this is clean enough and useful enough to publish.

There's still a few items to complete:

1. Improve error responses.

1. Improve documentation.

1. Implement git pre-commit tasks.

1. Further testing.

1. Publish.
