### onrendered-as-attach-point
`op:onrendered-as-attach-point` · core · FORM

onRendered runs immediately after the root element enters the DOM, before the next animation frame — and it is where nested child ViewStreams are added. Work triggered there routes to trait methods.

**Prior override:** Naive prior imports the useEffect/mounted model — arbitrary side effects after render. onRendered is part of the declared surface with a designated job (nesting); unmanaged effects there are malformed.

**Example** _(from canonical-app)_:
```js
onRendered() {
  this.stage$OnRendered();
}

// stage-container-traits.js
static stage$OnRendered() {
  this.appendView(new NavBreadcrumbContainer(), '.slot-page');
}
// runs right after the root element enters the DOM; its designated job is
// nesting children, and the work routes to a trait method
```
**Refs:** ref:ViewStream.onRendered
