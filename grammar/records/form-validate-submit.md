### form-validate-submit
`record:form-validate-submit` · standard

**Recognize when:** "a contact/signup form," "validate before submitting," "show errors next to fields."

Form with field-level validation (pure-prior computation in a trait), declared submit broadcast, paused ChannelFetch submission triggered by REQUEST_EVENT, typed outcomes.

**Composes:** op:declare-broadcast-events, op:author-in-correct-register, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:error-as-conformed-payload, op:typed-reconciliation-outcome, op:clone-frozen-payload, op:shape-data-for-logicless-template
