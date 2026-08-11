### dispose-by-predicate-filter
`op:dispose-by-predicate-filter` · standard · FORM

A transient view can self-dispose when a channel condition STOPS holding: register ['ACTION','disposeViewStream', filter] where the ChannelPayloadFilter admits on the negative match (search term no longer contained in this item's name, or term emptied). Disposal as a subscription outcome; each stale item removes itself, no orchestrator diffs the set. Generalizes to THRESHOLD predicates: canonical tic-tac-toe move buttons dispose via payload:(v)=>v.moveNum <= this.props.moveNum — numeric condition, same distributed-exit architecture.

**Prior override:** Naive prior has a parent reconcile the result set (diff old vs new, remove stale nodes). Here reconciliation is distributed: every item carries its own exit condition, and the payload filter is the exit predicate.

**Example** _(from spyne-toh)_:
```js
addActionListeners() {
  const reFalseMatchPayloadFilter = new ChannelPayloadFilter({
    payload: (p) =>
      this.props.data.name.includes(p.searchStr) === false || p.searchStr === '',
  });
  return [
    ['CHANNEL_TOH_SEARCH_EVENT', 'disposeViewStream', reFalseMatchPayloadFilter],
  ];
}
// the payload predicate is the exit condition — each stale item removes
// itself; no orchestrator diffs the result set
```
**Refs:** ref:ChannelPayloadFilter.constructor, ref:ViewStream.disposeViewStream

**Caveats:**
- Also grounds function-predicate filters generally: ChannelPayloadFilter accepts payload:(p)=>bool and event:(ev)=>bool predicates (keyup character gating observed) — extends admit-by-payload-filter.

