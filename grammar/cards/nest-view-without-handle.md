### nest-view-without-handle
`op:nest-view-without-handle` · standard · FORM

Rendering a child view — appendView/prependView/appendViewAfter(v, query?) in the parent's onRendered — exchanges parent/child lifecycle context via an internal observable chain, not handles.

**Prior override:** Naive prior stores child refs on the parent to call later. No references exist to store; coordination that seems to need a handle goes through a channel.

**Example** _(from canonical-app)_:
```js
static app$OnAppViewRendered() {
  this.appendView(new UIHeaderView());
  this.appendView(new UIMenuDrawerView());
  this.appendView(new StageContainer());
  this.appendView(new UIFooterView());
}
// no child references stored — lifecycle context exchanges through the
// internal observable chain; coordination goes through channels
```
_modernized: dropped specimen's LocalStorageNullView line (another op's subject)_
**Refs:** ref:ViewStream.appendView, ref:ViewStream.prependView, ref:ViewStream.appendViewAfter, ref:ViewStream.onRendered, 01:views-are-isolated
