# Knowledge Map Maintenance Rules

Copy this file into your knowledge-base location and edit the solution list
below to match what you actually work with — the `example/` directory in
this repo ships with `CPAAS`, `IBA`, and `S2S` filled in as a ready-to-edit
starting point; rename or replace them with your own solutions before you
install this.

Location: one subdirectory per solution, e.g. `<KB_ROOT>/<SOLUTION_NAME>/`.
Currently tracked solutions: `CPAAS`, `IBA`, `S2S`
(edit this list — add, remove, or rename solutions as needed).

## When to use

If you recognize that the current task touches one of these solutions (their
apps, hosts, Kubernetes workloads, configs, or related debugging/incident
work), open that solution's map before analysis, configuration changes, or
debugging. Treat it as your first reference point, in addition to — not
instead of — reading the live repo/cluster state.

## Structure (per solution directory)

1. `README.md` at the root of the solution directory — describes the overall
   architecture and operating principles of everything in that directory
   (how the pieces fit together, high-level data/call flow, deployment
   model).
2. One subdirectory per concrete application/host/Kubernetes
   resource/component. Example (see `example/CPAAS/`): `freeswitch/`,
   `kamailio/`, `api-gw/`, etc. Each component subdirectory documents that
   component specifically — role, configuration, how to inspect/debug it,
   known quirks.

## Maintenance rule

During any session that works with these solutions, update the relevant map
file(s) with newly learned facts that weren't already captured — especially
anything that will help understand or diagnose similar problems in the
future (root causes, non-obvious configuration, gotchas, where to look). Do
this incrementally as you learn things, not only at the end of a task.

Keep secrets/credentials out of these files — reference them indirectly
(e.g. "see vault/secret X") instead of inlining them.

## Keep it generic, not stand-specific

These solutions get deployed on different projects/stands, each with its own
IPs, hostnames, passwords, and other concrete values. Write the maps so they
describe the solution itself, not one particular deployment:

- Capture the *how it works*, *what it's for*, and *how it's structured* —
  components, their roles, how they interact, typical failure modes — not
  hardcoded IPs, hostnames, credentials, or other stand-specific values.
- Where a concrete value would otherwise appear, use a placeholder (e.g.
  `${HOST}`, `${API_PORT}`) instead of a literal one, so the same page stays
  valid across stands.
- If a value truly only makes sense for one specific stand (e.g. a one-off
  workaround), say so explicitly rather than presenting it as the general
  rule.
