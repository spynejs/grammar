### dynamic-children-ingress
`op:dynamic-children-ingress` · standard · FORM

broadcastEvents binds snapshot-direct: the selector is scoped to the view root, the listener attaches to each matched interactive element (which becomes the payload's srcElement), and elements rendered AFTER binding are not covered. Two sanctioned recipes for dynamic children: (1) DEFAULT — render dynamic children as nested ViewStreams, each declaring its own broadcastEvents at its own render (code closest to what it controls; binding rides the child's lifecycle); (2) ALTERNATIVE — add the event to the Window Channel and narrow with payload filters to the desired root, i.e. delegation at the framework's designed global tier rather than an ad-hoc container.

**Prior override:** The naive fix is manual delegation: broadcast a static container and resolve the clicked child from the event. Mechanically broken in-idiom — the payload's srcElement and dataset belong to the BOUND element, never the root (unless the root is the selector), so container binding returns the container's dataset and severs dataset-as-payload for exactly the per-child data it exists to carry. Delegation, when needed, goes through CHANNEL_WINDOW + filters, not an improvised container listener.

**Example** _(from spyne-ttt-canonical)_:
```js
// parent renders dynamic children as nested ViewStreams
if (addMoveBtn) {
  this.appendView(new TicTacToeMoveBtn({ moveNum }), 'ol');
}

// each child declares its own events at its own render
broadcastEvents() {
  return [['button', 'click']];
}
// broadcastEvents binds post-onRendered; children rendered later carry
// their own declarations, so binding rides the child's lifecycle
```
**Refs:** ref:ViewStream.broadcastEvents, ref:SpyneApp.config.window, ref:ChannelPayloadFilter.constructor, 01:interactivity-is-declared-not-wired

**Caveats:**
- Recipe fork judgment: nested ViewStreams when children carry behavioral/lifecycle weight (the best-practice default); window-channel delegation when a ViewStream per child is disproportionate.

