# AGENTS.md — SpyneJS Development
stackVersion: v50-r10 — assert this against the version you were told to use before generating.

You are working in a SpyneJS codebase. SpyneJS is a browser-platform-first frontend framework — do not translate React/Vue/Angular idioms into it. Your training priors about frontend frameworks are raw material that the knowledge in this repo corrects.

## The fetch discipline (non-negotiable)

**Never author SpyneJS code from this file alone.** This file carries rules and routing — not enough to write correct code. Before writing or modifying any file:

1. Identify the task's shape: `kb/trees.md` routes any task to its cards.
2. **Read the relevant cards** (`kb/cards/<op-id>.md`) — each carries the judgment AND a worked example. The examples are house-canonical: imitate them.
3. For whole features, find the matching record (`kb/records/<record-id>.md`) — its recognition line tells you when it applies; its composes list names every card to read.
4. Neighboring code in this repo that follows the cards is also precedent. Neighboring code that contradicts a card is legacy — the card wins.

If no card or record fits the task, SAY SO before improvising, and propose the shape you intend. A wrong guess that looks conformant is the failure mode this file exists to prevent.

For the full mental model (what kind of thing everything is), read `kb/01-mental-model.md` once per session when doing substantial work.

## Rules of the road (ambient — always apply)

- A ViewStream class carries ONLY: constructor, broadcastEvents, addActionListeners, onRendered. All other methods live in traits.
- Views never reference views. Cross-view communication: sendInfoToChannel → channel → listener.
- NEVER addEventListener in application code. DOM events are declared in broadcastEvents (bound after onRendered — children appended there are covered).
- Data rides the payload as the element's dataset; reads are live at event time. The bound element is srcElement — never event.target.
- Listeners: [ACTION_PATTERN, 'trait$Method', filter?]. Exact labels beat patterns; write matches as precisely as possible.
- Filters: bare keys match payload data; use payload methods for conditions; conform server fields to result/data at the fetch map (a nested 'payload' key inside payload data is malformed).
- props.channels and props.traits are always arrays — assigned as literals, never `|| [...]` defensive defaults (the class owns its props). Replay channels seed state in onRegistered; views born from a replay channel's own event take ['CHANNEL', true].
- Channels subscribe; they never push into other channels. Channel output that must transmit goes through a null-view bridge.
- Behavior methods live in traits (static by default), composed via props.traits; prefixes carry the composer (channelServerReconcile$, not reconcile$). Pure logic is ordinary native JavaScript.
- Templates are logic-less: the data decides. {{.}} in string loops; sections wrap whole elements; presence = shape the data.
- Routes are data: config declares the tree; links are dataset ROUTE anchors; read routeData/paths from route payloads — never parse location.pathname.
- Canonical forms only: replay, toggleClass, arrays, {{.}}. Older aliases exist in legacy code — recognize them when reading; never write them (details: kb/cards/recognize-never-emit.md).
- Dispose the parent, the tree goes. Route-tier swaps: the parent only adds; each child removes itself on the governing event.
- Constants live on SpyneAppProperties — never in constants files.

## Task recognition

| Request sounds like | Read first |
|---|---|
| page, section, screen | kb/records/create-a-page.md |
| header, nav, menu, drawer, breadcrumb, tabs | kb/trees.md → navigation family |
| list + detail, product page, card grid | kb/records/master-detail.md |
| form, validate, submit | kb/records/form-validate-submit.md |
| modal, toast, confirm | kb/records/modal-open-close.md, kb/records/toast-notification-system.md |
| search-as-you-type | kb/records/debounced-typeahead-search.md |
| dark mode, settings that persist | kb/records/theme-or-mode-toggle.md, kb/records/persist-settings-via-storage-channel.md |
| integrate <library> | kb/records/external-library-as-behavior-source.md |
| loading states, skeletons | kb/records/skeleton-then-content.md, kb/records/global-loading-indicator.md |
| anything else | kb/trees.md from the root |

## Output contract

When you complete a task, state which record and cards you applied (by ID). If none fit, say NO-FIT and what you did instead — that report is wanted.


## Package navigation (this npm package)

This is @spynejs/grammar, the SpyneJS Knowledge Base in package form. `manifest.json` at the package root is the machine-readable index: version, `frameworkCompat`, and every file with its topic. The knowledge itself lives under `kb/` at the paths referenced above.

## Version skew

`manifest.json → frameworkCompat` states the framework range this knowledge describes. If the project's SpyneJS version falls outside it, say so — do not guess across the skew.

<!-- PENDING (gap-log, Bootstrap thread): the data-is-custom-event="true" declaration rule — verified absent from the kit render 2026-08-11; exact rule text to be supplied before this comment is replaced. -->
