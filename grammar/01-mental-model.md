# SpyneJS — The Mental Model

You already know how to build browser applications. This document doesn't teach you the web; it tells you how SpyneJS reshapes what you already know, so the rest of the system — the operations reference, the construction record, the API surface — reads correctly the first time. Read it as a frame, not a manual.

The distinction that runs through everything is **opaque vs. inspectable.** SpyneJS exists to make a frontend legible — to answer, by reading structure rather than running the app, what owns a region, what can reach it, what responds, and what else a change could touch. Every reshaping below serves one payoff: **a change's blast radius can be described before the change is made.** When a choice is ambiguous, the SpyneJS answer is the one that keeps structure, behavior, and effect visible.

## The frame at a glance

The whole frame, one line each; every section expands one. Return here mid-reasoning to re-grip it.

- Reason **browser-platform-first** — no React/Vue/Angular/Svelte priors; they're contrast, not translation.
- Every view belongs to one **lifecycle tier** — who governs its existence: Persistent, Page, or PageItem.
- **VBL spine**: View (ViewStream), Behavior (Channel), Logic (SpyneTrait) — and **behavior is primary.**
- Views are **isolated** DOM-region owners; all view-to-view communication flows through Channels.
- **Real DOM, no virtual DOM, no reconciliation**; lifecycle is structural, riding the observable chain.
- **One uniform envelope** — `{ action, payload, srcElement, event }` — across UI, route, window, fetch; "the envelope" wraps "the payload data."
- Interactivity is **declared, not wired**; `props.channels` declares only what a view *listens* to.
- Fan-out is **by action-label + filter, not by channel** — reach requires label match *and* filter admit.
- Behavior lives in **Channels and the traits composed into them**; logic stays out of views.
- Channels are **persistent, composable, RxJS-backed services**; combining them is primary work.
- A channel's keystone job is **conform** — shape data + filterable flags + action label into the payload, then re-emit.
- The **DOM is meaningful structure**, not disposable output.
- Two registers: **structural-encoding** edits carry traceable reach; **pure-prior** edits have zero reach.

## Orientation: don't translate

Do not interpret SpyneJS through React, Vue, Angular, or Svelte. Reasoning that begins by translating a concept into a component, hook, directive, or reactive declaration is wrong before it starts — the thing being translated doesn't exist here. Begin from the browser platform itself — HTML, the DOM, events, lifecycle, layout — and let SpyneJS reshape those primitives.

## Who governs existence: the lifecycle tiers

Before asking what kind of thing a view is, ask **who decides when it exists.** Every view belongs to exactly one of three tiers, and the answer shapes everything downstream:

- **Persistent** — app-governed: appended at scaffold (header, footer, drawer, modal/toast hosts, invisible behavior views), never disposed. Long-lived subscriptions and replay semantics concentrate here.
- **Page** — route-governed: rendered/disposed or shown/hidden on route location. The governor is fixed; the mechanism (dispose vs. hide) is per-view. Disposal is typically the single-active-child pattern — the parent only adds; each page removes itself on the governing event.
- **PageItem** — parent-governed: existence rides the parent's disposal cascade. A pageItem may listen to routes for *content*, never for its own *existence*. Self-termination is allowed (a toast's timeout, a modal's close) — the parent's cascade still bounds it.

The taxonomy is total: transient views (modals, toasts) are parent-governed children of persistent hosts, with self-termination as an early-exit clause, not a governance transfer. This question — tier first — precedes archetype and record selection in every generation.

## VBL: the spine

A browser app looks like a content-display system but is really a behavior-and-data integration system that *displays* content as a consequence. Because behavior is primary, it gets a first-class home rather than being scattered across the views it touches. Three layers, mapping onto things you already understand:

- **View** — the visible interface structure. Primitive: the **ViewStream**, which owns one DOM region rooted at a single element.
- **Behavior** — timing and flow: when things happen, how information moves. Primitive: the **Channel**, an RxJS Subject wrapped in SpyneJS conventions.
- **Logic** — reusable computation: formatting, shaping, decisions, validation. Primitive: the **SpyneTrait**, composable methods bound into ViewStream or Channel instances.

These aren't interchangeable containers — each class is constrained to its layer's capabilities, so separation of concerns is enforced by the framework, not left to discipline. A ViewStream *cannot* quietly become a logic dump; logic lives in traits because that's the only place it can. RxJS (streams, observable coordination) and Ramda (functional composition) are the conceptual influences — you needn't write either directly, but their ideas explain the framework's shape. In the pure register (below), the house style is ordinary native JavaScript: library dialects only where genuinely load-bearing.

## The reshapings

Each item is a place your default web-development instinct points the wrong way.

### Views are isolated

No ViewStream knows another exists — no parent or child references, no registry, no view calling another's method. This is the sharpest break from the component tree. **All communication between views flows through Channels**; proposing a ref, a registry, or a direct call is proposing something the framework doesn't have. Isolation is what makes a view's blast radius knowable — a change inside an isolated view can't reach another instance. (A view doesn't even recognize its own emissions returning through a channel without an explicit filter — identity is never implicit.)

### Lifecycle is structural, not reconciled

No virtual DOM, no diffing, no re-running render against a previous tree — drop the reconciliation model entirely. Lifecycle rides an observable chain: each ViewStream owns an anonymous self-observable, and nesting exchanges parent/child *context*, not handles — a parent holds a merged anonymous stream of itself and its descendants while knowing nothing about any of them as instances. Disposal cascades depth-first (children first, up to the initiator); with no external references retained, disposed views become GC-eligible at once. This is why total isolation and unit-disposal coexist — one mechanism produces both. A view exists in one of **four modes**: rendered (default), hidden (CSS, behavior live), null-appended (behavior without presence), or adopted (`{el}` — joined to a pre-existing element; adoption is ownership *transfer*, and disposal removes the adopted tree like any rendered one). The consequence to carry: a view's creation, attachment, and teardown are part of what it *means*. A solution that leaks a subscription, orphans DOM behavior, or attaches an unmanaged effect is malformed, because lifecycle here is the structure, not a hook bolted onto it.

### Behavior is one primitive, one signature

Every meaningful event — a user interaction, a route change, a browser event, a returning fetch — arrives as the same shape on a named channel: **the envelope** — `{ action, payload, srcElement, event }`. Two tiers, two names: the envelope, and **the payload data** (the inner `payload` object — for UI broadcasts, the element's dataset, read live at event time). Both tiers legitimately carry an `action`: the envelope's is the channel action label; a dataset `action` nests at `payload.action`. The `event` tier is a conformed safe subset of the native event. Your instinct says a click handler, a router callback, and a fetch `.then` are three different kinds of thing; here they're one — a payload on a channel — and that uniformity is what lets behavior be named, routed, filtered, and inspected as a single system.

Three channels exist before you write any code, registered automatically at init: **CHANNEL_UI** (declared DOM events from every view), **CHANNEL_ROUTE** (navigation and history as data — the URL conformed into route data), and **CHANNEL_WINDOW** (global browser events configured at init). Custom and fetch channels are registered explicitly. Payloads are immutable frozen envelopes — a subscriber that needs to mutate works on a clone.

Fetch isn't special either. A **ChannelFetch** takes the usual fetch parameters plus a map that conforms the returned data, and the result enters the application as a payload, not a resolved promise handled at the call site. The strong prior being overridden is `fetch().then(data => handle(data))` — that external data resolves *to you*, inline. In SpyneJS it resolves *into the channel system*, conformed to the same signature and subscribed to like any other behavior.

### Interactivity is declared, not wired

SpyneJS never attaches a handler imperatively — no `addEventListener` in application code, no inline `onClick`. A view *declares* which of its DOM events broadcast and which channel actions it listens for (and which method each maps to); the framework does the wiring. Stop thinking "find the element, attach the handler"; think "declare what fires, declare what listens, let the framework connect them." A channel is a firehose carrying every declared event of its kind from every live view; a listener narrows it **by action-label, optionally by a payload-data property — reach requires both.** Note the asymmetry: `props.channels` declares only what a view *listens* to, never what it emits.

### Behavior lives in Channels and their traits

Because interactivity is declared, the method that runs when an event fires lives in a **SpyneTrait**, not the view. This is enforced at the structural edge: `broadcastEvents`, `addActionListeners`, `onRendered`, and the constructor are the *only* methods a ViewStream class carries — the wiring surface is ViewStream-level, and everything else is a trait. To learn what happens on an interaction, you don't read the view's markup; you follow the declared action to its trait method.

A Channel is not a passive bus. It holds its own traits, runs lifecycle hooks, processes input, and shapes what it emits — and its keystone job is to **conform**: shape incoming data, filterable flags, and an action label into the uniform payload before re-emitting. Channels are **RxJS underneath** (Subject/ReplaySubject via `this.observer`); the idioms ride on top, and raw RxJS is the sanctioned escape hatch when they don't reach. `sendChannelPayload` is `observer.next()` in a sealed signature. Channels are **persistent — there is no delete mechanism**; idle until engaged, they are the designed home for long-lived state, so **state machines and logic live in Channels via composed trait methods** — never in a view, since nothing durable persists in a ViewStream instance (durable state lives in a Channel or SpyneAppProperties).

Coordination splits by tier into **two dedicated traits**: a ViewStream trait *transmits* into a channel (`sendInfoToChannel`), and a Channel trait *acquires* (`getChannel`), conforms, and re-emits. The asymmetry is load-bearing: **a Channel cannot push an action into another channel** — it reaches others only by subscribing (`getChannel`), merging, or deriving. Bridging a channel's *output* back into a transmit therefore requires a ViewStream (the operation that does this belongs to the operations reference). And **combining channels is primary work** — gating UI on whether data has arrived, merging a route change with a fetch, timing emissions so the app stays coherent. The question is usually "how do these channels combine," not "where do I store this state." The general form: **a domain channel is a state machine** — trait methods combine event channels (route, UI, window) with data acquisition (a held collection, a merged fetch, or ChannelFetchUtil in the trait), resolve and conform per event, and deliver finished payloads. Views only ever receive.

### The DOM is meaningful structure

Not throwaway output a reconciler regenerates — part of the application's readable surface. Selectors, dataset attributes, semantic elements, and view boundaries carry behavioral, routing, styling, accessibility, testing, and inspection roles; the framework auto-tags rendered elements so a view can address regions inside itself without holding DOM references. So don't casually rename, wrap, flatten, or relocate elements — a DOM change is a structural change. A small one may well be safe, but safe *because you checked what roles the element served*, not because markup is assumed disposable.

### Two registers: structural encoding vs. pure prior

A SpyneJS codebase is written in two registers, and knowing which you're editing is how you know where to look for effects.

*Structural encoding* is everything the framework reads as structure: `index.js`, Channel and ViewStream instances, their props, wiring declarations, registrations — and, crucially, structural work *inside trait methods* (rendering or nesting a view, modifying an instance, parsing channel data, combining channels, timing a `sendChannelPayload` at a synchronization point). The register is set by what the code *does*, not which file it lives in. You edit structure confidently and well; what it demands is not caution but *awareness of reach* — a structural edit can have effects beyond itself, in knowable ways. HTML templates sit just inside this side: they're a SpyneJS mustache form with a bound surface the framework reads, so editing a template's bound fields is a structural edit even though the surrounding markup is ordinary.

*Pure prior* is code that carries no SpyneJS structure and reaches nothing past its own boundary: SCSS modules, and the self-contained computation inside trait methods (formatting, shaping, validation — input to output, no framework touch). Here your raw web-development priors apply directly and a pure-prior edit's blast radius is trivially zero. Pure-register code is written in ordinary native JavaScript and is independently testable — a pure trait method runs framework-free, and may even be invoked unbound as a plain function. So the line doesn't run cleanly between files — it runs *through* them, often through a single trait method, separating the framework-touching operations from the self-contained computation.

## Why the trace is possible

Each VBL layer is independently hierarchical, and you operate at any level of each: views nest into a disposal tree (render or dispose a leaf, a subtree, or the root); payloads fan out across a composed channel or narrow to a single listener; a trait binds to one consumer or composes into many. That macro-to-micro addressability *is* the expressiveness — and the mechanism is **composition, not inheritance**: traits compose into ViewStreams and Channels, Channels into refined Channels. You already know the shape from the C in CSS: an effect propagates predictably along a hierarchy *because* the hierarchy is explicit; SpyneJS generalizes that to all three layers (each cascade runs along one layer, never across the three orthogonal concerns). Because each hierarchy is explicit and structural rather than runtime-buried, effects propagate traceably — which is what makes the dependency graph and side-effect reporting computable at all.

You author a module by extending one of six public base classes — ViewStream, Channel, SpyneTrait, DomElement, ChannelFetch, SpynePlugin — exactly once. Richness comes from breadth (composing many traits and channels), not depth; inheritance beyond that single extension is an anti-pattern. The reason is opaque-vs-inspectable again: deep inheritance is opaque — to know what a method does you walk the chain — while composition is inspectable, because the traits and channels a module composes are declared in its props, readable in place.

## What this buys you

Every reshaping converges on one property: **the blast radius of a change can be described before the change is made** — because views are isolated, behavior flows through enumerable named channels, logic sits in identifiable traits, lifecycle is structural, and the DOM carries declared meaning. The structural-vs-prior line is how you know *where to look*: a pure-prior edit's reach is settled the moment you place it there; a structural edit is where reach becomes a live question, answered by tracing the network the edited structure participates in. The skill is not avoiding structural edits — you make those confidently and well — it's making the edit *and* knowing whether its effects extend past what was asked. That single property — stating what a change touches before touching it — is what lets an AI show its work rather than guess.

Generation follows the entry protocol in `00` — DEFINE, RESOLVE, TABLE, BUILD-NOVEL — with this document as the frame those steps assume. So reason structurally before reaching for code: understand the user-visible intent, find the view that owns the affected region, trace the behavior or event path that drives it, identify the reusable logic, account for lifecycle and cleanup, consider what else subscribes to the same channel, and choose the smallest explicit change that satisfies the request. The other documents — operations reference, construction record, API surface — are depth reached through this frame; with it installed, they read as one coherent system.
