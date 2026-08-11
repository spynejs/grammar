### prototype-in-data-then-promote
`op:prototype-in-data-then-promote` · standard · FORM

pageItems support a data-first lifecycle: isPrototype (true/absent) marks a fully data-defined item, iterable rapidly through the CMS copy/paste loop with AI; when the design stabilizes or behavior outgrows data, the item is promoted to a declared module (viewClass lookup) and pinned (isPrototype:false).

**Prior override:** Naive prior runs the workflow backwards: write a component first, wire data later. Here prototyping happens IN the model — zero code churn while the design is fluid; promotion is a deliberate, single act when structure is earned.

**Example** _(from canonical-app)_:
```js
// fluid: fully data-defined, inline template (isPrototype absent/true)
{ "viewClass": "ViewStream",
  "props": { "template": "<h2>{{headline}}</h2>", "data": { "headline": "Draft" } } }

// promoted and pinned: named class + template file
{ "viewClass": "ContactUsView",
  "isPrototype": false,
  "props": { "template": "contact-us.tmpl.html" } }
// promotion = an entry in the viewClass lookup + isPrototype:false switching
// template resolution from inline HTML to the template-file lookup
```
**Refs:** ref:ViewStream.constructor

**Caveats:**
- PROMOTION MECHANICS RESOLVED: promotion = adding the component's entry to PageItemCoreTraits' viewClass lookup table (sparse lookup, ViewStream default) and, at the template layer, isPrototype:false switching template resolution from inline HTML to template file name.

