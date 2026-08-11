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

