# Claude Project Knowledge Base — a reusable pattern

A small, reusable convention that lets Claude Code build and maintain a
**living, generic knowledge map** of the infrastructure solutions you work
with — across sessions, without re-discovering the same things every time,
and without baking in credentials or stand-specific values.

It solves one recurring problem: when you repeatedly work with the same
kind of solution (deployed differently on every project/stand), an AI
assistant re-learns its architecture, quirks, and gotchas from scratch each
session. This pattern gives it a place to write that knowledge down once,
keep it generic enough to stay valid across stands, and read it back before
the next debugging/config session.

## How it works

1. **A short, always-loaded pointer** lives in your `CLAUDE.md` (or
   equivalent always-loaded instructions file). It just says: "if this task
   touches solution X/Y/Z, check its knowledge map before acting, and update
   it as you learn things." See [`CLAUDE-MD-SNIPPET.md`](CLAUDE-MD-SNIPPET.md).
2. **The detailed maintenance rules** live in a separate file
   ([`RULES.md`](RULES.md)) that Claude reads only when the pointer applies —
   keeping your always-loaded instructions short.
3. **The actual knowledge** lives in one directory per solution, each with:
   - a root `README.md` describing the overall architecture and operating
     principles of that solution;
   - one subdirectory per concrete application/host/Kubernetes
     resource/component, each documenting that piece specifically.
4. Everything is written **generically** — no real IPs, hostnames,
   passwords, or other stand-specific values. Use placeholders
   (`${HOST}`, `${API_PORT}`, ...) instead, so the same map stays valid
   across every deployment of that solution.

## Quick start

This repo ships with a concrete, ready-to-edit example already filled in:
`example/CPAAS`, `example/IBA`, `example/S2S` (with `freeswitch/`,
`kamailio/`, `api-gw/` as example components under `CPAAS`). Treat it as a
starting point to rename and rewrite, not a fixed requirement.

1. Pick a location for your knowledge base (a dedicated repo like this one,
   or a folder inside your Claude Code data directory — anywhere Claude can
   read/write).
2. Copy the `example/` directory there and rename `CPAAS` / `IBA` / `S2S`
   (and their component subdirectories) to your own solutions and
   components — or delete/add as needed. Rewrite each `README.md`'s content
   to match what you actually run.
3. Copy [`RULES.md`](RULES.md) next to it and update the solution list at
   the top to match what you kept/renamed.
4. Copy the block from [`CLAUDE-MD-SNIPPET.md`](CLAUDE-MD-SNIPPET.md) into
   your own `CLAUDE.md`, adjusting the path and solution names.
5. From then on, just work normally — Claude checks the map when relevant
   and keeps it updated, generic and up to date as you go.

## Layout of this repo

```
.
├── README.md               — this file
├── RULES.md                — the maintenance rules (copy into your KB location)
├── CLAUDE-MD-SNIPPET.md     — the block to paste into your own CLAUDE.md
└── example/                — a ready-to-edit example (rename/replace before use)
    ├── CPAAS/
    │   ├── README.md
    │   ├── freeswitch/README.md
    │   ├── kamailio/README.md
    │   └── api-gw/README.md
    ├── IBA/
    │   └── README.md
    └── S2S/
        └── README.md
```

## Design principles

- **Generic over specific** — capture how a solution works and why, not one
  particular deployment of it.
- **Incremental** — update the map as you learn things during real work, not
  as a separate documentation task.
- **Cheap by default** — the always-loaded part of this is two lines; the
  rest is loaded only when relevant.
- **No secrets, ever** — reference credentials indirectly (e.g. "see vault
  entry X"), never inline.
