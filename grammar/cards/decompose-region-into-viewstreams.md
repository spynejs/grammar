### decompose-region-into-viewstreams
`op:decompose-region-into-viewstreams` · core · FORM

Slice the requested UI into ViewStreams by DOM-region ownership and disposal-unit boundaries — each view owns one region rooted at a single element.

**Prior override:** Naive prior slices by reuse and prop-flow (component granularity). Here granularity follows region ownership and lifecycle: if a region should appear/disappear as a unit, it is a view; nesting exchanges context, not handles.

**Example** _(from canonical-app)_:
```js
export class StageContainer extends ViewStream {
  constructor(props = {}) {
    props.id = 'stage-view';
    props.channels = ['CHANNEL_APP', 'CHANNEL_ROUTE'];
    props.traits = [StageContainerTraits];
    props.template = `<div class="slot slot-ui"></div>
                      <div class="slot slot-page"></div>`;
    super(props);
  }

  onRendered() {
    this.stage$OnRendered();
  }
}
// each slot is a region a child ViewStream owns as a disposal unit
```
**Refs:** ref:ViewStream.constructor, ref:ViewStream.appendView, 01:views-are-isolated, 01:lifecycle-is-structural-not-reconciled
