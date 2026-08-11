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
