# @spynejs/kb

The SpyneJS Knowledge Base, in package form — the served knowledge layer that AI agents read when building SpyneJS applications.

## What this is

A content-only package (nothing compiles, nothing executes): 91 operation cards, 32 feature records, the mental model, and the task-routing trees that route any SpyneJS task to the cards that govern it. It is a render of the same corpus that produces the framework's agent kits — one source, versioned together.

## Who consumes it

- **Application templates** ship it, so a fresh project starts with current knowledge.
- **Agents** read it — start at `AGENTS.md`, which routes into `kb/`.
- **You** rarely open it directly; tooling and agents do.

## Install

```bash
npm install @spynejs/kb
```

## Currency

The knowledge here is versioned with framework releases: the package **minor** tracks framework releases; **patch** is knowledge-only corrections. Every version's `manifest.json` records `generatedFrom` — the exact hash-pinned knowledge-stack round it renders. See `CHANGELOG.md` for what changed in each cut.

## For agents

Read `AGENTS.md` at the package root. It states this package's authority over model priors, how to navigate (`manifest.json` → topic files), and what to do on version skew.
