### choose-merge-emission-mode
`op:choose-merge-emission-mode` · standard · CHOOSE

mergeChannels(channelsArr, emitOnce): each emission is a keyed object — one key per entry (string entries keyed by channel name; observables by resolved name or channel_<index>), value = that channel's full ChannelPayload (read as e['CHANNEL_X'].payload). emitOnce=true (default): emits once when all sources have emitted, then completes — a snapshot, the natural render gate. emitOnce=false: emits continuously on any source update, but only once every source has emitted at least once (combineLatest semantics). Choose by 'wait for all' vs 'track all'.

**Prior override:** Naive prior tracks arrival with boolean flags and manual checks, and expects a single latest payload rather than a keyed bundle. The mode parameter IS the coordination semantics, and BOTH modes gate on full presence — no partial-bundle handling is ever needed.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Snapshot mode live: the meme channel's conform-and-emit gates on both fetches — merge completion IS the sync point (time-emission-at-sync-point, channel-side).
**Refs:** ref:Channel.mergeChannels

**Caveats:**
- EMISSION SHAPE: keyed object — channel names as keys, full ChannelPayload envelopes as values, consumed as e['CHANNEL_X'].payload.

