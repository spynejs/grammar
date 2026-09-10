### multi-step-wizard
`record:multi-step-wizard` · standard

**Recognize when:** "a checkout/onboarding flow," "step 1, step 2, step 3," "back and next with state kept."

Sequential steps with accumulated state, back/forward, validation gates between steps, and a terminal submit.

**Composes:** op:state-machine-in-channel, op:route-as-data, op:design-route-config-tree, op:dispose-as-unit, record:gate-render-on-data, record:form-validate-submit
