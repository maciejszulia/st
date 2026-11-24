# ADR 0002: Scrollback as a ring buffer in st.c

## Status

Accepted.

## Context

Upstream st has no built-in scrollback. The [FAQ](../../../FAQ) lists the
upstream alternatives: a terminal multiplexer, the `scroll` tool or the
scrollback patch. This workstation needs scrollback in the terminal itself.

## Decision

- Apply the suckless scrollback patch and the scrollback-mouse patch to the
  source.
- Keep the history in a fixed ring buffer `Line hist[HISTSIZE]` with
  `HISTSIZE 2000`, indexed by `term.histi`; `term.scr` is the scroll offset.
- `TLINE(y)` selects a history line or a live-screen line; `tscrollup()`
  moves the line that leaves the screen into the buffer.
- Track both patch files in the repository for provenance; the build does
  not apply them again.

## Consequences

- Scrollback needs no extra process or library.
- Memory for 2,000 history lines is reserved in the `Term` structure.
- The patched [st.c](../../../st.c) differs from upstream, so upstream updates
  need a manual merge.

## Evidence

- Commit `4735753` ("chore: track local config and applied patches (scrollback)").
- Commit `26b5e54` ("chore: ignore build artifacts, track the applied scrollback patches").
- [st-scrollback-0.9.2.diff](../../../st-scrollback-0.9.2.diff),
  [st-scrollback-mouse-20220127-2c5edf2.diff](../../../st-scrollback-mouse-20220127-2c5edf2.diff).
- `HISTSIZE`, `TLINE`, `kscrollup()`, `kscrolldown()` and `tscrollup()` in [st.c](../../../st.c).
