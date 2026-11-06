# CLAUDE.md snippet

Paste this block into your own `CLAUDE.md` (or equivalent always-loaded
project instructions). Adjust `<KB_ROOT>` to wherever you placed the
knowledge base (this repo, a folder inside your Claude Code data directory,
or anywhere else Claude can read/write). The example below lists `CPAAS`,
`IBA`, `S2S` as a ready-to-edit starting point — rename or replace them
with your own solution names before you install this.

Keep it short — the point is that this stays in your always-loaded
instructions, while the detailed rules live in a separate file that gets
read only when relevant.

---

```markdown
# SOLUTION KNOWLEDGE MAPS
If a task touches CPAAS, IBA, or S2S (or another solution added later
under `<KB_ROOT>/`), check that solution's map in `<KB_ROOT>/<SOLUTION>/`
before analysis/config changes/debugging, and update it with newly learned
facts as you go. Full rules: `<KB_ROOT>/RULES.md` (read it the first time
this applies in a session).
```
