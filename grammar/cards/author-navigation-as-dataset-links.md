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
- A BARE ANCHOR IS NOT A BROKEN ROUTE LINK — IT IS AN ORDINARY LINK. `<a href="/page">` with no `data-channel="ROUTE"` still reaches the page: the browser follows the href and the application loads afresh. Nothing errors and nothing warns, and any check of where the link goes passes; the symptom is a page that flashes and state that resets on one link and not on its neighbours. This holds even where a parent view broadcasts the anchor's click — without `data-channel` the captured event is CHANNEL_UI's, which does not suppress the browser's default. Every anchor to a place inside the app carries the ROUTE dataset; only a link that leaves the app goes without. Verify navigation by clicking and confirming the document did not reload, not by reading the href.
- THE HREF IS NEVER READ. A ROUTE anchor's destination is its dataset laid over the CURRENT route; `href` only supplies the address a browser shows and opens in a new tab. So the dataset must say everything the link means, at every level of the route tree. A routeName key that is PRESENT BUT EMPTY clears that level — an empty `data-page-id` is the start route, so a link whose data did not arrive goes home, silently. A key that is ABSENT keeps the current route's value — from /about/coaches, a link carrying only `data-page-id="classes"` lands on /classes/coaches, and a link carrying no ids at all does nothing. Bind every level from data (an explicit empty value, or data-end-route, for the levels the link does not use); for links rendered in a template loop, carry the ids on each item.

