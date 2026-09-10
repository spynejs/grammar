### drag-reorder-with-persist
`record:drag-reorder-with-persist` · standard

**Recognize when:** "drag to reorder," "sortable list that remembers its order."

Drag-and-drop reordering (drag events via CHANNEL_UI or CHANNEL_WINDOW) applied optimistically, persisted to the server, reconciled on the round-trip.

**Composes:** op:declare-broadcast-events, op:dataset-as-payload, op:admit-by-payload-filter, op:author-dom-with-declared-roles, op:address-region-by-el$, record:optimistic-update-with-reconcile
