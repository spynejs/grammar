### register-channel-action-vocabulary
`op:register-channel-action-vocabulary` · core · FORM

A Channel declares its accepted actions via addRegisteredActions — pure label registration plus optional ["ACTION", "method"] pairs that auto-wire incoming sendInfoToChannel calls (via onViewStreamInfo) to channel methods. This is the channel's public contract.

**Prior override:** Naive prior emits ad-hoc strings with no registry. Registration enforces consistency, powers debugger validation of unregistered/typo'd actions, and enables action-to-method auto-wiring.

**Example** _(from canonical-app)_:
```js
addRegisteredActions() {
  return [
    'CHANNEL_LOCAL_STORAGE_APP_SETTINGS_INITIALIZED_EVENT',
    [
      'CHANNEL_LOCAL_STORAGE_UPDATE_KEY_REQUEST',
      'localStorage$onChannelUpdateKeyRequest',
    ],
  ];
}
// plain labels register; ['ACTION', 'method'] pairs auto-wire incoming transmits to channel methods
```
**Refs:** ref:Channel.addRegisteredActions, ref:Channel.onViewStreamInfo

**Caveats:**
- Label direction convention (design intent): `[label, method]` pairs are for VIEW→CHANNEL transmits only — the paired method emits a DIFFERENT, plain-registered label (house naming: `…_REQUEST` in, `…_EVENT` out). One label = one direction; a label serving as both a request into a method and an emission to subscribers makes wiring impossible to follow. Emitting a method-paired label via sendChannelPayload logs a misleadingly-worded `not registered` warning (the label IS registered — the framework is objecting to direction): treat it as "you emitted a transmit label." Relay channels whose transmits map 1:1 to emissions register plain strings and dispatch in onViewStreamInfo.
- Custom-event actions (spyne >= 0.26.7): an action deliberately outside the channel's registered vocabulary — a custom event — declares itself with `data-is-custom-event="true"` on the broadcasting element, which suppresses the `not registered within the <CHANNEL> channel` warning for that emission. It is a debug-mode warning suppressor only: it does not register the action, does not affect delivery, and has no effect outside debug mode. The test is string equality against `"true"` — a programmatic payload must carry the string `isCustomEvent: 'true'`, not a boolean. On spyne < 0.26.7 the attribute is inert and the warning still fires.

