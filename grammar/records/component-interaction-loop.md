### component-interaction-loop
`record:component-interaction-loop` · core

**Recognize when:** any first component — "make the button update the counter," "wire this input to that list" — the full view→channel→view loop in miniature.

The complete minimal loop of one interactive component, in a single artifact: template with data-* flags → broadcastEvents declaration → the domain channel acquiring/conforming (onRegistered, ChannelPayloadFilter) → semantic action label → addActionListeners → trait method. The normative 'anatomy of a SpyneJS component' — a prescription, not a feature tour.

**Composes:** op:dataset-as-payload, op:declare-broadcast-events, op:use-framework-ui-action-labels, op:conform-incoming-data, op:admit-by-payload-filter, op:declare-action-listeners, op:behavior-to-trait-not-view, op:dynamic-children-ingress
