### deferred-behavior-adoption
`record:deferred-behavior-adoption` · standard

**Recognize when:** "hundreds of items, add interactivity when needed," "enhance server-rendered HTML," "progressive enhancement at scale."

Large numbers of items rendered up front (statically, server-side, or in one cheap pass) with ViewStream behavior attached only on visibility or interaction: elements exist as plain DOM until a trigger adopts them ({el}) — from then on they are full views with normal wiring and disposal. The progressive-enhancement / islands record.

**Composes:** op:adopt-existing-element, op:dispose-as-unit, op:declare-broadcast-events, op:window-event-via-channel, op:no-leaked-subscription
