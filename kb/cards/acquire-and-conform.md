### acquire-and-conform
`op:acquire-and-conform` · core · FORM

Inbound cross-channel dependency: a Channel acquires another channel's stream via getChannel(name, payloadFilter?) in onRegistered, conforms, and re-emits under its own registered action label.

**Prior override:** Naive prior passes data via props/callbacks or imports a shared store. The SpyneJS move is subscribe, conform, re-emit — the dependency becomes a readable structural edge.

**Example** _(from spyne-3js)_:
```js
static threejsChannel$AddUIChannel() {
  const uiActions = ['CHANNEL_UI_MOUSEDOWN_EVENT', 'CHANNEL_UI_MOUSEUP_EVENT',
    'CHANNEL_UI_TOUCHSTART_EVENT', 'CHANNEL_UI_TOUCHEND_EVENT'];
  const uiFilter = new ChannelPayloadFilter('#threejs', {
    action: (str) => uiActions.indexOf(str) >= 0,
  });
  this.getChannel('CHANNEL_UI', uiFilter)
    .subscribe(this.threejsChannel$OnMouseEvent.bind(this));
}

static threejsChannel$OnMouseEvent(e) {
  const start = /(START|DOWN)/.test(e.action);
  this.sendChannelPayload(start ? 'CHANNEL_THREEJS_START_ANIMATION_EVENT'
    : 'CHANNEL_THREEJS_END_ANIMATION_EVENT', {});
}
// acquired in onRegistered; input-modality differences die here —
// consumers know only domain vocabulary
```
**Refs:** ref:Channel.getChannel, ref:Channel.sendChannelPayload, ref:Channel.onRegistered
