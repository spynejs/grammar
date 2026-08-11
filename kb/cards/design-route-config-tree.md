### design-route-config-tree
`op:design-route-config-tree` · core · FORM

Author the nested routePath tree in SpyneApp.init as the SPA's page topology: routeName keys, URL-segment mappings (string or array/glob), nesting mirroring the app's navigation hierarchy. Declared once, before any view exists.

**Prior override:** Naive prior reaches for a router library with per-view route registration and route components. In SpyneJS the route config IS the skeleton — a single declarative tree the Route Channel reads for both navigation and emitted routeData.

**Example** _(from canonical-app)_:
```js
routes: {
  routePath: {
    routeName: 'pageId',
    home: '',
    'page-view': {
      routePath: {
        routeName: 'topicId',
        'card-a': 'card-a',
        'card-b': 'card-b',
      },
    },
    about: 'about',
  },
},
// config.channels.ROUTE in SpyneApp.init — the page topology, declared once, before any view exists
```
**Refs:** ref:SpyneApp.config.route, ref:SpyneApp.init

**Caveats:**
- Per-branch key vocabularies: each branch declares its own descent keys (see name-route-keys-for-legibility).
- Branch values may be arrays of aliases including simple-regex strings (canonical: cr: ['construction-record', 'construction-.*']; ToH: 'dashboard|^$|index.html').
- RULED: branch members are string | regex | array — literal members and dynamic (regex) members coexist at one level (sibling literal+dynamic CLOSED; Acme's invoices/create beside invoices/{id} is expressible).

