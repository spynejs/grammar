### author-navigation-as-dataset-links
`op:author-navigation-as-dataset-links` · standard · FORM

Navigation links are DOM-declared: an element with data-channel="ROUTE" plus a dataset attribute matching a routeName key (e.g. data-page-id="page-1"). The Route Channel captures the click, updates the URL (slash/query/hash per config), and emits routeData.

**Prior override:** Naive prior writes <Link> components or programmatic navigate() calls. In SpyneJS navigation is authored as data — dataset attributes resolved against the route config; no navigation code exists.

**Example** _(from canonical-app)_:
```js
<a
  class="nav"
  data-channel="ROUTE"
  data-event-prevent-default="true"
  data-page-id="{{pageId}}"
  href="{{href}}"
>{{title}}</a>
// data-channel="ROUTE" sends the captured click to CHANNEL_ROUTE;
// data-page-id resolves against the route config (camelCased into routeData)
```
**Refs:** ref:SpyneApp.config.route, 01:the-dom-is-meaningful-structure

**Caveats:**
- data-end-route="true": the link terminates the route at its declared level — checkForEndRoute walks the route config below the matched value and clears the next-deeper routeName param from the payload (warns if used at the start route). Use for links to a parent page from deeper routes so stale deeper params don't persist.
- Capture clarified: route-link clicks are captured via broadcastEvents like any DOM event; data-channel='ROUTE' routes the captured event to CHANNEL_ROUTE instead of CHANNEL_UI.

