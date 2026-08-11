### pause-fetch-vs-autofire
`op:pause-fetch-vs-autofire` · standard · CHOOSE

ChannelFetch fires on creation unless pause=true. On-demand or repeat fetching is triggered via sendInfoToChannel with the derived {CHANNEL_NAME}_REQUEST_EVENT action (the generic CHANNEL_FETCH_REQUEST_EVENT label is also registered).

**Prior override:** Naive prior constructs the request at the moment of need. The channel exists up front (boot data: autofire; on-demand: paused); the request is an action, not a construction.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_
**Refs:** ref:ChannelFetch.constructor, ref:ViewStream.sendInfoToChannel

**Caveats:**
- CLOSED: request-time parameters ride the REQUEST_EVENT payload. The following values can be sent to update the ChannelFetch parameters upon new request: ['map', 'url', 'header', 'body', 'mode', 'method', 'responseType', 'debug'].

