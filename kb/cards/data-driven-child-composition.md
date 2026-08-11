### data-driven-child-composition
`op:data-driven-child-composition` · core · FORM

A view's supplied data declares whether and which children load — composition read from data at render time rather than hardcoded in onRendered. 'The data decides' promoted from template conditionals to view nesting; one class serves many configurations.

**Prior override:** Naive prior treats composition as code: the parent imports and mounts its children unconditionally, so every configuration variant becomes a new component. Here children are data-declared; the parent's nesting logic reads the supplied data file.

**Example** _(from canonical-app)_:
```js
static pageItemCore$onRendered(props = this.props) {
  const { hero, pageItems, content, pageType } = props.data;

  if (hero) {
    this.appendView(new HeroView({ data: hero, pageType }), '.page-heading');
  }
  if (content) {
    this.appendView(new CardsContainerView({ data: content, pageType }), '.page-body');
  }
  if (pageItems) {
    this.pageItemCore$AddPageItems();
  }
}
// the supplied data decides whether and which children load —
// one PageView class serves every page configuration
```
**Refs:** ref:ViewStream.onRendered, ref:ViewStream.appendView, 01:the-dom-is-meaningful-structure

**Caveats:**
- See author-pageitem-spec's birth-vs-domain-data note — the lifetime test decides construction handoff vs subscription per value.

