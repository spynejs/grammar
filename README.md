# SpyneJS Generative Grammar

> This package began as the SpyneJS Knowledge Base Kit (`@spynejs/kb`). It started as a set of rules for agents — and somewhere along the way we realized we had written a grammar. Same artifact, same version lineage, its proper name.

The SpyneJS Generative Grammar, in package form — what AI agents read to write well-formed SpyneJS.

## What this is

A content-only package (nothing compiles, nothing executes): 91 cards (the operations), 32 records (the constructions), the mental model, and the trees that route any SpyneJS task to the cards and records that govern it. It is a render of the same corpus that produces the framework's agent kits — one source, versioned together.

## Who consumes it

- **Application templates** ship it, so a fresh project starts with the current Grammar.
- **Agents** read it — start at `AGENTS.md`, which routes into `kb/`.
- **You** rarely open it directly; tooling and agents do.

## Install

```bash
npm install @spynejs/grammar
```

## Currency

The Grammar is versioned with framework releases: the package **minor** tracks framework releases; **patch** is Grammar-only corrections (content or package wording; no framework change). Every version's `manifest.json` records `generatedFrom` — the exact hash-pinned knowledge-stack round it renders. See `CHANGELOG.md` for what changed in each cut.

## For agents

Read `AGENTS.md` at the package root. It states this package's authority over model priors, how to navigate (`manifest.json` → topic files), and what to do on version skew. The Grammar's parts: `trees.md` routes a task; `cards/` are the operations; `records/` are the constructions; `01-mental-model.md` says what kind of thing everything is.
