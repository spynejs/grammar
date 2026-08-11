### route-scoped-view-state
`op:route-scoped-view-state` · standard · FORM

The generalizable navigation-family pattern: a view parameterized by ROUTE COORDINATES from data (bcProps, navLevel — discovered from navLinks/paths, never hardcoded key names), deriving all render state purely from (route payload + own coordinates), applying via el$, and writing its navLink's route keys back into its anchor's dataset so the view's own links stay live ROUTE links as the app moves.

**Prior override:** Naive nav components hardcode key names and hold route state. Vocabulary-agnostic coordinate discovery is what lets ONE implementation serve every branch's key vocabulary (profile/userId and products/productId simultaneously).

**Example** _(from canonical-app)_:
```js
static navBreadcrumbView$UpdateLink(e) {
  const { payload } = e;
  const { isVisible, navLink } = this.navBreadcrumbView$DeriveState(payload);
  if (!isVisible || navLink === undefined) return;
  this.props.link$.el.innerText = navLink.title;
  this.props.link$.el.href = navLink.href;
  // write route coordinates into the dataset — reads are live, so the
  // crumb stays a correct ROUTE link as the app moves
  for (const key of payload.paths) {
    if (navLink[key] !== undefined) {
      this.props.link$.el.dataset[key] = navLink[key];
    }
  }
}
// coordinates (bcProps, navLevel) come from data, key names discovered from
// paths — one implementation serves every branch's vocabulary
```

**Composes:** op:read-route-context-from-payload, op:author-navigation-as-dataset-links, op:dataset-as-payload
**Refs:** ref:ViewStream.el$
