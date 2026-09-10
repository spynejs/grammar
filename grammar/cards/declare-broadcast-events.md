### declare-broadcast-events
`op:declare-broadcast-events` · core · FORM

A view declares which of its internal elements' events broadcast — broadcastEvents returns nested selector-event pairs, captured by the UI or Route Channel (fromEvent under the hood). Binding model: selector scoped to the view root; the listener attaches to each matched element (which becomes srcElement); binding is a render-time post-onRendered binding — see dynamic-children-ingress for children rendered later.

**Prior override:** Naive prior finds the element and attaches a handler (addEventListener / inline onClick). SpyneJS never attaches imperatively; declare what fires.

**Example** _(from spyne-toh)_:
```js
broadcastEvents() {
  return [
    ['button', 'click'],
    ['#hero-name', 'input'],
  ];
}
// selectors scoped to the view root; each matched element becomes srcElement
// and its dataset rides the payload
```
**Refs:** ref:ViewStream.broadcastEvents, 01:interactivity-is-declared-not-wired

**Caveats:**
- COVERAGE MODEL: post-onRendered coverage — children appended in onRendered are covered; event-time additions still need the dynamic-children recipes.
- UNIFIED CAPTURE (author): broadcastEvents captures for BOTH UI and ROUTE — the element's data-channel attribute decides the destination channel. Route links are not a separate capture mechanism.
- Bind hook: postRender — runs broadcastEvents once, after onRendered. The coverage boundary is mechanical, not conventional.
- BROWSER DEFAULT IS CHANNEL-DEPENDENT. A broadcast event on CHANNEL_UI does NOT suppress the browser's own handling — a declared `['form','submit']` runs the trait AND submits the page; a plain anchor still navigates. Declare `data-event-prevent-default="true"` on the element to suppress it. ROUTE is the opposite: the broadcaster suppresses by default, because route clicks are captured to drive the internal route structure rather than a page load; `data-event-prevent-default="false"` is the override, and only there. On both channels the attribute is read by PRESENCE, not value — the channel calls `preventDefault()` whenever the key exists — so a UI-side `="false"` still suppresses; ROUTE honors `"false"` only because the broadcaster removes the key before the channel sees it. Calling `preventDefault` inside the trait is not the remedy; the declaration is.

