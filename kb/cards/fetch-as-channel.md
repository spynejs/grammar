### fetch-as-channel
`op:fetch-as-channel` · core · FORM

External data enters via ChannelFetch(channelName, {url, map?, responseType?, pause?, disableSanitize?, ...fetchOptions}). Every outcome is a conformed ChannelPayload: success under {CHANNEL_NAME}_RESPONSE_EVENT, failure under {CHANNEL_NAME}_ERROR_EVENT — both derived from the registered name, registered alongside the channel's actions, narrowable like any action. Responses are cached. Fetched data is always sanitized with the app posture regardless of configured mode (remote data is untrusted by definition); a trusted feed can opt out per-channel with disableSanitize.

**Prior override:** Naive prior is fetch().then(data => handle(data)) — data resolves *to you*, inline at the call site. In SpyneJS it resolves *into the channel system*, uniform-signatured, subscribed like any behavior.

**Example** _(from canonical-app)_:
```js
SpyneApp.registerChannel(
  new ChannelFetch('CHANNEL_FETCH_MODEL', { url: AppModelURL }),
);
// every outcome is a conformed payload: success under CHANNEL_FETCH_MODEL_RESPONSE_EVENT,
// failure under CHANNEL_FETCH_MODEL_ERROR_EVENT — subscribed like any behavior
```
**Refs:** ref:ChannelFetch.constructor, 01:behavior-is-one-primitive-one-signature
