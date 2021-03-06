# Changelog

## Changelog for 2.2.1

### Bugfix

  * When no type is defined and it cannot be derived from the default value,
    then it should return `any()` instead of `binary()`.

## Changelog for 2.2.0

### Enhancements

  * Added JSON config provider.
  * Added new `Skogsra.Binding` behaviour for adding custom variable bindings.
  * New option `binding_order` for setting a custom order for variable binding
    (defaults to `[:system, :config]`). Possible values:
    + `:system`: For loading OS environment variables.
    + `:config`: For loading application configuration variables.
    + `module()`: For loading variables using a custom module implementing
      `Skogsra.Binding` behaviour.
  * Added `binding_skip` option to skip one or several variable binding types
    (defaults to `[]`).

### Breaking changes

  * Improved YAML config provider by making it equivalent to the JSON provider.

### Deprecations

  * The option `skip_config` was deprecated favoring `binding_skip: [:config]`.
  * The option `skip_system` was deprecated favoring `binding_skip: [:system]`.

## Changelog for 2.1.1

### Bug fixes

  * Fixed bug where `Skogsra.Type` couldn't be used as a type (see [Custom Type Fails at get_spec_type](https://github.com/gmtprime/skogsra/issues/4))

## Changelog for 2.1.0

### Enhancements

  * Improved function specs.
  * Improved generated docs.
  * Added option to avoid automatically generated docs.
  * Added function for OS environment variable generation for Unix, Releases
    and Windows.

## Changelog for 2.0.4

### Enhancements

  * Improved documentation.

## Changelog for 2.0.3

### Enhancements

  * Improved errors when a variable is missing.

## Changelog for 2.0.2

### Enhancements

  * Added `:module` built-in type.
  * Added `:unsafe_module` built-in type.

## Changelog for 2.0.0

### Enhancements

  * Added `Skogsra.Type` behaviour for defining custom types.
  * Application configuration values are now casted as well to the defined
    type in the `Skogsra` environment variable definition.
  * Added YAML configuration provider.

## Changelog for 1.3.0

### Enhancements

  * Namespaces now inherit values from default namespace.
  * Favoring the use of `:persistent_term`s over `:ets` tables. This avoids the
    creation of an application tree for this project, thus making it even
    faster.

## Changelog for 1.2.1

### Bug fixes

  * Fixed bug where `Skogsra.Cache` didn't work at compilation time.

## Changelog for 1.2.0

### Enhancements

  * Added autogenerated reload functions.
  * Added autogenerated setter functions.
  * Improved documentation.
  * Code rearrangement and refactor for maintainability.
