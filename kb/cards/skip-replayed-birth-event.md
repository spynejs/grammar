### skip-replayed-birth-event
`op:skip-replayed-birth-event` · core · FORM

When a view is spawned by a channel event and listens to that same replaying channel (e.g. for disposal), skip the first emission: [CHANNEL_NAME, true] in props.channels (sanctioned form; addChannel(name, true) exists but is undocumented — codegen never emits it). Otherwise the view acts on its own replayed birth event. CONDITION PRECISE: skip-first is required IFF the channel replays; non-replay channels' spawned children listen safely without it (spyne-3js CalloutViewItem: born on ANGLE_CHANGE, disposes on ANGLE_CHANGE, no skip — CHANNEL_THREEJS has no replay).

**Prior override:** Naive prior subscribes and reacts to every emission. A ReplaySubject replays the spawning payload to the new subscriber; without skipFirst, a disposal listener fires immediately on the event that created the view.

**Example** _(from canonical-app)_:
```js
export class PageView extends ViewStream {
  constructor(props = {}) {
    props.channels = [['CHANNEL_ROUTE', true]];
    props.template = PageTmpl;
    super(props);
  }

  addActionListeners() {
    return [['CHANNEL_ROUTE_CHANGE_EVENT', 'disposeViewStream']];
  }
}
// true = skip the replayed birth event; without it the dispose listener
// fires on the very emission that created the view
```
**Refs:** ref:ViewStream.constructor, ref:ViewStream.addChannel

**Caveats:**
- SMELL CHECK (Acme): if skip-first appears to fix an ordering problem, first ask whether the ordering problem is self-inflicted (a pattern applied at the wrong tier) — a fix for a self-inflicted wound reads exactly like a fix for a real one.

