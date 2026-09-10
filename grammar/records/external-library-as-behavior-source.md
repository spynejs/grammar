### external-library-as-behavior-source
`record:external-library-as-behavior-source` · standard

**Recognize when:** "integrate Three.js / a map / a player / a socket" — a library with its own events joining app behavior.

A third-party library participates in application behavior by EMITTING, not owning control: one ViewStream owns the library's DOM region; the library's objects live in the trait; continuous/native library events are discretized at source and transmitted onto a dedicated domain channel; the channel translates acquired framework events (UI/WINDOW) into domain actions (lookup hash — mouse and touch unify to one action; device modality dies at the channel); consumer views react by domain label with no reference to the library or its view. CUSTODY (ruled): library objects live on props by default — props is GC-significant, disposal reaches it; trait instance fields are a sanctioned convenience ONLY when the owning view is persistent-tier (never disposed). A disposable view integrating a library must carry its machinery on props or leak.

**Composes:** op:decompose-region-into-viewstreams, op:discretize-continuous-input-at-source, op:transmit-into-channel, op:acquire-and-conform, op:register-channel-action-vocabulary, op:use-framework-ui-action-labels, op:single-active-child, op:clone-frozen-payload, op:window-event-via-channel
