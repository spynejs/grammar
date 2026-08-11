### name-route-keys-for-legibility
`op:name-route-keys-for-legibility` · core · FORM

RouteName keys are BRANCH DECLARATIONS, not a global ladder: the RouteMap supports per-branch key vocabularies (depth 2 under 'profile' may be userId while depth 2 under 'products' is productId). Level 1 (pageId) is the one shared key — it selects the branch. Deeper keys should take domain nouns per branch; the canonical trio (topicId, optionId) is simply what the canonical app's branches declare. A dataset ROUTE link then self-describes (data-product-id). Depth is NEVER encoded in names: the route config declares each branch's order and every payload carries paths[] + pathInnermost.

**Prior override:** Two wrong instincts. (1) Encoding hierarchy into names (subPageL1Id, subPageL2Id) duplicates what paths[] already guarantees and destroys at-a-glance distinctness — level tokens differ by one mid-token glyph, and data-page-id vs data-sub-page-id is a confusable adjacent pair. (2) Treating the canonical trio as framework-fixed vocabulary — the keys are config; domain nouns are encouraged and fully discoverable via the homology + paths machinery.

**Example** _(from canonical-app)_:
```js
routePath: {
  routeName: 'pageId',
  home: '',
  'page-view': {
    routePath: {
      routeName: 'topicId',
      'card-a': 'card-a',
    },
  },
},
// level-1 pageId selects the branch; each branch declares its own domain-noun key
// depth is never encoded in names — paths[] carries order
```
**Refs:** ref:SpyneApp.config.route, 01:the-dom-is-meaningful-structure

**Caveats:**
- App-model homology follows automatically: node keys mirror whatever the route config names.
- Discourage cross-branch reuse of generic keys (e.g. 'id' in two branches): distinct nouns app-wide keep navLinks derivation and dataset anchors unambiguous.
- Replica exception RULED: fidelity ports (spyne-toh keeps 'id' matching Angular's :id) may retain source-fidelity keys — mark with a deliberate-deviation comment so agents don't adopt generic keys as house style.

