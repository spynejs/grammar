# Changelog

All notable changes to the SpyneJS Knowledge Base package. Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning policy: **minor tracks framework releases, patch is knowledge-only corrections.** Every release records the knowledge-stack round it renders (`generatedFrom` in `manifest.json`).

## [Unreleased]

## [0.3.0] — 2026-09-10

- Rendered from knowledge-stack round v50-r11 (hash-pinned in `manifest.json`)
- BREAKING (structure only): payload directory renamed kb/ → grammar/ (ruled 2026-09-10). manifest.json → entry and files[] paths follow; consumers that locate files through the manifest need no change. package.json exports keeps ./kb/* as an alias of ./grammar/* for one transition window
- Content unchanged: same v50-r11 render as 0.2.x
- Framework compatibility: spynejs >=0.25

## [0.2.1] — 2026-09-10

- Rendered from knowledge-stack round v50-r11 (hash-pinned in `manifest.json`)
- Package wording: agents are pointed at the SpyneJS Grammar by its ratified name (the Grammar / the SpyneJS Grammar / Generative Grammar) — AGENTS.md package section, README, manifest envelope description
- Content unchanged: same v50-r11 render as 0.2.0
- Framework compatibility: spynejs >=0.25

## [0.2.0] — 2026-09-10

- Rendered from knowledge-stack round v50-r11 (hash-pinned in `manifest.json`)
- Content round — 8 caveats across 6 cards (deck 2026-08-30 §1/§2/§5, crm-tracker 2026-09-02 §1/§2/§3, packaging 2026-08-11 §1a, data-is-custom-event rule per spyne 0.26.7)
- `skip-replayed-birth-event`: +1 caveat
- `safeclone-for-proxified-data`: +2 caveats
- `declare-action-listeners`: +1 caveat
- `declare-broadcast-events`: +1 caveat
- `author-template-bound-surface`: +1 caveat
- `register-channel-action-vocabulary`: +2 caveats
- Framework compatibility: spynejs >=0.25

## [0.1.0] — 2026-08-11

Initial release.

- Rendered from knowledge-stack round v50-r10 (hash-pinned in `manifest.json`)
- 91 operation cards, 32 feature records, mental model, task-routing trees
- Framework compatibility: spynejs >=0.25
