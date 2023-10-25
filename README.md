# gen_ex

A generic Elixir generator that doesn't require Phoenix.

I essentially want to create an Elixir tool similar to:
- https://www.cookiecutter.io/
- https://www.hygen.io/
- https://yeoman.io/

## Concepts / Goals

- EEx Templates
  - Put custom templates in `priv/templates`.
  - Run `mix gen <template_slug> <args>` to generate files.
  - Each file in `priv/templates` represents a template that will generate a single file.
    - `priv/templates/new_thing.ex` can be used by running `mix gen new_thing <args>`.
  - Each subdirectory in `priv/templates` represents a set of templates that will generate multiple files
    - `priv/templates/new_things/` can be used by running `mix gen new_things <args>`.
    - If a directory shares the name of a single-file template, the single-file template will be used. If there are subdirectories, the generated code will match the same directory structure.

- Tag metadata
  - The generator will tag generated files/modules with some sort of trackable metadata and version (similar to a Mix project).
  - It should allow manual editing of everything except the metadata tags.
  - You can get a list of all template usages and versions with `mix gen.list <template_slug>`
  - The generator will attempt to update old versions of templates via something like `mix gen.update <template_slug> <new_version>`.
    - If it can't, it will display code that needs to be manually added.

## Links

Generic Elixir generators:

- https://hexdocs.pm/mix/Mix.Generator.html
- https://github.com/phoenixframework/phoenix/blob/main/lib/mix/phoenix.ex
- https://github.com/phoenixframework/phoenix/blob/main/installer/lib/phx_new/generator.ex
- https://github.com/phoenixframework/phoenix/blob/main/installer/lib/mix/tasks/phx.new.ex
- https://github.com/elixir-ecto/ecto/blob/master/lib/mix/tasks/ecto.gen.repo.ex
- https://github.com/pragdave/mix_generator
- https://github.com/zestcreative/elixirstream/blob/main/lib/utility/gen_diff/generator.ex

Phoenix generators:

- https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.html
- https://victorbjorklund.com/guide-to-custom-phoenix-phx-new-generator-mix-task
- https://fly.io/phoenix-files/customizing-phoenix-generators/

Code modification:

- https://github.com/doorgan/sourceror
  - Examples:
    - https://github.com/surface-ui/surface/blob/main/lib/mix/tasks/surface/surface.init.ex
    - https://github.com/liveshowy/webauthn_components/blob/main/lib/wac_gen/router.ex
