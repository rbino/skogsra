# Skogsra

> The _Skogsrå_ was a mythical creature of the forest that appears in the form
> of a small, beautiful woman with a seemingly friendly temperament. However,
> those who are enticed into following her into the forest are never seen
> again.

This library attempts to improve the use of OS environment variables and
application configuration. You would create a settings module e.g:

```elixir
defmodule Settings do
  use Skogsra

  # Rather equivalent to `System.get_env("POSTGRES_PORT") || 5432` (misses
  # the automatic casting to integer). Generates the function
  # `Settings.postgres_port/0`.
  @spec portgres_port() :: integer()
  system_env :postgres_port,
    default: 5432

  # Equivalent to
  # ```
  # System.get_env("POSTGRES_HOSTNAME") ||
  # (Application.get_env(:my_app, MyApp.Repo, []) |>
  #  Keyword.get(:hostname, "localhost"))
  # ```
  # Generates the function Settings.postgres_hostname/0
  @spec postgres_hostname() :: binary()
  app_env :postgres_hostname, :my_app, :hostname,
    domain: MyApp.Repo
    default: "localhost"
end
```

It can be used in the configuration file as well e.g:

```elixir
config :my_app, MyApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  hostname: Skogsra.get_env("POSTGRES_HOSTNAME", "localhost"),
  port: Skogsra.get_env_as(:integer, "POSTGRES_PORT", "5432"),
  (...)
```

Or from a module:

```elixir
defmodule MyApp do
  @port Skogsra.get_app_env "POSTGRES_PORT", :my_app, :port,
    domain: MyApp.Repo,
    default: 5432

  @spec get_port() :: integer()
  def get_port, do: @port
end
```

## Installation

The package can be installed by adding `skogsra` to your list of dependencies
in `mix.exs`:

```elixir
def deps do
  [{:skogsra, "~> 0.1"}]
end
```

## Author

Alexander de Sousa.

## License

`Skogsra` is released under the MIT License. See the LICENSE file for further
details.
