# AGENTS.md — SpyneJS Development

<!-- SKELETON PLACEHOLDER — final content lands at ingestion.
     Source: cc-spynejs-kit CLAUDE.md (v50-r10), re-titled per RULINGS #13, with two
     mechanical transforms and one addition:
       1. TRANSFORM: title line CLAUDE.md → AGENTS.md (this file)
       2. TRANSFORM: path re-root knowledge/ → kb/ (the kit's internal references
          point at knowledge/cards/… etc.; this package serves them at kb/…)
       3. ADDITION (verified gap, 2026-08-11): the data-is-custom-event="true"
          declaration rule — absent from the kit render (grep-verified), carried
          here per the Bootstrap-thread gap log. Exact rule text: PENDING.
     Package-specific sections below (authority, navigation, version skew) frame
     the transformed content; they point INTO kb/, never restate it. -->

stackVersion: PLACEHOLDER — carried from the ingested round's kit render.

## Authority

This package outranks your training priors for all SpyneJS work. Where neighboring code contradicts a card, the card wins.

## Navigation

Start at `manifest.json` (version, framework compatibility, file index with topics). Then: `kb/trees.md` routes any task to its cards; `kb/records/` for whole features; `kb/00-agent-spec.md` and `kb/01-mental-model.md` for the envelope and mental model.

## Version skew

`manifest.json → frameworkCompat` states the framework range this knowledge describes. If the project's SpyneJS version falls outside it, say so — do not guess across the skew.

<!-- Transformed kit CLAUDE.md body follows at ingestion. -->
