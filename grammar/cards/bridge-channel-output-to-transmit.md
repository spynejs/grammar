### bridge-channel-output-to-transmit
`op:bridge-channel-output-to-transmit` · standard · FORM

Route one channel's output back into a transmit using a null-appended ViewStream (appendToNull — lives in hidden #spyne-null-views, fully active on channels) that listens and does sendInfoToChannel.

**Prior override:** Naive prior has channel A push an action directly into channel B. A Channel cannot push into another channel — it only subscribes/merges/derives. Bridging output into a transmit requires a ViewStream.

**Example** _(from canonical)_:
```js
// channels cannot sendInfoToChannel — broadcast a request event
// that the null relay ViewStream forwards to the transport
static channelServerReconcile$fireRequest(intent) {
  this.sendChannelPayload(
    this.props.serverTestConstants.FIRE_REQUEST_EVENT,
    { url: this.props.serverTestConstants.MUTATE_URL,
      method: 'POST', responseType: 'json', body: intent }
  );
}
// the null view's only job: relay this event via sendInfoToChannel
```
**Refs:** ref:ViewStream.appendToNull, ref:ViewStream.sendInfoToChannel, ref:Channel.getChannel
