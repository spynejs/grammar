### render-nav-from-config
`op:render-nav-from-config` · core · FORM

Application navigation can be rendered from SpyneAppProperties.getNavLinks(), which returns dynamically generated links derived from the route config.

**Prior override:** Naive prior hand-authors the nav and keeps it manually in sync with routes. The route config is the single source; the nav is derived from it.

**Example** _(from canonical-app)_:
```js
static uiHeader$UIHeaderViewOnAppInitEvent(e) {
  const { navLinks } = e.payload.initData;
  const data = navLinks.filter((o) => o.navLevel === 1);
  this.appendView(new NavPrimaryView({ data }), '.header-content');
}
// navLinks are derived from the route config and ride the payload — the nav is never hand-authored
```
**Refs:** ref:SpyneAppProperties.getNavLinks, ref:SpyneApp.config.route
