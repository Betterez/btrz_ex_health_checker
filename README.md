# BtrzHealthchecker

[![Build status badge](https://img.shields.io/circleci/project/github/Betterez/btrz_ex_health_checker/master.svg)](https://circleci.com/gh/Betterez/btrz_ex_health_checker/tree/master)

Health checker gets the information for the desired services passed as Checkers in addition to environment information.

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `btrz_ex_health_checker` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:btrz_ex_health_checker, "~> 0.1.1", app: false}
  ]
end
```
## Usage

```elixir
  my_connection_opts = %{hostname: "localhost", username: "postgres", password: "mypass", database: "mydb"}

  BtrzHealthchecker.info([%{checker_module: BtrzHealthchecker.Checkers.Postgres, opts: my_connection_opts}])
    %BtrzHealthchecker.Info{build: "d3b3f9133f68b8877347e06b3d7285dd1d5d3921", commit: "3d7285dd1d5d3921d3b3f9133f68b8877347e06b", 
      instanceId: "i-b3f9133f68b88", services: [%{name: "postgres", status: 200}], status: 200}
```

## Postgres checker
You can use the pre-defined BtrzHealthchecker.Checkers.Postgres
## Create your custom checkers
You can create and pass your own checkers using the Checker behavour, implementing `check_status/1` and `name/0`.

```elixir
defmodule MyApp.CustomChecker do
  @behaviour BtrzHealthchecker.Checker

  def name, do: "my_service"
  
  def check_status(opts) do
    // checking code here...
    200
  end
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/btrz_ex_health_checker](https://hexdocs.pm/btrz_ex_health_checker).

