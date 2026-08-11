### query-params-as-route-state
`op:query-params-as-route-state` · standard · FORM

Shareable, back-button-correct UI state (search terms, page numbers, filters) lives in URL query params conformed into routeData — not in channel state alone. The Route Channel's query URL support carries it; listeners react to param diffs like any route change.

**Prior override:** Naive prior holds filter/pagination state in component or channel state, losing shareability and history. The Next.js searchParams prior maps here directly — SpyneJS's version is routeData, same envelope as everything else.

**Example** _(from spyne-toh)_:
```js
ROUTE: {
  type: 'query',
  routes: {
    routePath: {
      routeName: 'pageId',
      dashboard: 'dashboard|^$|index.html',
      heroes: 'heroes',
      detail: {
        routePath: { routeName: 'id', '\\d+': '\\d+' },
      },
    },
  },
},
// type:'query' → ?pageId=detail&id=12, conformed into routeData like any
// route change — shareable and back-button-correct by construction
```
**Refs:** ref:SpyneApp.config.route

**Caveats:**
- RULED with caveat: ONE capture type per app (slash | query | hash). Identity-in-path + state-in-query requires either all-query routing (filter state becomes ordinary routeData free — ToH-style; URL aesthetics cost) or slash routing + manual query capture consolidated by a custom RouteCombinedChannel.

