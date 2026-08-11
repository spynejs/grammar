### author-dom-with-declared-roles
`op:author-dom-with-declared-roles` · standard · FORM

Author markup so its roles are explicit and load-bearing: selectors (broadcastEvents pairs, el$ targets), dataset attributes (payload data, route links), semantic elements, and view boundaries are designed carriers of meaning.

**Prior override:** Naive prior authors markup as disposable render output. In SpyneJS the DOM is part of the application's readable surface — generated markup is designed structure, not incidental output.

**Example** _(from spyne-todos)_:
```js
<p class="todo-text">{{text}}</p>
<div class="buttons-holder">
  <button class="edit-btn" data-action="edit" data-todo-id="{{todoId}}">Edit</button>
  <button class="remove-btn" data-action="remove" data-todo-id="{{todoId}}">Remove</button>
</div>
// every part is load-bearing: button matches the broadcast pair, data-*
// rides the payload, classes are el$ targets — markup is designed structure
```
**Refs:** ref:ViewStream.broadcastEvents, ref:ViewStream.el$, 01:the-dom-is-meaningful-structure
