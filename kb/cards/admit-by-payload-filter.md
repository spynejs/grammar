### admit-by-payload-filter
`op:admit-by-payload-filter` · core · MULTI-FORM

Narrow a listener at admission with ChannelPayloadFilter. MATCHING MODEL (source-grounded, test-anchored): criteria run against a merge barrel Object.assign({}, v, srcElement, event, payload) — payload spread LAST, so payload keys SHADOW envelope keys; {action: X} therefore matches payload.action when the dataset carries one, else the envelope action. FAIL-CLOSED: every declared criterion must pass; unknown keys are criteria and block. Forms: strings for action/selector (selector string or array, against srcElement); filter METHODS: any criterion's value may be a boolean-returning method receiving the value at its key — tier keys (payload/srcElement/event) receive that tier's object (compound conditions live there); bare keys receive the flattened value. String/boolean/number values compare by equality; array/object values are invalid (warn + always-false). GUIDANCE: payload matching uses a payload predicate — the string-action form is envelope matching that payload data can shadow; reliable envelope-action narrowing lives in the addActionListeners label. Debugging: { debugLabel: 'x' } logs every matching attempt with per-criterion pass/fail.

**Prior override:** Naive prior does imperative if-checks inside the handler. Filtering at admission keeps the listener's admission set declared in structure rather than buried in code. For custom/fetch channels, filter on action or payload only — event/srcElement may be absent.

**Forms:** _(inventory below; each line links to its REFERENCE example)_

- Self-scope idiom grounded (spyne-todos): each item view filters by its own birth data ({todoId: this.props.data.todoId}), template-bound into its buttons' datasets — an item admits only its own elements' events. The practical sibling of recognize-own-emission.
**Refs:** ref:ChannelPayloadFilter.constructor, ref:ViewStream.addActionListeners, ref:Channel.getChannel

**Caveats:**
- propFilters is a deprecated EARLY API — a formal wrapper for payload-tier properties, semantically identical to bare keys on the modern barrel. Agents reading older SpyneJS code read propFilters wrappers as payload-tier specs; emit bare keys only.
- RULED: payload.action overrides action (barrel-wins).
- SOURCE-CONFIRMED: reserved meta keys = selector, debugLabel, label, props, propFilters, testMode; all other keys are criteria (typo'd key → undefined test → blocks). Wrappers props/propFilters still function (mergeAll into criteria) — deprecated for authoring only. Selector also accepts an HTMLElement; matching = el.matches, any-of-array; invalid CSS warns→false. Empty filter = always-false + debug warning. debugLabel is a String (positional 3rd param or key), logging data-criteria booleans AND selector results separately. testMode returns internals for unit tests.
- STATE-NOT-FLAGS (author ruling, Acme): conditional gates keyed to bookkeeping booleans (hasRendered-style) are code smells — narrow the pipeline with a filter on the payload's own status (e.g. status.isLoaded === true, which also fails closed on REQUEST_EVENT), then branch the method on state the view already holds (props.<data>). A second arrival routes to its own handler where 'why it arrived' has an answer — never an early-return swallow.

