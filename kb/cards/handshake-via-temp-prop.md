### handshake-via-temp-prop
`op:handshake-via-temp-prop` · scaffold · FORM

One-time secrets (handshake tokens, nonces, single-consumer handoffs) are stored as SpyneAppProperties temp props (isTemp=true): removed on first read, so exactly one reader can consume the value and later readers find nothing. Designed for the authenticated handshake between separate SpyneJS applications communicating over postMessage.

**Prior override:** Naive prior parks tokens in module globals, window properties, or long-lived state — readable by any code, any number of times, for the lifetime of the app. Read-once is a security property expressed as data lifecycle; consumption IS revocation.

**Example:** _pending — specimen (secure postMessage plugin) not in the extraction workspace; follow-up mini-run when supplied._
**Refs:** ref:SpyneAppProperties.setProp, ref:SpyneAppProperties.getProp
