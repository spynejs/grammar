### bare-metal-event-listener
`op:bare-metal-event-listener` · rare · GATED
**GATE:** Only for multi-event capture within/between paint cycles where the channel round-trip cannot keep up; explicit disposal path required.

The rare sanctioned use of raw addEventListener in application code: capturing multiple events within or between paint cycles, where content renders and disposes faster than the broadcast/channel round-trip can track and only the most minimal direct connection works. Escalation ladder: (1) default — declare-broadcast-events; (2) dynamic children — dynamic-children-ingress (nested ViewStreams, or Window Channel + filters); (3) bare metal — only for within/between-paint-cycle capture, and only with an explicit disposal path for every listener attached.

**Prior override:** Inverted from the usual: here the naive prior (addEventListener) IS the mechanism — the correction is the GATE. An agent must not reach this rung because it feels familiar; it is justified by paint-cycle timing constraints, not by convenience, and prevalence is roughly two instances across hundreds of production SpyneJS applications.
**Refs:** ref:ViewStream.broadcastEvents, ref:ViewStream.disposeViewStream, 01:interactivity-is-declared-not-wired

**Caveats:**
- Raw listeners bypass payload filters, the behavior console, and channel observability; the disposal-path requirement is what keeps the exception lifecycle-complete.

