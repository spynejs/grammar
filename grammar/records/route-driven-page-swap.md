### route-driven-page-swap
`record:route-driven-page-swap` · standard

**Recognize when:** "clicking nav should switch the content," "show a different page per URL."

Top-level navigation: a routeData change disposes the current page subtree and renders the next, optionally gated on that page's data.

**Composes:** op:route-as-data, op:dispose-as-unit, op:nest-view-without-handle, op:no-leaked-subscription, op:skip-replayed-birth-event, record:gate-render-on-data
