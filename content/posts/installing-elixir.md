---
title: "Installing Elixir on Mac OS"
author: "ray@AppropriateSolutions.com"
type: ""
date: 2023-01-03T01:00:00-05:00
subtitle: ""
image: ""
tags: [LearningElixir, Elixir]
---

Soon as I hit [Programming Elixir](https://pragprog.com/titles/elixir16/programming-elixir-1-6/)
Chapter 5 I found I needed to start testing some of the concepts.

You can install [Livebook](https://livebook.dev/#install) or install the command line environments.

Here's how I installed Elixir on my Mac OS 13.1 (Ventura) environment.

1) Install [Xcode Command Line Tools](https://mac.install.guide/commandlinetools/4.html)
1) Install [Homebrew](https://brew.sh/)

1) Install [asdf](https://asdf-vm.com/):
   {{< highlight bash >}}
   brew install asdf
   # Apache Formatting Objects Processor for PDF generation.
   brew install fop
   {{< /highlight >}}

1) Add asdf.sh to the zshrc configuration file.
   {{< highlight bash >}}
   echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ${ZDOTDIR:-~}/.zshrc
   {{< /highlight >}}

1) Exit and restart terminal.

1) Install Erlang and Elixir plugins.
   {{< highlight bash >}}
   asdf plugin-add erlang
   asdf plugin-add elixir
   {{< /highlight >}}

1) Get list of available Erlang/OTP and Elixir versions.
   {{< highlight bash >}}
   asdf list-all erlang
   asdf list-all elixir
   {{< /highlight >}}

1) Check the Elixir/Erlang [compatibility chart](https://hexdocs.pm/elixir/compatibility-and-deprecations.html#compatibility-between-elixir-and-erlang-otp)
to determine which versions to install.
   Erlang versions are listed as OTP versions.

1) Install the latest (2023-01-02) versions.
   Grab a cup of tea as the Erlang build takes some time.
   {{< highlight bash >}}
   asdf install erlang 25.2
   asdf install elixir 1.14.2-otp-25
   {{< /highlight >}}

   * Erlang generates warnings about jinterface and odbc being disabled.
     Neither are required at this time.

1) Install Erlang/OTP and Elixir versions globally while learning.
   {{< highlight bash >}}
   asdf global erlang 25.2
   asdf global elixir 1.14.2-otp-25
   {{< /highlight >}}

1) Test by starting IEx:
   {{< highlight bash >}}
   iex
   ```

_All notes and comments are my own opinion._
