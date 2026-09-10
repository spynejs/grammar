### single-active-child
`op:single-active-child` · core · FORM

Route-tier (and analogous) swapping via the single-active-child pattern: the parent container instantiates the incoming child; the CHILD removes itself on the governing event (['CHANNEL_ROUTE_CHANGE_EVENT','disposeViewStream'] + skip-first). Parent never tracks or disposes outgoing children.

**Prior override:** Naive prior has the parent manage the swap: hold the current child, dispose it, mount the next. Here disposal is distributed — each child carries its own exit, the parent only ever adds.

**Example** _(from canonical-app)_:
```js
// parent: only ever adds the incoming child
static stage$OnRouteEvent(e) {
  this.appendView(new PageView({ data: e.payload }), '.page-container');
}

// child: carries its own exit
addActionListeners() {
  return [['CHANNEL_ROUTE_CHANGE_EVENT', 'disposeViewStream']];
}
// the parent never tracks or disposes outgoing children
// child declares [['CHANNEL_ROUTE', true]] — see skip-replayed-birth-event
```
**Refs:** ref:ViewStream.disposeViewStream, ref:ViewStream.addActionListeners, 01:lifecycle-is-structural-not-reconciled

**Caveats:**
- TIER SCOPE (Acme error, logged): this is a PAGE-tier (route-governed) pattern. Generalizing it down to parent-governed pageItems creates ordering problems that then attract spurious fixes — the observed failure chained skip-first onto an ordering bug the generalization itself caused.

