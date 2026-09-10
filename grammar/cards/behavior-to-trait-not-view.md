### behavior-to-trait-not-view
`op:behavior-to-trait-not-view` · core · FORM

The method that runs when a declared action fires is authored in a SpyneTrait, never on the view.

**Prior override:** Naive prior writes the handler where the element lives. The handler lives in a SpyneTrait; the label→method declaration is the connection.

**Example** _(from spyne-todos)_:
```js
// todo-list-view.js — the declaration is the connection
addActionListeners() {
  return [['CHANNEL_UI_CLICK_EVENT', 'todos$OnAddTodo']];
}

// todo-traits.js — the handler lives in the trait, never on the view
static todos$OnAddTodo() {
  const text = this.props.el$('.new-todo').el.value.trim();
  if (!text) return;
  this.appendView(new TodoItemView({ data: { text } }), '.items');
}
// trait methods run with the view as context — this.props, this.appendView
```
**Refs:** ref:SpyneTrait.constructor, ref:ViewStream.addActionListeners, 01:behavior-lives-in-channels-and-their-traits

**Caveats:**
- RULED: static is the DEFAULT trait-method form — useful, not mandatory (unit-testable framework-free; callable unbound/uncomposed). Instance methods remain valid, notably for library-custody traits.

