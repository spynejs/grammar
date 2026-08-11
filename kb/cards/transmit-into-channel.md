### transmit-into-channel
`op:transmit-into-channel` · core · FORM

Outbound communication from a view: sendInfoToChannel(channelName, payload, action?) from a ViewStream trait. The action parameter is OPTIONAL: with an action, a registered ['ACTION','method'] pair auto-invokes the paired channel method; an UNPAIRED action (registered as a plain string, no method) also routes to onViewStreamInfo, carrying its action; with the action omitted, the payload routes there too. Full routing: paired action → method; unpaired action → onViewStreamInfo; no action → onViewStreamInfo. The relay receiver (onViewStreamInfo cloning and re-emitting via sendChannelPayload) is the validate-and-rebroadcast pattern for channels whose transmits map 1:1 to emissions.

**Prior override:** Naive prior calls another component's method, lifts state to a shared parent, or emits a custom DOM event upward. Views are isolated; the sole outbound move is sendInfoToChannel.

**Example** _(from spyne-3js)_:
```js
static threejs$OnFrameUpdate(controlRads) {
  const angle = this.props.angleUtils.checkAngle(controlRads);
  if (angle !== null) {
    this.sendInfoToChannel('CHANNEL_THREEJS', angle,
      'CHANNEL_THREEJS_ANGLE_CHANGE_EVENT');
  }
}
// the sole outbound move from a view; the action routes to the channel's
// paired method or to onViewStreamInfo
```
_modernized: instance trait method → static (majority-specimen house form)_
**Refs:** ref:ViewStream.sendInfoToChannel, ref:Channel.onViewStreamInfo, 01:views-are-isolated
