### window-event-via-channel
`op:window-event-via-channel` · standard · FORM

Global browser events arrive as payloads on CHANNEL_WINDOW, configured at init (event list, debounce for scroll/resize/orientation, mediaQueries via matchMedia emitting CHANNEL_WINDOW_MEDIA_QUERY_EVENT with mediaQueryName).

**Prior override:** Naive prior calls window.addEventListener or matchMedia in application code. Global events are channel payloads; the init config is the declaration.

**Example** _(from spyne-3js)_:
```js
// SpyneApp.init config — the declaration
WINDOW: {
  listenForScroll: true,
  listenForWheel: true,
  debounceMSTimeForResize: 24,
},

// any view narrows the global event like any behavior
addActionListeners() {
  return [['CHANNEL_WINDOW_RESIZE_EVENT', 'threejs$onWindowResize']];
}
// global browser events are channel payloads — no window.addEventListener
// in application code
```
**Refs:** ref:SpyneApp.config.window
