### choose-replay-semantics
`op:choose-replay-semantics` · core · CHOOSE

A Channel's replay prop (set at construction) decides Subject vs ReplaySubject — whether late subscribers receive the last cached payload. Decide per channel by whether its state is 'current value' (replay) or 'ephemeral event' (no replay).

**Prior override:** The naive prior has no equivalent concept, so the model never asks the question — and defaults silently to whichever behavior it assumes. Replay is a deliberate, per-channel design decision with direct consequences for every future subscriber.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Both branches now specimened: replay=true (ttt, localStorage, canonical app) vs deliberate no-replay (meme-gen: one-shot merge result late subscribers shouldn't inherit).
**Refs:** ref:Channel.constructor


BUFFER SEMANTICS (empirical): replay is PER-CHANNEL — one ReplaySubject(1) buffer for the whole channel; every action must carry complete state; late subscribers get only the single latest payload.

**Caveats:**
- Deprecated alias in wild code: sendCachedPayload (same semantics). Never emit; recognize when reading.
- Companion pattern (spyne-ttt-canonical): replay channels SEED their cache at onRegistered (SendCurrentState()) so the first subscriber receives state before any interaction — replay + initial emission as a pair; naive prior waits for the first event and leaves early subscribers empty.

