### default-class-with-sparse-exceptions
`op:default-class-with-sparse-exceptions` · standard · FORM

Dynamic view resolution (e.g. pageId → Page) uses a SPARSE lookup of ViewStream classes with a default: pageLookupTable[pageId] || PageView — one data-configured default class serves all ordinary cases; only behaviorally exceptional cases (404) earn a dedicated class. The lookup lives in a trait method (e.g. StageTraits.stage$OnRouteEvent), which destructures the payload, resolves the class, and nests via this.appendView(new PageClass({data, isDeepLink}), '.page-container'). Class references are sanctioned; instance references are not.

**Prior override:** Two corrections. (1) Naive prior builds one component per page and an exhaustive route→component registry; here class variation is the exception and data variation is the rule — the default class absorbs difference through its supplied data. (2) An agent over-applying isolation may refuse the lookup entirely — isolation forbids holding INSTANCES; a map of classes exposes nothing of a live view and is the framework-legible route-to-view mechanism.

**Example** _(from canonical-app)_:
```js
static stage$OnRouteEvent(e, isDeepLink = false) {
  const { pageId, is404 } = e.payload;
  const pageLookupTable = { 404: Page404View };
  let PageClass = pageLookupTable[pageId] || PageView;
  if (is404) PageClass = Page404View;
  this.appendView(new PageClass({ data: e.payload, isDeepLink }), '.page-container');
}
// one data-configured default serves every ordinary page; only behavioral
// exceptions earn a class — class references are sanctioned, instances never
```
**Refs:** ref:ViewStream.appendView, ref:SpyneTrait.constructor, 01:views-are-isolated

**Caveats:**
- Per-branch route keys: resolution key lists derive from the route (payload.paths) or route config per branch — never from a hardcoded uniform ladder. The canonical resolver's ['pageId','topicId','optionId'] default is the canonical app's branches, not a framework constant; paths-driven keys is the vocabulary-agnostic form.

