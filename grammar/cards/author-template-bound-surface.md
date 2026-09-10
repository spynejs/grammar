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

**Caveats:**
- FORM FIELD NAMES: the template sanitizer strips `name` (and `id`) attributes whose VALUE is a DOM-clobbering token — `id`, `name`, `role`, `body` and their kin shadow real properties of `document` and the form element. The input renders, looks right, and never reaches `FormData`; nothing warns. This is deliberate and is not going to be relaxed: prefix the field instead (`contactName`, not `name`; `messageBody`, not `body`). Learn the RULE, not the list — an author who had already been bitten by `id`/`name`/`role` still wrote `name="body"`. Same silent-breakage class as the safeClone and attr-prefix rules: correct-looking markup, no authoring-time error, wrong behaviour at runtime.

