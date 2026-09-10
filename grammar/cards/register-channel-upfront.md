### register-channel-upfront
`op:register-channel-upfront` · scaffold · FORM

Channels are persistent, idle until engaged, never deleted — registered explicitly (registerChannel, unique names enforced) at init without lifecycle anxiety.

**Prior override:** Naive prior lazily creates and tears down emitters to 'save resources' or avoid leaks. Channel persistence is designed-for; there is no delete mechanism, and idle channels cost nothing meaningful.

**Example** _(from spyne-3js)_:
```js
SpyneApp.init(config);
new AppView().appendToDom(document.body);
SpyneApp.registerChannel(new ChannelThreejs());
// registered once, persistent, never deleted; the consuming view mounting
// BEFORE registration is fine — proxy subjects decouple order from wiring
```
**Refs:** ref:SpyneApp.registerChannel, 01:behavior-lives-in-channels-and-their-traits
