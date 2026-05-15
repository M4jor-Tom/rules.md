# Proto sharing across monorepo + submodules

- Source of truth: dedicated proto repository
- Root monorepo pins it as a submodule at `protos/`
- Each subproject commits its generated files
- The root's CI checks that building the protos does not generate diff into submodules
- Each submodule is proto-agnostic, and is able to run on its own. They still can build protos from ../protos if present
- To update protos: edit in protos/, generate protos for each submodule, commit+push submodule
