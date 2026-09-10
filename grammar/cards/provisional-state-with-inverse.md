### provisional-state-with-inverse
`op:provisional-state-with-inverse` · standard · FORM

Apply a provisional (optimistic) state change while recording its inverse, so rollback is a structural application rather than a re-derivation.

**Prior override:** Naive prior applies the optimistic change with no structural undo path, then re-fetches or re-computes on failure. Record the inverse at apply time.

**Example** _(from canonical)_:
```js
static channelServerReconcile$applyOptimistic(intent) {
  const key = this.channelServerReconcile$key(intent);
  const value = this.channelServerReconcile$valueOf(intent.resource, intent.data);

  intent.prevValue = this.props.reconcileState[key];  // capture the inverse
  this.props.reconcileState[key] = value;             // apply optimistically
}
// the inverse rides the intent — rollback needs no other lookup
```
_modernized: payload→data field rename applied_
**Refs:** 01:behavior-lives-in-channels-and-their-traits
