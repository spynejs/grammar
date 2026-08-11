### conditional-via-object-section
`op:conditional-via-object-section` · standard · MULTI-FORM

Conditional rendering is an object section: {{#obj}}...{{/obj}} renders once when obj is truthy, not at all when absent — including wrapper tags. Dynamic variants (e.g. tag choice) use pre-computed flags with object sections.

**Prior override:** Naive prior reaches for {{#if}}/{{^key}} inverted sections. Neither exists; shape the data so the desired section renders naturally, or resolve in a trait.

**Forms:** _(inventory below; each line links to its REFERENCE example)_

- Grounded: the docs' canonical example uses the object section INSIDE an array loop ({{#eyebrow}} within {{#items}}) — inside-loop element-wrapping sections are first-class, not an exception.
**Refs:** ref:DomElementTemplate.objectSectionAsConditionalWrapper
