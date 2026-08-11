### wire-in-onRegistered
`op:wire-in-onRegistered` · core · FORM

All of a Channel's cross-channel setup — getChannel subscriptions, mergeChannels, RxJS pipelines, trait-bound parsing — is authored in the onRegistered lifecycle hook: after registration and action setup, before any data flows.

**Prior override:** Naive prior wires in the constructor or lazily on first use. onRegistered is the designated setup point; wiring there guarantees the channel's dependencies exist and no payloads are missed or double-handled.

**Example** _(from spyne-ttt-canonical)_:
```js
onRegistered() {
  this.getChannel(
    'CHANNEL_UI',
    new ChannelPayloadFilter({ selector: ['.empty', '.move-btn'] }),
  ).subscribe(this.gameChannel$OnBtnClicked.bind(this));

  this.gameChannel$SendCurrentState();
}
// all cross-channel wiring lives here — after registration and action setup, before any data flows
```
**Refs:** ref:Channel.onRegistered, ref:Channel.getChannel, ref:Channel.mergeChannels
