### author-template-bound-surface
`op:author-template-bound-surface` · standard · FORM

Design a template's bound (mustache) fields as its structural contract; the surrounding markup is ordinary HTML.

**Prior override:** Naive prior treats a template as inert markup with holes. The bound surface is read by the framework — bound fields are API, chosen deliberately.

**Example** _(from spyne-toh)_:
```js
<li class="hero-item hero-item-{{id}}">
  <a data-channel="ROUTE" data-page-id="detail" data-id="{{id}}">
    <span class="badge">{{id}}</span> {{name}}
  </a>
</li>
// the bound fields ({{id}}, {{name}}) are the template's structural
// contract, chosen deliberately; the surrounding markup is ordinary HTML
```
**Refs:** ref:DomElementTemplate.constructor, 01:the-dom-is-meaningful-structure
