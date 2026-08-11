### mint-channel-vs-ride-existing
`op:mint-channel-vs-ride-existing` · standard · CHOOSE

Decide whether a feature needs its own registered channel or rides an existing one with new action labels. registerChannel enforces unique names app-wide.

**Prior override:** Naive prior creates an emitter per feature or dumps everything on one global bus. The judgment is by conform/fan-out needs: a new channel earns registration when it conforms its own data shape or serves a distinct behavioral domain; otherwise mint labels on an existing channel.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- behavior derived from the same external data or external behavior, eg, merged channels and / or UI behavior pertaining to a specific feature where logic can be shared should add actionLabels. Novel data or behavior merits its own Channel.
- THRESHOLD BRACKETED by the comparison pair: spyne-ttt-canonical MINTS (durable shared state, replay for late subscribers, typed outcome labels, board↔move-list coordination); spyne-todos RIDES CHANNEL_UI (per-item ephemeral state in each item's data, zero cross-item coordination, edit-mode as class toggle). Two similar-sized apps, one per branch — interpolate between them.
- Upgrade path when the threshold is crossed: a trait's fn-lookup dispatch (todos$onItemEvent actionsFnLookup) IS the embryonic action vocabulary — minting the channel converts payload-dispatch to label-dispatch mechanically.
**Refs:** ref:SpyneApp.registerChannel, ref:Channel.constructor

**Caveats:**
- Below the threshold, per-item content state on the item's own props.data (mutated in place) is sanctioned — the no-channel branch's state placement, per the todos specimen.

