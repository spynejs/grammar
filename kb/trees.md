# Trees — route any task to its cards

**tree:root** — Is the request a recognized feature shape?
- Yes — matches an archetype noun -> index:records (archetype → record recognition surfaces; the record's composes pulls its operations)
- No — decompose; then per move, which concern? -> node:root-layer

**node:root-layer** — Which concern is this move in?  (op: choose-base-class)
- A region's existence, boundaries, or DOM -> tree:view
- Events, data flow, coordination, state -> tree:behavior
- Where a method/computation lives -> tree:logic
- App setup: index.js, routes, model, build -> tree:scaffold

**tree:view** — Who governs this region's existence?  (op: assign-view-lifecycle-tier)
- The app (scaffold-born, never disposed) — incl. invisible and transient-host views -> node:view-persistent
- The route -> node:view-page
- A parent's cascade -> node:view-child

**node:view-persistent** — What kind of persistent view?
- Visible chrome rendering empty, populated on events -> op:render-empty-populate-on-event
- Behavior without presence -> op:null-appended-behavior-view
- Host for self-terminating transients (modal, toast) -> record:modal-open-close | record:toast-notification-system

**node:view-page** — On route change, dispose or hide?  (op: dispose-vs-hide)
- Dispose (default): parent adds, child removes itself -> op:single-active-child
- Hide (state worth keeping warm) -> op:dispose-vs-hide

**node:view-child** — Does this element need a channel the parent doesn't listen to?  (op: mint-child-view-by-channel-need)
- No — parent maintains it (broadcastEvents + el$) -> op:address-region-by-el$
- Splitting a larger region into multiple views -> op:decompose-region-into-viewstreams
- Yes, and it carries behavior/lifecycle -> node:view-class
- Yes, but children are rendered dynamically after binding -> op:dynamic-children-ingress
- Static fragment, no behavior ever -> op:domelement-vs-viewstream
- Children are generated from data -> node:view-data-children
- The parent's own content/markup -> node:view-template

**node:view-class** — How does the view come to exist in the DOM?
- Rendered and appended (default) -> op:onrendered-as-attach-point | op:nest-view-without-handle
- Adopting substantial pre-existing DOM -> op:adopt-existing-element
- Many items now, behavior later -> record:deferred-behavior-adoption

**tree:behavior** — Which direction does this move flow?
- View → channel (something happened) -> node:b-ingress
- Channel → view (react to behavior) -> node:b-egress
- Channel ← channels (combine, derive, acquire) -> node:b-combine
- The route (location as behavior) -> node:b-route
- External world → channel (data, libraries, browser) -> node:b-external
- Where does state live -> node:b-state

**node:b-ingress** — What kind of source?
- A declared DOM event on this view's elements -> op:declare-broadcast-events
- Elements rendered after binding -> op:dynamic-children-ingress
- A semantic moment (step done, threshold crossed) -> op:transmit-into-channel
- A continuous signal (rAF, drag physics, sensor) -> op:discretize-continuous-input-at-source
- Multi-event capture within/between paint cycles -> op:bare-metal-event-listener

**node:b-egress** — How should the listener narrow?
- Declare it: [PATTERN, 'trait$Method', filter?] -> op:declare-action-listeners
- One label vs a family of labels -> op:match-action-labels-by-pattern
- Admission conditions (payload data, selector, predicates) -> op:admit-by-payload-filter
- State-dependent interactivity (legal moves only) -> op:gate-interactivity-via-class-and-filter
- Self-removal when a condition stops holding / threshold passes -> op:dispose-by-predicate-filter
- Spawned by the channel's own replayed event -> op:skip-replayed-birth-event
- Must ignore its own emissions -> op:recognize-own-emission

**node:b-combine** — Does this behavior need its own channel?  (op: mint-channel-vs-ride-existing)
- No — ride CHANNEL_UI/ROUTE/WINDOW with filters + trait dispatch -> op:admit-by-payload-filter
- Yes — mint; then how do sources relate? -> node:b-combine-mode (and register the vocabulary: op:register-channel-action-vocabulary)

**node:b-combine-mode** — How do the source channels relate?  (op: choose-derived-vs-merged-channel)
- React to one, enhance, emit own (sequential) -> op:acquire-and-conform
- Need several together (simultaneous) -> node:b-merge-mode
- Async triggered per action (search, save, spam-clicks) -> op:select-concurrency-operator
- The idioms can't express the timing -> op:escape-to-raw-rxjs
- Channel output must trigger a transmit -> op:bridge-channel-output-to-transmit

**node:b-merge-mode** — Snapshot or continuous?  (op: choose-merge-emission-mode)
- Once, when all sources have emitted (gate) -> record:combine-sources-into-domain-payload
- Continuously as any source emits -> op:choose-merge-emission-mode

**node:b-external** — What kind of external source?
- HTTP data -> node:b-fetch
- A JS library with its own events/loop -> record:external-library-as-behavior-source
- Browser/window events (resize, scroll, media query, keyboard) -> op:window-event-via-channel
- Storage (settings, persistence) -> record:persist-settings-via-storage-channel
- Entities addressed by route params -> op:entity-routes-from-data
- Another frame/app -> record:cross-app-postmessage-bridge

**node:b-fetch** — When should the fetch fire?  (op: pause-fetch-vs-autofire)
- On registration (app model, initial data) -> op:fetch-as-channel
- On demand (mutations, per-navigation, search) -> op:pause-fetch-vs-autofire
- Inside a channel trait (channels can't push into ChannelFetch) -> op:retry-backoff-via-channelfetchutil
- Shaping the response / errors -> op:fetch-conform-map

**node:b-state** — What kind of state?  (op: spyneappproperties-vs-channel-state)
- Durable domain state, evolving on events -> op:state-machine-in-channel
- App constants and settings -> op:spyneappproperties-vs-channel-state
- Ephemeral display mirroring -> op:live-mirror-via-el$
- Should late subscribers get current state? -> op:choose-replay-semantics
- Optimistic mutations against a server -> record:optimistic-update-with-reconcile

**tree:logic** — Which register is this code in?  (op: author-in-correct-register)
- Structural (touches the framework: renders, wires, emits, times) -> node:l-structural
- Pure prior (input → output, no framework touch) -> node:l-pure

**node:l-structural** — Where does the method live?  (op: behavior-to-trait-not-view)
- In a trait composed into its host (never on the class) -> op:compose-trait-for-capability
- Which trait? Slice by concern; prefix carries the composer -> op:slice-traits-by-concern
- Naming -> op:name-trait-prefixes-by-composer
- Tempted to subclass a subclass -> op:single-extension-only

**node:l-pure** — Pure-register placement
- Native JS inside a trait method; independently testable -> op:author-in-correct-register
- Library machinery (scene, player, socket objects) -> record:external-library-as-behavior-source

**tree:scaffold** — Which scaffold surface?
- index.js: init, registrations, imports -> op:index-js-as-structural-spine
- Channels registered before use -> op:register-channel-upfront
- Routes: the tree, per-branch keys -> op:design-route-config-tree
- Content: pages, subpages, pageItems -> op:author-app-model-node
- Dev-only tooling -> op:gate-dev-tools-by-env-import
- The whole greenfield app -> record:greenfield-app-from-model
- CMS present (template-as-data) -> op:attr-prefix-for-attribute-placeholders
- Cross-frame handshake -> op:handshake-via-temp-prop

**node:view-template** — How does this region's content render?
- Template with data-shaped presence (items/blocks/attributes) -> op:shape-data-for-logicless-template
- Optional block or wrapper -> op:conditional-via-object-section
- Choosing/designing the bound fields -> op:author-template-bound-surface
- DOM roles: targets, dataset identity, semantic classes -> op:author-dom-with-declared-roles

**node:view-data-children** — Children come from data — how?
- Lookup table with a configured default class; named classes sparse -> op:default-class-with-sparse-exceptions
- The composition mechanics -> op:data-driven-child-composition
- Authoring a pageItem spec (viewClass, props, container) -> op:author-pageitem-spec
- Data-first now, promote to a module later -> op:prototype-in-data-then-promote

**node:b-route** — What about the route?
- Reading location context (routeData, paths, pathInnermost) -> op:read-route-context-from-payload
- Reacting to the KIND of move (added/removed/changed) -> op:react-to-route-diff
- A view parameterized by route coordinates -> op:route-scoped-view-state
- Filters/pagination as shareable URL state -> op:query-params-as-route-state
- Authoring links -> op:author-navigation-as-dataset-links
- Nav/menus/breadcrumbs from config -> op:render-nav-from-config
- Navigation itself is data on a channel -> op:route-as-data

Ambient rules (always apply, in CLAUDE.md): wiring-surface-only-on-viewstream, srcElement-over-event-target, dataset-as-payload, conform-incoming-data, wire-in-onRegistered, use-framework-ui-action-labels, design-action-label-vocabulary, dispose-as-unit, no-leaked-subscription, clone-frozen-payload, recognize-never-emit, name-route-keys-for-legibility, name-views-by-role-suffix, name-trait-prefixes-by-composer, safeclone-for-proxified-data, images-by-search-intent-not-url