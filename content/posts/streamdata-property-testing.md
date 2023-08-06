---
title: "StreamData Property Testing"
subtitle: "Parameterized tests"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-08-06T03:00:00-05:00
image: ""
tags: [LearningElixir, Elixir, SimpleCardBrand]
#LearningElixir #Elixir #SimpleCardBrand
---

I was recently lamenting Elixir's lack of Pytest-like parameterized testing
(or at least my inability to find such).

I'd found several examples including [ExUnit.Parameterized](https://hexdocs.pm/ex_parameterized/ExUnit.Parameterized.html),
but I could not find a solution that output the actual parameters from among hundreds that caused the failed assert.

Maciej Lukksepp (`icejam_@hachyderm.io`) responded that [StreamData](https://github.com/whatyouhide/stream_data
) property testing should solve the problem, and provided a useful starting point.

<!--more-->

An example test for JCB card brand using StreamData property tests:

```elixir
defmodule SimpleCardBrandJCB do
  @moduledoc """
  JCB tests.
  """

  use ExUnit.Case, async: true
  use ExUnitProperties

  property "JCB" do
    check all(
            fragment <- StreamData.integer(3528..3589),
            pan_length <- StreamData.integer(16..19)
          ) do
      assert SimpleCardBrand.card_brand(Integer.to_string(fragment), pan_length) == {:ok, :jcb}
    end
  end
end
```

Which provides an explicit description of an error:
```text
➜  simplecardbrand git:(main) ✗ mix test
.......

  1) property JCB (SimpleCardBrandJCB)
     test/jcb_test.exs:9
     Failed with generated values (after 6 successful runs):

         * Clause:    fragment <- StreamData.integer(3528..3589)
           Generated: 3530

         * Clause:    pan_length <- StreamData.integer(16..19)
           Generated: 16

     Assertion with == failed
     code:  assert SimpleCardBrand.card_brand(Integer.to_string(fragment), pan_length) == {:ok, :jcb}
     left:  {:ok, :rupay}
     right: {:ok, :jcb}
     stacktrace:
       test/jcb_test.exs:14: anonymous fn/3 in SimpleCardBrandJCB."property JCB"/1
       (stream_data 0.6.0) lib/stream_data.ex:2367: StreamData.shrink_failure/6
       (stream_data 0.6.0) lib/stream_data.ex:2327: StreamData.check_all/7
       test/jcb_test.exs:10: (test)

......................................
Finished in 0.1 seconds (0.1s async, 0.00s sync)
8 doctests, 1 property, 37 tests, 1 failure

```

Thanks Maciej.
