### author-pageitem-spec
`op:author-pageitem-spec` · standard · FORM

Adding display content to a page means authoring a pageItem object — a serialized view spec {viewClass, props:{tagName, template, styles, data}, container} — not writing a module. viewClass resolves via lookup table with ViewStream as default; named classes (ContactUsView) are the sparse exceptions. container.isEnabled:false renders without the wrapper.

**Prior override:** Naive prior creates a component file for every new section. Here the default path is data: one spec object in pageItems. A new module is authored only when behavior exceeds what a data-configured ViewStream expresses — default-class-with-sparse-exceptions, seen from the data side.

**Example** _(from canonical-app)_:
```js
{
  "viewClass": "ViewStream",
  "props": {
    "tagName": "div",
    "class": "cards-title",
    "template": "<h2>{{headline}}</h2><p>{{subheadline}}</p>",
    "data": {
      "headline": "Section Headline",
      "subheadline": "Optional subhead text for the cards below."
    }
  },
  "container": { "isEnabled": false }
}
// a serialized view spec, not a module — viewClass resolves via lookup with
// ViewStream default; container.isEnabled:false renders without the wrapper
```
**Refs:** ref:ViewStream.constructor, ref:DomElementTemplate.constructor, 01:the-dom-is-meaningful-structure

**Caveats:**
- Validate output against app-model.schema.json (pageItem $def).
- RULED: isEnabled canonical everywhere; 'enabled' is removed/legacy.
- BIRTH vs DOMAIN DATA (Acme-derived): birth data flows down (spec, construction props); domain data flows through channels — and which one a value IS depends on whether it changes within the lifetime of the view holding it. Domain data that cannot change within a page's lifetime is correctly handed down at construction; per-item subscriptions for it are machinery for a change that never comes.

