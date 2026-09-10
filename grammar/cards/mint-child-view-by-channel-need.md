### mint-child-view-by-channel-need
`op:mint-child-view-by-channel-need` · core · CHOOSE

The granularity test for single elements and small element groups: if the parent ViewStream ALREADY listens to the behavior's channel, the parent maintains the element (broadcastEvents on the parent; multiple static interactive elements with few sync updates stay parent-maintained). A dedicated child ViewStream is warranted only when the element needs a channel the parent does not listen to (canonical hamburger: parent header doesn't listen to CHANNEL_MENU_DRAWER, so the hamburger is its own Item view). Dynamic additions always fork to dynamic-children-ingress.

**Prior override:** Component-tree priors mint components by reuse and visual identity. Here the criterion is CHANNEL TOPOLOGY: a view boundary exists to host a channel subscription the parent lacks — not to wrap markup.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- From the hamburger and menu-drawer-nav @cr comments — the invocable test decompose-region-into-viewstreams has lacked since v1.
- Applied silently in the tic-tac-toe port: squares earn no child views — template-authored buttons with dataset identity, parent-maintained, because no square needs a channel the parent lacks.
**Refs:** ref:ViewStream.broadcastEvents, ref:ViewStream.constructor, 01:views-are-isolated
