### dispose-as-unit
`op:dispose-as-unit` · core · FORM

Design teardown around unit disposal: disposeViewStream cascades from the bottom of the nested chain — children remove and unsubscribe first, then the instance removes itself from DOM and memory.

**Prior override:** Naive prior writes manual cleanup checklists or per-piece unmount logic. One mechanism produces both isolation and unit-disposal — author so disposal is a single structural act.

**Example** _(from spyne-todos)_:
```js
static todos$RemoveItem() {
  this.disposeViewStream();
}
// one structural act: nested children unsubscribe and remove first,
// then the instance leaves DOM and memory — no cleanup checklist
```
**Refs:** ref:ViewStream.disposeViewStream, 01:lifecycle-is-structural-not-reconciled
