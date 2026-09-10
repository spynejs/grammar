### modal-open-close
`record:modal-open-close` · standard

Modal rendered as a disposed-by-default subtree, opened/closed via channel actions (and optionally route), with escape-key handling via CHANNEL_WINDOW.

- Specimen: the transient-host pattern — a persistent-tier host view owns modal existence; the modal itself is parent-governed with self-termination (close/confirm/Escape) as the early-exit clause, never a governance transfer.
- Dispose is the default close (dispose-vs-hide): Cancel/Escape leaves zero modal DOM — hidden modals accumulate stale state and listeners.
- Open rides the UI channel: any element with the right dataset opens it (data carries intent + context ids); confirm transmits a semantic action into the owning domain channel — the modal never performs the action itself.

**Caveats:**
- Tier ruling: a persistent ModalContainer hosts; the modal is its self-terminating child (see assign-view-lifecycle-tier).

**Composes:** op:declare-action-listeners, op:nest-view-without-handle, op:dispose-as-unit, op:dispose-vs-hide, op:window-event-via-channel, op:skip-replayed-birth-event