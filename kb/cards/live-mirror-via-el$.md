### live-mirror-via-el$
`op:live-mirror-via-el$` · standard · FORM

Ephemeral display mirroring (an input's in-progress value reflected in a heading) is an el$ DOM mutation driven by the input broadcast — no channel state, no re-render, the value held nowhere but the input element itself. Durable propagation happens separately, on the commit action (save).

**Prior override:** The two-way-binding prior (ngModel, controlled inputs) manufactures state for what is purely cosmetic reflection. Ephemeral display state needs no state: broadcast input → el$('#target').el.innerText. State enters only at commit.

**Example** _(from spyne-toh)_:
```js
static tohPage$UpdateDetailsHeroLabel(e) {
  const inputStr = e.srcElement.el.value;
  this.props.el$('#hero h2').el.innerText =
    `${String(inputStr).toUpperCase()} Details`;
}
// input broadcast → el$ mutation; the value lives nowhere but the input
// element itself — state enters only at the commit action (save)
```
**Refs:** ref:ViewStream.el$, ref:ViewStream.broadcastEvents

**Caveats:**
- Companion pattern RULED sanctioned-for-now: commit → window.history.go(-1) → route event rebuilds prior page from mutated channel state ('navigate-to-refresh'). History updates are not yet framework-addressed; planned declarative forms: (a) anchor data-channel="ROUTE" data-route-history="-1"; (b) sendInfoToChannel('CHANNEL_ROUTE', {history:-1}, 'CHANNEL_ROUTE_HISTORY_UPDATE_REQUEST_EVENT'). When either ships, raw history.go becomes legacy.

