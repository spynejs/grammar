### use-framework-ui-action-labels
`op:use-framework-ui-action-labels` · core · FORM

UI broadcasts arrive under framework-derived action labels — event 'click' emits CHANNEL_UI_CLICK_EVENT, 'input' emits CHANNEL_UI_INPUT_EVENT, per the documented UIEvents tables. Listeners narrow with these given labels plus ChannelPayloadFilter; label DESIGN applies to custom channels only.

**Prior override:** Naive prior mints its own label for a UI event or expects to name the click action. UI channel labels are framework constants derived from the event name; the model's design freedom on CHANNEL_UI is which events broadcast and how listeners filter — not what the labels are.

**Example** _(from spyne-todos)_:
```js
broadcastEvents() {
  return [['.add-todo', 'click']];
}

addActionListeners() {
  const addActionFilter = new ChannelPayloadFilter({ action: 'add' });
  return [['CHANNEL_UI_CLICK_EVENT', 'todos$OnAddTodo', addActionFilter]];
}
// 'click' arrives as the framework-derived CHANNEL_UI_CLICK_EVENT — you never name the label
// listeners narrow with a filter (here the element's data-action)
```
**Refs:** ref:ViewStream.uiEvents, ref:ViewStream.broadcastEvents, ref:ViewStream.addActionListeners
