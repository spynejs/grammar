### slice-traits-by-concern
`op:slice-traits-by-concern` · core · FORM

Partition logic into traits organized by what it does, not where it's used (FormTraits, AnimationTraits, AuthTraits), each namespaced by its prefix$ and composed in props. Trait methods are pure and stateless.

**Prior override:** Naive prior groups methods by the component they serve. Traits are composed capabilities shared across ViewStreams and Channels; by-what-it-does slicing plus prefix$ namespacing is what makes them reusable and readable.

**Example** _(from canonical-app)_:
```js
export class AppStatusTraits extends SpyneTrait {
  constructor(context) {
    let traitPrefix = 'appStatus$';
    super(context, traitPrefix);
  }

  static appStatus$OnRouteEvent(e) {
    this.appStatus$SendDataEvent(e.payload.routeData);
  }
}
// sliced by what it does, not where it's used; every method wears the prefix$ namespace
```
**Refs:** ref:SpyneTrait.constructor
