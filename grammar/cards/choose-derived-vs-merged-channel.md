### choose-derived-vs-merged-channel
`op:choose-derived-vs-merged-channel` · standard · CHOOSE

Pick the channel-combination form: derived (react to one channel's stream, enhance, emit own — sequential) vs mergeChannels (combine several — simultaneous) vs raw RxJS on obs$.

**Prior override:** Naive prior coordinates with ad-hoc booleans, instance flags, and manual ordering. Choose the structural combination form; 'merge' names only the mergeChannels case.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_
**Refs:** ref:Channel.getChannel, ref:Channel.mergeChannels
