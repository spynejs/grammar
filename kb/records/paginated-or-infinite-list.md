### paginated-or-infinite-list
`record:paginated-or-infinite-list` · standard

**Recognize when:** "load more," "page 2," "infinite scroll," "only fetch what's visible."

List that loads pages on demand (button or scroll threshold via CHANNEL_WINDOW with debounce), appends item views, and never double-fires a page request.

**Composes:** op:window-event-via-channel, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:select-concurrency-operator, op:nest-view-without-handle, op:time-emission-at-sync-point, op:state-machine-in-channel, op:domelement-vs-viewstream
