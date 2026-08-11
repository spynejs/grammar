### author-app-model-node
`op:author-app-model-node` · standard · FORM

Adding a page or subpage means authoring a NODE in the app model: an entry in the correct subpages array (or pages, at root) whose route-identity keys match THAT BRANCH'S route-config params, validated against app-model.schema.json. Content rides the node (hero, pageItems, card presentation); routing, nav, breadcrumbs, and page swapping all derive.

**Prior override:** Naive prior creates a view class and a route entry per page. Here 'add a page' is a DATA edit — a schema-valid node in the right branch; a new module is authored only when behavior exceeds what data-configured views express.

**Example** _(from canonical-app)_:
```js
{
  "pageId": "about",
  "pageType": "about",
  "title": "About Us",
  "template": "section-template.html",
  "hero": {
    "headline": "Our Mission",
    "subheadline": "Explicit architecture, predictable behavior.",
    "attrImageSrc": "imgs/pexels-photo-3184418.jpeg",
    "ctaText": "Explore the docs"
  },
  "pageItems": []
}
// adding a page is a DATA edit: a node whose route-identity keys match the
// branch's params — routing, nav, breadcrumbs, and swapping all derive
```
_modernized: subheadline shortened; pageItems elided; specimen's drift keys (img, ctaHref) dropped for canonical attr* forms_

**Composes:** op:name-route-keys-for-legibility, op:author-pageitem-spec, op:data-driven-child-composition
**Refs:** ref:SpyneApp.config.route
