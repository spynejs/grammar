### select-concurrency-operator
`op:select-concurrency-operator` · standard · CHOOSE

Choose the RxJS concurrency operator (switchMap/concatMap/exhaustMap/mergeMap) by the action's ordering semantics when a channel action triggers async work.

**Prior override:** Bare await / naive promise handling is an accidental mergeMap — a stale response can clobber newer state. Choose the operator deliberately from the action's ordering semantics.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Empirically proven: all four operators run against an adversarial server; mergeMap produced a wrong final state (preserved as failure fixture).
**Refs:** ref:Channel.getChannel, ref:ChannelFetchUtil.constructor
