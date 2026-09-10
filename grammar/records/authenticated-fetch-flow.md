### authenticated-fetch-flow
`record:authenticated-fetch-flow` · standard

**Recognize when:** "API calls need the auth token," "refresh the token when it expires," "log out on 401."

Requests carry auth state; expiry outcomes trigger refresh or redirect; token placement decided between SpyneAppProperties and a session channel.

**Caveats:**
- Error surface now grounded: 401 handling filters {CHANNEL_NAME}_ERROR_EVENT on errorType FETCH_HTTP_ERROR + status; the refresh-then-retry loop likely needs the bridge op. Mind the cached-error hazard for late subscribers.

**Composes:** op:spyneappproperties-vs-channel-state, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:error-as-conformed-payload, op:bridge-channel-output-to-transmit, op:typed-reconciliation-outcome, op:route-as-data
