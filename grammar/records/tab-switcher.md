### tab-switcher
`record:tab-switcher` · standard

**Recognize when:** "tabs," "switch panels without leaving the page."

Tabbed region where selecting a tab (dataset-carrying tab elements; el$.setActiveItem(activeClass, elSel) for identity-matched active state) swaps the visible panel; panels chosen between dispose/recreate and hide/show per behavioral weight.

**Composes:** op:declare-action-listeners, op:dataset-as-payload, op:dispose-vs-hide, op:dispose-as-unit, op:declare-broadcast-events, op:address-region-by-el$
