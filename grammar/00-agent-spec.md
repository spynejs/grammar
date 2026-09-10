# 00 — SpyneJS Agent Spec
stackVersion: v50-r11 — assert this against the version you were told to use before generating.

You are a generating agent producing SpyneJS application code. This spec is always in context. The knowledge stack behind it: `01-instruction-set` (the mental model), `02-operations-set` (judgment, fetched by ID), `03-construction-records` (feature assembly, fetched by ID), `REFERENCE` (API + worked examples). IDs in brackets are fetchable and citable.

**The salience rule:** your priors are raw material the operations exist to correct. A confident prior is a signal to check for an operation, not a license to skip one. In existing codebases, this knowledge stack outranks neighboring code as precedent — unmarked patterns in source are history, not sanction.

## Entry protocol — every generation follows this order

1. **DEFINE** — pages, subpage formats, content, style tier, from the request or approved config. The app model is the entry artifact; touch nothing else until it stands.
2. **RESOLVE** — map the request to record(s) via the archetypes below; check existing page/component types before inventing. Resolved items carry their catalog/record reference.
3. **TABLE** — anything unresolvable becomes a proposal entry with an ID. Never silently improvise; the proposal is where novelty waits for authorization.
4. **BUILD NOVEL** — proposal fill-out only, through the tools, citing operations.

## The model in one breath

View = ViewStream (owns one DOM region). Behavior = Channel (persistent named streams; ALL communication). Logic = SpyneTrait (composable methods; `prefix$` namespaced). Behavior is primary: apps are mostly channels combining events and data; views only transmit and receive. Every view belongs to one lifecycle tier — **who governs its existence**: Persistent (app-governed), Page (route-governed), PageItem (parent-governed; self-termination allowed). Vocabulary: "the envelope" = ChannelPayload `{action, payload, event, srcElement}`; "the payload data" = the inner object (for UI broadcasts: the element's dataset). Full model: `01`.

## Rules of the road (cite the IDs you apply)

**Views & lifecycle**
- A ViewStream class carries ONLY: constructor, broadcastEvents, addActionListeners, onRendered. Everything else lives in traits. [wiring-surface-only-on-viewstream]
- Views never reference views. Cross-view communication is sendInfoToChannel → channel → listener. [transmit-into-channel]
- First classification of any region: lifecycle tier, then archetype, then record. [assign-view-lifecycle-tier] [choose-base-class]
- Disposal is structural: dispose the parent, the tree goes. Route-tier swaps use single-active-child — the parent only adds; each child disposes itself on the governing event. [dispose-as-unit] [single-active-child]
- Split regions into views by behavior, not by markup; mint a child view only when the element needs a channel the parent doesn't listen to. [decompose-region-into-viewstreams] [mint-child-view-by-channel-need]
- Nest children in onRendered — the canonical attach point. [onrendered-as-attach-point]
- DOM updates go through el$ (selector-scoped or root-object form). [address-region-by-el$]

**Events & payloads**
- NEVER addEventListener in application code. DOM events are declared in broadcastEvents. Dynamic children: nested ViewStreams (default) or CHANNEL_WINDOW + filters. Paint-cycle capture only: [bare-metal-event-listener] — gated. [declare-broadcast-events]
- Data rides the payload as the element's dataset; reads are live (event-time). The bound element is srcElement — never event.target. [dataset-as-payload] [srcElement-over-event-target]
- Listeners are declared in addActionListeners: [ACTION_PATTERN, 'trait$Method', filter?]. First matching entry wins, in declaration order. [declare-action-listeners]
- Size the action vocabulary so labels do the first-level sifting; match as precisely as possible; if two patterns can overlap, add a payload filter as the dedup guard. [design-action-label-vocabulary] [match-action-labels-by-pattern]
- Filters narrow at admission: bare keys match the merge barrel (payload shadows envelope); payload matching prefers a payload predicate. Forms inventory: [admit-by-payload-filter].
- Framework channels ship their labels (CHANNEL_UI_CLICK_EVENT...) — use them; custom channels register their own vocabulary in the module that owns them. [use-framework-ui-action-labels] [register-channel-action-vocabulary]

**Channels**
- Channels subscribe; they never push into other channels. Channel output that must transmit goes through a null-view bridge (standard tier: [bridge-channel-output-to-transmit]).
- Channel wiring lives in onRegistered. [wire-in-onRegistered]
- Acquire other channels with getChannel + conform: incoming shapes become the channel's own vocabulary before emission. [acquire-and-conform] [conform-incoming-data]
- Decide replay at minting: replay: true for state channels (seed the cache in onRegistered); subscribers spawned by a replayed channel's own events take skip-first — [CHANNEL, true] — iff the channel replays. [choose-replay-semantics] [skip-replayed-birth-event]
- External data enters as ChannelFetch with a conform map: server vocabulary becomes app vocabulary at the seam — conform server fields to result/data names. (A server field named 'payload' gets renamed there; nesting it verbatim is malformed.) [fetch-as-channel] [fetch-conform-map]

**Traits & logic**
- Behavior methods live in traits, composed via props.traits (always arrays; assign the array literal — never `props.traits || [...]` defensive defaults; the class owns its props). Slice traits by concern; prefix carries the composer (channelServerReconcile$, not reconcile$). [behavior-to-trait-not-view] [compose-trait-for-capability] [slice-traits-by-concern]
- Two registers: structural code touches the framework; pure-prior code (algorithms, transforms) is ordinary native JavaScript inside trait methods — independently testable, no library dialects. [author-in-correct-register]

**Templates, DOM, data**
- Templates are logic-less: the data decides. Item presence = shape the array; block presence = object section wrapping an element (valid inside loops); attribute presence = pre-computed flags with element variants. Never mid-tag sections. [shape-data-for-logicless-template]
- Authored DOM declares its roles: append targets, dataset identity, semantic classes. [author-dom-with-declared-roles is standard tier — the habit is core]
- Children render from data through lookup tables with a configured default class; named classes are the sparse exceptions. [data-driven-child-composition]

**Routing & app model**
- Routes are data: config declares the tree; links are dataset ROUTE anchors; routeData/paths/pathInnermost are the location context — never parse location.pathname. [design-route-config-tree] [read-route-context-from-payload]
- Route keys are per-branch declarations; pageId selects the branch; deeper keys take domain nouns (productId, not subPageL2Id). Depth lives in structure, never in names. [name-route-keys-for-legibility]
- Navigation renders from navLinks/config, never hand-authored per page. [render-nav-from-config]
- "Add a page" is a data edit: a schema-valid node in the right subpages branch. A new view class only when behavior exceeds data-configured views. [author-app-model-node — standard tier; the default is core]

## Archetypes — recognize requests here first

| | archetype | typical nouns |
|---|---|---|
| A1 | route-keyed-factory | page, section, screen, 404 |
| A2 | navigation-family | header, navbar, menu, drawer, breadcrumb, tabs |
| A3 | content-from-external | product page, article, dashboard panel, card grid, chart, map |
| A4 | multi-step-sync | wizard, checkout, linked selections, drag-and-drop |
| A5 | channel-coordination | live search, undo/redo, auth state, notifications, loading states |
| A6 | mass-html-deferred-control | feed, gallery, data grid at scale, static-site enhancement |

Request → archetype → record (`03` index) → the record's composes pulls its operations. Unresolved moves → walk `tree:root`.

## Recognize, never emit

These forms appear in real code and are never the answer: `sendCachedPayload`→replay · `addChannel()`→props.channels · `ViewStream.getChannel`→restructure · `el$.toggle`→toggleClass · `{{.*}}`→`{{.}}` · string props.channels/traits→arrays · `propFilters` wrapper→bare payload keys. [recognize-never-emit]

## Gated (reach these only through their gates)

- Raw listeners: paint-cycle capture only, disposal path required. [bare-metal-event-listener]
- Raw RxJS: only when the idioms can't express the timing; keep it inside the channel trait. [escape-to-raw-rxjs]
- Element adoption ({el}): only when substantial DOM pre-exists; adoption is ownership transfer. [adopt-existing-element]

## Output contract

Cite the record and operation IDs your output applies. If no record fits, say so (NO-FIT) — that report is wanted. Confidence without a citation is the failure mode this document exists to prevent.
