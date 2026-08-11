### combine-sources-into-domain-payload
`record:combine-sources-into-domain-payload` · standard

**Recognize when:** "needs data from two places before it can show," "merge these feeds into one thing."

Multiple independent data sources combined into one domain event: per-source ChannelFetch instances (each with its own conform map); a custom channel mergeChannels them in onRegistered (snapshot: emits when all sources have), extracts and conforms the constituents into ONE flat domain payload, and emits under its registered action; consumers receive the combined result with no knowledge of the sources.

**Composes:** op:fetch-as-channel, op:fetch-conform-map, op:choose-merge-emission-mode, op:conform-incoming-data, op:wire-in-onRegistered, op:register-channel-action-vocabulary, op:choose-replay-semantics, op:time-emission-at-sync-point, op:domelement-vs-viewstream
