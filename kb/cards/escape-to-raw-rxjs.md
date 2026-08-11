### escape-to-raw-rxjs
`op:escape-to-raw-rxjs` · rare · GATED
**GATE:** Only when the declared idioms cannot express the timing/combination; keep the escape inside the channel trait.

When the idioms don't reach (debounce, interval, retry, custom operators), drop to the channel's obs$ — an RxJS Subject with the full library available; ChannelFetchUtil similarly wraps a fetch as a raw observable for advanced stream behaviors.

**Prior override:** Naive prior hacks around with setTimeout, flags, or polling loops in application code. The escape hatch is raw RxJS on obs$, keeping the behavior inside the channel system.
**Refs:** ref:Channel.constructor, ref:ChannelFetchUtil.constructor
