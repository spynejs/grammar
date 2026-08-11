### no-leaked-subscription
`op:no-leaked-subscription` · standard · FORM

Generated code must be lifecycle-complete: no leaked subscription, orphaned DOM behavior, or unmanaged effect — a leak makes the solution malformed, not untidy.

**Prior override:** Naive prior treats a stray listener as a minor smell to clean later. Lifecycle is the structure; generation isn't done until every attached behavior has a structural teardown path.

**Example** _(from spyne-3js)_:
```js
export class CalloutViewItem extends ViewStream {
  constructor(props = {}) {
    props.tagName = 'article';
    props.channels = ['CHANNEL_THREEJS'];
    props.template = CalloutViewTmpl;
    super(props);
  }

  addActionListeners() {
    return [['CHANNEL_THREEJS_ANGLE_CHANGE_EVENT', 'disposeViewStream']];
  }
}
// born on the event, disposes on the event: subscriptions and DOM leave
// together — every attached behavior has a structural teardown path
```
**Refs:** ref:ViewStream.disposeViewStream, 01:lifecycle-is-structural-not-reconciled
