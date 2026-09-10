### toast-notification-system
`record:toast-notification-system` · standard

**Recognize when:** "show a toast/snackbar," "brief confirmations that dismiss themselves."

App-wide ephemeral notifications: a toast channel receives requests, a host view renders toast views that self-dispose on timeout or dismissal.

**Caveats:**
- Tier ruling: persistent ToastContainer host; toasts are self-terminating parent-bounded children.

**Composes:** op:state-machine-in-channel, op:register-channel-action-vocabulary, op:nest-view-without-handle, op:dispose-as-unit, op:escape-to-raw-rxjs, op:transmit-into-channel, op:skip-replayed-birth-event, op:choose-replay-semantics
