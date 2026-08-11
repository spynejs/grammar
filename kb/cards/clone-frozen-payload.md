### clone-frozen-payload
`op:clone-frozen-payload` · standard · FORM

ChannelPayloads are immutable (frozen); a subscriber needing local mutation calls payload.clone().

**Prior override:** Naive prior mutates the event/data object in place. Frozen envelopes make mutation a silent failure or throw; clone() is the documented move.

**Example** _(from spyne-3js)_:
```js
onViewStreamInfo(vsPayload) {
  const { action, payload } = vsPayload.clone();
  this.sendChannelPayload(action, payload);
}
// envelopes are frozen; clone() before local mutation or re-emission
```
_modernized: let → const_
**Refs:** ref:ChannelPayload.clone, ref:ChannelPayload.constructor

**Caveats:**
- CMS-proxified data has its own mutation contract — see safeclone-for-proxified-data; payload.clone() does not preserve proxy metadata.

