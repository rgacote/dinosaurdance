---
title: "Actors"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-02-06T01:00:00-05:00
subtitle: "It's About Time"
image: ""
tags: [LearningElixir, Elixir, ProgrammingElixirBook]
---

For me, the lure of Elixir is Actors.

<!--more-->

When I first learned of Object Oriented Programming (OOP) my reading quickly
lead me to [Smalltalk](https://en.wikipedia.org/wiki/History_of_the_Actor_model#Smalltalk)
and then to [Simula](https://en.wikipedia.org/wiki/History_of_the_Actor_model#Simula).

At the time, I was professionally buried in large assembly language and C projects
(and, so help me, Forth).
Reading about Smalltalk and Simula formed my understanding of OOP.
In my mind, a program could be built of simple little objects all chatting with each other.
Each of these little objects ran independently and asynchronously.

Seymour Papert described this model as a "little person."
Two other terms I've seen are homunculus and kobito (Japanese for child).

Add to my book learning the release of [BeOS](https://en.wikipedia.org/wiki/BeOS) in 1995.
BeOS was designed from the ground up to provide multitasking and multiprocessing.
In my mind, these two concepts were a match.

Imagine my surprise when I attended [OOPSLA 2022](http://www.oopsla.org/2002/) in Seattle Washington
and found that hardly any of the talks and workshops had anything to do with the Actor model.

Instead, the topics were:
- Data storage
- Multi-platform objects
- Aspect Oriented Software
- Agile/Extreme Programming
- C#, Java, and comparisons
- CORBA, etc.

There was one workshop on [Agent-oriented methodologies](http://www.oopsla.org/2002/fp/files/wor-14.html)
which was Actor-like.
The [workshop summary](http://www.oopsla.org/2002/fp/files/wor-14.html) stated,
"Following the success of object technology, the next advance is likely to be the introduction...agent technology for business applications."
(Interestingly, there were several sessions, including a two-day panel session, discussing how OOP had failed.)

Next advance? I thought it was already here.

Both I and a co-worker left OOPSLA disheartened.
This was not why we had come.

Eventually, I started using ObjectPascal/Delphi and eventually Python OOP, C++, C#, etc.,
which left me wanting something better.

Elixir on BEAM is the mature Actor model for which I've been looking __and__ it has Agents, which are Actors with memory.

_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
