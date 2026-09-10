### optimistic-update-with-reconcile
`record:optimistic-update-with-reconcile` · standard

**Recognize when:** "update the UI immediately, sync with the server after" — likes, toggles, inline edits that can't wait for the round trip.

User action applies provisional state immediately; the server round-trip reconciles it — confirm, roll back via inverse, or supersede — under deliberately chosen concurrency semantics.

**Composes:** op:select-concurrency-operator, op:provisional-state-with-inverse, op:action-reconciliation-identity, op:typed-reconciliation-outcome
