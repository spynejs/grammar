### live-polling-updates
`record:live-polling-updates` · standard

**Recognize when:** "refresh the data every N seconds," "live scores/prices/status."

Periodic refresh of a data view: interval via raw RxJS inside a channel, fetch per tick (REQUEST_EVENT into a paused ChannelFetch), no overlapping requests, coherent emission timing.

**Composes:** op:escape-to-raw-rxjs, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:select-concurrency-operator, op:time-emission-at-sync-point, op:bridge-channel-output-to-transmit
