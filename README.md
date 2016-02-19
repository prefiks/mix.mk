# mix.mk

A plugins for [erlang.mk](http://erlang.mk) to generate a compatible [mix.exs](http://elixir-lang.org/docs/stable/mix/Mix.html) file. 

The command `make mix.exs` will generate the Mix file

## Example

```makefile
PROJECT = test

DEP_PLUGINS = mix.mk
BUILD_DEPS = mix.mk
ELIXIR_VERSION = ~> 1.2

dep_mix.mk = git https://github.com/botsunit/mix.mk.git master

DEPS = lager erlydtl
dep_lager = git https://github.com/basho/lager.git master
dep_erlydtl = git https://github.com/erlydtl/erlydtl.git master

include erlang.mk
```

`make mix.exs` will generate :

```elixir
defmodule Test.Mixfile do
  use Mix.Project

  def project do
    [app: :test,
     version: "0.0.1",
     elixir: "~> 1.2",
     build_embedded: Mix.env == :prod,
     start_permanent: Mix.env == :prod,
     deps: deps]
  end

  def application do
    [applications: [:lager], mod: {:test_app, []}]
  end

  defp deps do
    [ 
      {:lager, ~r/.*/, git: "https://github.com/basho/lager.git", branch: "master"},
      {:erlydtl, ~r/.*/, git: "https://github.com/erlydtl/erlydtl.git", branch: "master"},  
    ]
  end
end
```

## Licence

Copyright (c) 2016, Bots Unit<br />
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
1. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.


THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


