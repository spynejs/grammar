### typed-reconciliation-outcome
`op:typed-reconciliation-outcome` · standard · FORM

Conform a reconciliation result into typed outcome labels/flags (confirm, rollback, supersede) rather than a success boolean.

**Prior override:** Naive prior returns success/failure. Under chosen concurrency semantics, 'superseded' is a distinct outcome from 'failed'; the type set must carry it.

**Example** _(from canonical)_:
```js
const { status } = response;

if (status === 'confirmed') {
  state[key] = valueOf(intent.resource, response.data);      // server value
} else if (status === 'rejected') {
  state[key] = valueOf(intent.resource, response.authoritative); // server's truth
} else {
  state[key] = intent.prevValue;                             // error → inverse
}
// three typed recoveries: confirm, rollback-to-authoritative, rollback-to-inverse
```
_modernized: condensed from channelServerReconcile$reconcileResponse_
**Refs:** ref:Channel.sendChannelPayload, ref:Channel.addRegisteredActions
