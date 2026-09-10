### cross-view-selection-sync
`record:cross-view-selection-sync` · standard

**Recognize when:** "selecting here should update there," "two widgets that stay in sync," "linked dropdowns."

Two or more sibling views stay in sync on a shared selection without knowing each other exists — all coordination through a selection channel.

**Composes:** op:transmit-into-channel, op:acquire-and-conform, op:register-channel-action-vocabulary, op:recognize-own-emission, op:admit-by-payload-filter, op:state-machine-in-channel, op:design-action-label-vocabulary, op:choose-replay-semantics
