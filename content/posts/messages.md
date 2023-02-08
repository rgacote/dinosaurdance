---
title: "Message Ordering"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-08T01:00:00-05:00
subtitle: "Some side reading"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

The Erlang blog post, _[A few notes on message passing](https://www.erlang.org/blog/message-passing/)_,
describes how interprocess message passing works.

The most important takeaway for me is that messages have a [defined order](https://www.erlang.org/doc/apps/erts/communication.html#passing-of-signals).

<!--more-->

Messages sent from one process to another appear in the order in which the messages are sent.
This allows us to know that when we receive the 'DOWN' message, that all messages sent by the process have been received.

This guaranteed message ordering is only for message passing from one single process to another.
Messages sent from multiple processes do not have a guaranteed delivery order.
Likewise, messages sent from one process to multiple processes do not have a guaranteed delivery order.


_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
