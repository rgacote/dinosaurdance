---
title: "Streaming Lists"
subtitle: "StreamData Property Testing"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-06T19:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand, StreamData, Testing]
#LearningElixir #Elixir #SimpleCardBrand
---

Use an Enum function to stream data from a list.

<!--more-->

```elixir
  property "RuPay" do
    check all(fragment <- StreamData.member_of(Enum.take([60, 81, 82, 508, 353, 356], 6))) do
      assert SimpleCardBrand.card_brand(Integer.to_string(fragment), 16) == {:ok, :rupay}
    end
  end
```
