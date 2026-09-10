### assign-view-lifecycle-tier
`op:assign-view-lifecycle-tier` · core · CHOOSE

The first classification of any view region, before archetype or record: WHO GOVERNS ITS EXISTENCE? Three tiers: PERSISTENT — app-governed; appended in AppContainer before Stage (header, footer, drawer); never disposed; owns its own show/hide behavior capture. PAGE — route-governed; renders/disposes or shows/hides on route location (the tier fixes the governor; dispose-vs-hide remains the per-view mechanism choice). PAGEITEM — parent-governed; existence rides the parent's disposal cascade, never its own route subscription. Event-driven transients (modal, toast) are NOT a fourth tier — RULED: persistent host + self-removing children. A dedicated container (ModalContainer, ToastContainer) is persistent-tier, scaffold-instantiated; transients are its parent-governed children holding SELF-TERMINATION privilege (own timeout/close action initiates early dispose) while the host's cascade bounds their existence.

**Prior override:** Component-tree priors classify views by content and reuse; here identity is lifecycle governance. Two concrete violations the tier discipline prevents: a pageItem subscribing to CHANNEL_ROUTE to decide its own existence (route-listening-for-CONTENT is fine — route-scoped items; route-listening-for-EXISTENCE belongs to the page tier); and a persistent view being disposed/re-rendered on navigation.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Completes the top-down reasoning stack: lifecycle tier (who governs) → archetype (what pattern) → record (how assembled) → ops (which moves). Scaffold-time question preceding all feature-time questions.
- Tier consequences are mechanical: persistent tier is where replay semantics and long-lived subscriptions concentrate; page tier is where dispose-vs-hide is live; pageItem tier inherits everything.
- The three-tier question stays singular — 'who ultimately owns this existence?' — with self-termination as an early-exit clause, not a governance transfer. Agent consequence: 'add a modal' routes through the existing persistent host (transmit → host instantiates → child self-disposes), never 'create a modal system.'
**Refs:** ref:ViewStream.constructor, ref:ViewStream.disposeViewStream, 01:lifecycle-is-structural-not-reconciled, 01:vbl-the-spine

**Caveats:**
- Edge placements: null-appended and plugin views = persistent tier, invisible variant; adopted views take the adopter's tier; upcoming 'blog view' = page tier with route governance remapped from lifecycle to scroll position — the model's expressive proof, not an exception.
- Route-tier disposal has two sanctioned mechanisms, one governor: (a) stage disposes the outgoing page; (b) each page self-disposes on the route event (['ROUTE-family action','disposeViewStream'] + skip-first) — ToH uses (b). Tier = governor; mechanism is per-app.

