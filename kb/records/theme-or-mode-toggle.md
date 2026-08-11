### theme-or-mode-toggle
`record:theme-or-mode-toggle` · standard

A theme/mode toggle is a replay state channel wearing a button. Assembly: a toggle view broadcasts its click (dataset carries the target mode or a bare toggle intent); a theme channel (replay: true) holds current mode as durable state, seeded in onRegistered from the storage channel so the persisted choice applies before first paint; on change it conforms, persists via the storage channel, and emits; consumers apply the mode via el$ (root data-theme attribute / class flip) — late subscribers receive current mode immediately via replay. The mode rides the DOM as an attribute, so CSS does the theming; views only flip the signature.

- Specimen: canonical app settings/localStorage cluster — the storage channel + replay-seeded state pattern this record rides.
- Replay is the load-bearing choice: a theme channel without replay greets late views with no mode at all — the flash-of-wrong-theme bug is a missing replay, not a CSS problem.
- Persistence is delegated: the theme channel never touches localStorage directly — it transmits to the storage channel (persist-settings record), keeping storage concerns in one place.

**Composes:** op:declare-broadcast-events, op:state-machine-in-channel, op:choose-replay-semantics, op:acquire-and-conform, op:transmit-into-channel, op:address-region-by-el$