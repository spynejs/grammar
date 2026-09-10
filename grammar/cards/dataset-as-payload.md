### dataset-as-payload
`op:dataset-as-payload` · core · FORM

Per-element data rides dataset attributes: a broadcast UI event's payload IS the element's dataset. Design dataset attributes as the data surface of interactive elements (and of ROUTE links). Dataset reads are LIVE, not bind-time snapshots: if a data-* value changes after broadcastEvents binding, the updated value is what rides the next payload — dataset attributes function as mutable per-element state the broadcast reflects.

**Prior override:** Naive prior captures per-element data in handler closures. Closures are invisible to structure; dataset → payload keeps the data on the inspectable path, and it's how the framework works anyway.

**Example** _(from spyne-ttt-canonical)_:
```js
// <button class="square" data-type="square" data-square-num=0></button>
// <button class="move-btn" data-type="move" data-move-num={{moveNum}}>
static gameChannel$OnBtnClicked(e) {
  const { type, squareNum, moveNum } = e.payload;
  const num = type === 'square' ? squareNum : moveNum;
  this.props.stateMachine[`${type}`] = num;
  this.gameChannel$SendCurrentState(
    `CHANNEL_TIC_TAC_TOE_${type.toUpperCase()}_CHANGE_EVENT`);
}
// the broadcast payload IS the element's dataset, read live at event time;
// data-type dispatches one listener with no handler branching
```
**Refs:** ref:ChannelPayload.constructor, ref:ViewStream.broadcastEvents, ref:SpyneApp.config.route

**Caveats:**
- RESOLVED: app-mode sanitization strips data-* only from dynamically added external content (e.g. an external HTML block with data-*) — which is an anti-pattern regardless. Datasets are typically encoded in view templates, which is the idiom; template-authored dataset payloads and data-channel ROUTE links are the supported path.
- Confirmed: auxiliary link dataset attributes ride routeData verbatim (channel, eventPreventDefault, endRoute observed).
- data-action is SAFE and idiomatic (nests at payload.action, distinct from the envelope action). The earlier shadow concern was terminological, not mechanical — resolved by the envelope/payload-data vocabulary convention.

