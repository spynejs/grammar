### fetch-conform-map
`op:fetch-conform-map` · core · FORM

Shape the fetch response once via the ChannelFetch map function, at the boundary, before emission. RESERVED-KEYS CLAUSE: 'payload' must not nest inside payload data (the framework warns) — under the filter merge barrel, a nested payload key shadows the filter's payload-predicate addressing ({payload: p => ...}), corrupting the form's grammar. Rename reserved server fields at the map seam (payload → result for mutation responses). Note the deliberate asymmetry: payload.action shadowing the envelope action is embraced (barrel-wins); payload.payload is warned, because it breaks the filter's own addressing rather than meaning something coherent.

**Prior override:** Naive prior shapes the response at each consuming site. Conform once; every subscriber receives the same shaped payload.

**Example** _(from spyne-meme-gen)_:
```js
new ChannelFetch('CHANNEL_MEME_IMG', {
  url: nasaUrl,
  map: (d) => {
    if (Array.isArray(d)) {
      d = d[0];
      d.message = d.message ?? d.url;
    }
    return d;
  },
});
// shape the response once at the boundary, before emission —
// every subscriber receives the same shaped payload
```
**Refs:** ref:ChannelFetch.constructor
