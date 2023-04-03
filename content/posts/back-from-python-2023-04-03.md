---
title: "Back to Elixir"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-04-03T01:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Python, ReportLab]
---

I'm ready to get back to Elixir after spending the last few weeks using Python and [ReportLab/RML](https://www.reportlab.com/) to generate multi-thousand line PDF reports.
The project is only about 2/3 finished and currently stalled waiting for client answers.

While coding the Python project I kept trying to think about how I'd approach the work in Elixir (assuming a ReportLab-style package was available).
In order to create a ReportLab/RML report, I first create a (fairly large) blob of data containing information loaded from multiple .csv files and then arranged and summarized multiple ways.

In Python I use multiple classes (a base class contains many attributes that are themselves classes).
Historically, I'd tend to use dictionaries instead of classes, but I also used an IDE (VS Code) for the first time and wanted to get the IDE hints as well as type hint everything.

In Elixir:
<!--more-->
- would I choose map or struct?
- does copying a map through a pipeline get garbage collected before the thread terminates?
  - Looks like [maps point to references](https://elixirforum.com/t/how-elixir-manages-memory/5989) so we're not copying all the data.
- how about copying structs?
- how many of the summary tasks could be split into separate tasks?
- what's the most efficient way to generate new summary lists using parallel maps?

Still lots to learn.


_All notes and comments are my own opinion. Follow me at [@rgacote@genserver.social](https://genserver.social/rgacote)_
