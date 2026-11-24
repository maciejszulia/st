# ADR 0003: Clipboard mouse bindings

## Status

Accepted.

## Context

Upstream st pastes the PRIMARY selection on middle click. On this
workstation the copy and paste flow uses the CLIPBOARD selection.

## Decision

In [config.h](../../../config.h):

- middle click (`Button2`) calls `clippaste`;
- right click (`Button3`) calls `clipcopy`;
- the wheel (`Button4`, `Button5`) with any modifier calls `kscrollup` and
  `kscrolldown`.

The same commit changes the Delete key in application keypad mode to send
`\033[3~` instead of `\033[P`.

## Consequences

- Copy and paste with the mouse use the same selection as Ctrl + Shift + C / V.
- [config.def.h](../../../config.def.h) keeps the upstream wheel bindings, so the
  template and the tracked configuration differ.

## Evidence

- Commit `fdf22ce` ("feat(config): clipboard mouse bindings, fix Delete escape").
- `mshortcuts` table in [config.h](../../../config.h); `clipcopy()` and `clippaste()` in [x.c](../../../x.c).
