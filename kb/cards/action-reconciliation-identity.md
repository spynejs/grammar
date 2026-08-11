### action-reconciliation-identity
`op:action-reconciliation-identity` · standard · FORM

Tag an outbound action with an identity so its returning result reconciles to the originating emission, not just to a label.

**Prior override:** Naive prior assumes responses map to requests implicitly (closure over the promise). In a channel system nothing is implicit — identity must ride the payload.

**Example** _(from canonical)_:
```js
const responseSub = this.getChannel(this.props.serverTestConstants.FETCH_CHANNEL)
  .pipe(
    filter((e) => e?.payload?.actionId === intent.actionId),
    take(1),
  )
  .subscribe((e) => {
    // reconcile THIS intent's response — no other response can match
  });
// take(1): the subscription completes itself after its one response
```
**Refs:** ref:ChannelPayload.constructor, ref:ChannelPayloadFilter.constructor
