### gate-render-on-data
`record:gate-render-on-data` · standard

**Recognize when:** "don't render until the data is ready," "wait for both requests before showing."

Render a view (or subtree) only when its data dependencies have arrived — mergeChannels with emitOnce=true (snapshot: emits once when all sources have emitted, then completes) as the render trigger.

**Caveats:**
- CAVEAT (empirically proven, Acme): take(1)-style merge-gating FREEZES route context — if a redirect (or any meaningful re-emission) can intervene before render, the frozen first value is stale. Gate on all-sources-present with latest-value semantics; take(1) only when sources are genuinely immutable for the view's lifetime.
- Companion ruling (Acme): render-once is achieved by narrowing the pipeline + branching on held state — never by a parallel rendered-flag.

**Composes:** op:choose-merge-emission-mode, op:choose-derived-vs-merged-channel, op:time-emission-at-sync-point
