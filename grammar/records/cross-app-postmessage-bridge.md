### cross-app-postmessage-bridge
`record:cross-app-postmessage-bridge` · standard

**Recognize when:** "talk to the iframe," "two apps on the page share events," "embed communicates with host."

Two SpyneJS applications in separate realms (host + embedded iframe app) communicate over postMessage: one-time handshake via a temp prop, then channel payloads bridged across the boundary — serializable by construction — so consumers in either app subscribe to the remote app's behavior like any local channel. The native micro-frontend composition.

**Composes:** op:handshake-via-temp-prop, op:conform-incoming-data, op:register-channel-action-vocabulary, op:error-as-conformed-payload, op:state-machine-in-channel, op:admit-by-payload-filter
