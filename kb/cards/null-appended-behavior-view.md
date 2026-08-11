### null-appended-behavior-view
`op:null-appended-behavior-view` · standard · FORM

A ViewStream rendered via appendToNull — functionally active (listening on channels, running methods) but visually absent — used as a behavior participant (bridge, orchestrator).

**Prior override:** Naive prior reaches for a 'service' singleton outside the framework. The framework-legible form is appendToNull, so the wiring stays declared and traceable.

**Example** _(from canonical-app)_:
```js
export class LocalStorageNullView extends ViewStream {
  constructor(props = {}) {
    props.channels = ['CHANNEL_LOCAL_STORAGE'];
    props.traits = [AppLocalStorageTraits];
    super(props);
  }

  onRendered() {
    this.localStorage$InitAppSettings();
  }
}

new LocalStorageNullView().appendToNull();
// lives in hidden #spyne-null-views — fully active on channels, visually
// absent; the framework-legible form of a 'service'
```
**Refs:** ref:ViewStream.appendToNull
