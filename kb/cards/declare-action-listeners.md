### declare-action-listeners
`op:declare-action-listeners` · core · FORM

A view declares which channel actions it listens for and which trait method each maps to — addActionListeners pairs [CHANNEL_ACTION, methodName, filter?] — with channels named in props.channels.

**Prior override:** Naive prior wires a handler to a source imperatively. Declare label → method; props.channels declares only what a view *listens* to, never what it emits.

**Example** _(from spyne-todos)_:
```js
export class TodoItemView extends ViewStream {
  constructor(props = {}) {
    props.channels = ['CHANNEL_UI'];
    props.traits = [TodoTraits];
    super(props);
  }

  addActionListeners() {
    const todoFilter = new ChannelPayloadFilter({ todoId: this.props.data.todoId });
    return [['CHANNEL_UI_CLICK_EVENT', 'todos$onItemEvent', todoFilter]];
  }
}
// props.channels declares only what the view listens to;
// each tuple maps [CHANNEL_ACTION, traitMethod, filter?]
```
**Refs:** ref:ViewStream.addActionListeners, ref:ViewStream.constructor

**Caveats:**
- RULED: props.channels is the sanctioned attachment form (tuple ['NAME', true] for skip-first). addChannel() is older — not deprecated, not officially documented; permitted for conditional attachment but no validated use case yet; codegen never emits it. ViewStream.getChannel (raw subject access) is undocumented and NOT sanctioned.
- props.channels and props.traits accept a string OR an array; ALWAYS AUTHOR ARRAYS (the string form predates practice) — string/single-class forms are recognize-never-emit.

