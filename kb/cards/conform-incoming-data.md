### conform-incoming-data
`op:conform-incoming-data` · core · FORM

The channel's keystone act: shape incoming data + filterable properties + registered action label into the uniform ChannelPayload before re-emitting via sendChannelPayload(action, payload, srcElement?, event?).

**Prior override:** Naive prior forwards raw fetch/event data and lets each consumer shape it. Conform once at the channel boundary; consumers rely on the uniform envelope.

**Example** _(from spyne-toh)_:
```js
static tohChannel$SendRouteChangeEvent(e) {
  const { pageId, id } = e.payload.routeData;
  const heroesArr = this.tohChannel$GetPageData({ pageId, id });
  const msg = this.tohChannel$GenerateMessage({ eventType: 'fetch', id });
  this.sendChannelPayload('CHANNEL_TOH_ROUTE_EVENT', { pageId, id, msg, heroesArr });
}
// shape data + filterable properties under a registered label, once, at the
// channel boundary — consumers rely on the uniform envelope
```
_modernized: dropped specimen's console.log_
**Refs:** ref:Channel.sendChannelPayload, ref:ChannelPayload.constructor, 01:behavior-lives-in-channels-and-their-traits

**Caveats:**
- VOCABULARY CONVENTION (corpus-wide): 'the ENVELOPE' = ChannelPayload {action, payload, event, srcElement}; 'the PAYLOAD DATA' = the inner payload object (for UI broadcasts: the element's dataset). Both tiers legitimately carry an 'action'; the two-name convention removes the ambiguity.
- Envelope event tier: the event object is a conformed SAFE SUBSET of the native event (value, coordinates, dimensions, target, ...) — circular references excluded by construction; all captured values are filterable.
- Channel-side srcElement: ChannelFetch emissions carry the CHANNEL'S identity as srcElement ({name, url, ...}) — the tier repurposed for non-DOM sources.

