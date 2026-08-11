### srcElement-over-event-target
`op:srcElement-over-event-target` · core · FORM

Read the ChannelPayload's srcElement (the framework's description of the event target: tagName, id, class) rather than walking event.target. ChannelPayloadFilter selectors match against srcElement.

**Prior override:** Naive prior reads event.target and walks the DOM. The envelope carries the resolved target description; the raw event is along for the ride, not the primary surface.

**Example** _(from canonical-app)_:
```js
static channelMenuDrawer$OnUiClick(e) {
  const isOpen = e.srcElement.el.classList.contains('open');
  this.channelMenuDrawer$SendMenuDrawerEvent(!isOpen);
}
// the envelope's srcElement is the resolved bound element — no event.target walking;
// ChannelPayloadFilter selectors match against it
```
_modernized: inlined specimen's ramda path() access as direct property reads_
**Refs:** ref:ChannelPayload.constructor, ref:ChannelPayloadFilter.constructor
