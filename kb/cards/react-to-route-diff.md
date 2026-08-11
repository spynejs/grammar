### react-to-route-diff
`op:react-to-route-diff` · standard · FORM
_Diff keys grounded: canonical nav-breadcrumb-view-traits.js._

Route payloads carry the TRANSITION, not just the destination: pathsAdded / pathsRemoved / pathsChanged, routeCount, isDeepLink. Listeners can respond to the KIND of move (deepening, retreating, first load, sibling swap) without diffing previous state per component.

**Prior override:** The naive prior stores previous route state in each component and diffs manually. The diff is already conformed into every route envelope — no mainstream router hands components a location diff.

**Example** _(from canonical-app)_:
```js
static navBreadcrumbView$DeriveState(payload, props = this.props) {
  const { bcProps, navLevel } = props;
  const { paths = [], pathInnermost, routeData = {} } = payload;
  const onCurrentPath = bcProps.some((p) => paths.includes(p));
  const isVisible = routeData.pageId !== 'home' && onCurrentPath;
  const isSelected = isVisible && bcProps.includes(pathInnermost);
  const isActive = isVisible && paths.length > navLevel;
  return { isVisible, isActive, isSelected };
}
// the KIND of move (deepening, retreating, terminal) is read from the
// envelope's paths[] / pathInnermost — no per-component previous-state diffing
```

**Composes:** op:read-route-context-from-payload
**Refs:** ref:SpyneApp.config.route
