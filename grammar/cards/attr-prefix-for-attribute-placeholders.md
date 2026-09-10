### attr-prefix-for-attribute-placeholders
`op:attr-prefix-for-attribute-placeholders` · conditional · FORM

In app-model / template data, any key whose value populates an ELEMENT ATTRIBUTE carries the attr prefix (attrImageSrc, attrCtaHref, attrRequired, attrMapSrc); text-content keys do not (headline, ctaText). SCOPE: the prefix is REQUIRED only when a ViewStream template is defined as data passing through the CMS; elsewhere it is optional. The prefix is a machine-facing contract: the CMS ignores attr-prefixed placeholders, so attribute positions are never converted into CMS-editable items (which breaks the HTML).

**Prior override:** Naive prior names keys semantically (imageSrc, href) — correct-looking, and it breaks silently under the CMS: no authoring-time error, just broken markup when the CMS proxifies attribute placeholders. Same silent-breakage class as safeClone. The rule is positional, not a memorized list: lands-in-attribute => prefix.

**Example** _(from canonical-app)_:
```js
{
  "attrId": "contact-email",
  "label": "Email",
  "attrName": "email",
  "attrType": "email",
  "attrPlaceholder": "you@example.com",
  "attrRequired": true
}
// keys landing in element attributes carry the attr prefix — the CMS skips
// them; text-content keys (label) don't. Positional rule, not a list
```
**Refs:** ref:DomElementTemplate.constructor, ref:ChannelFetch.constructor

**Caveats:**
- Necessity condition is precise: template-as-data + CMS. Uniform application outside that condition is a style choice, not a rule.
- RESOLVED (empty-attr mechanism retracted): the mid-tag ban is positional, not scopal. Boolean-attribute presence uses pre-computed flags with element-level variants; value attributes bind via attr* normally.

