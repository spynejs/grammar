### read-route-context-from-payload
`op:read-route-context-from-payload` · core · FORM

Location context comes from the route payload's data — routeData keys (the branch's params), paths[] (ordered active keys), pathInnermost (deepest) — never from parsing location.pathname. Auxiliary dataset attributes on the triggering link ride routeData verbatim (eventType, eventPreventDefault, endRoute), so links can carry custom context through navigation.

**Prior override:** The naive prior parses window.location or holds route state locally. The route IS conformed data on the bus; every consumer reads the same envelope.

**Example** _(from canonical-app)_:
```js
static uiMenuDrawer$SetActiveLink(e) {
  const { pageId, topicId = '' } = e.payload.routeData;
  const activeSel = `a.nav[data-page-id='${pageId}'][data-topic-id='${topicId}']`;
  this.props.el$('a.nav').setActiveItem('selected', activeSel);
}
// location context is the payload's routeData — never parsed from location.pathname;
// dataset ROUTE links self-describe (data-page-id)
```
**Refs:** ref:SpyneApp.config.route
