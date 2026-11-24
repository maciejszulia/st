# ADR 0001: Track the local config.h in git

## Status

Accepted.

## Context

Upstream st ships `config.def.h`; the [Makefile](../../../Makefile) copies it
to `config.h` only when `config.h` is absent. This fork carries scrollback
shortcuts, mouse bindings and a key-table fix that must survive a fresh clone.

## Decision

Track `config.h` in git next to `config.def.h`. Ignore build products and
patch residue in [.gitignore](../../../.gitignore), so local changes are visible
in `git status`.

## Consequences

- `make` on a fresh clone builds the workstation configuration.
- `config.def.h` and `config.h` differ; [README.md](../../../README.md) lists the
  bindings that differ.
- Upstream changes to `config.def.h` need a manual merge into `config.h`.

## Evidence

- Commit `4735753` ("chore: track local config and applied patches (scrollback)").
- Commit `26b5e54` ("chore: ignore build artifacts, track the applied scrollback patches").
- [config.h](../../../config.h), [config.def.h](../../../config.def.h), [.gitignore](../../../.gitignore).
