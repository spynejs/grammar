### recognize-own-emission
`op:recognize-own-emission` · standard · FORM

A view that must react to its own payload returning through a channel adds an explicit identity marker/filter.

**Prior override:** Naive prior assumes a component recognizes its own events (event.target identity). Identity is never implicit in SpyneJS — a view does not recognize its own emission without an explicit filter.

**Example** _(from spyne-todos)_:
```js
// <button data-action="edit" data-todo-id="{{todoId}}">Edit</button>
addActionListeners() {
  const todoFilter = new ChannelPayloadFilter({
    todoId: this.props.data.todoId,
  });
  return [['CHANNEL_UI_CLICK_EVENT', 'todos$onItemEvent', todoFilter]];
}
// identity is never implicit: the view's own broadcast returns through the
// shared channel and is reclaimed by the todoId marker riding its dataset
```
**Refs:** ref:ChannelPayloadFilter.constructor, 01:views-are-isolated
