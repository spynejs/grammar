### wiring-surface-only-on-viewstream
`op:wiring-surface-only-on-viewstream` · core · FORM

Only broadcastEvents, addActionListeners, onRendered, and the constructor live on a ViewStream class. Everything else is a trait.

**Prior override:** Two priors corrected. (1) Component-tree prior: methods live on the component class. (2) Legacy-SpyneJS prior: earlier framework versions permitted logic methods (e.g. hook callbacks like onFrameUpdate) on ViewStream classes — that allowance is REMOVED. Code exhibiting class-level logic is legacy idiom, never a template; hooks a trait invokes are defined in the trait. The wiring surface is the class's entire surface, enforced because humans and AI both require the strict VBL distinction.

**Example** _(from canonical-app)_:
```js
export class PageView extends ViewStream {
  constructor(props = {}) {
    props.channels = [['CHANNEL_ROUTE', true]];
    props.traits = [PageItemCoreTraits];
    super(props);
  }
  broadcastEvents() { return [['a', 'click']]; }
  addActionListeners() {
    return [['CHANNEL_ROUTE_CHANGE_EVENT', 'disposeViewStream']];
  }
  onRendered() {
    this.pageItemCore$onRendered();
  }
}
// the class's entire surface: constructor, broadcastEvents, addActionListeners,
// onRendered — everything else is a trait
```
**Refs:** ref:ViewStream.broadcastEvents, ref:ViewStream.addActionListeners, ref:ViewStream.onRendered, 01:behavior-lives-in-channels-and-their-traits
