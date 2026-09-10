### time-emission-at-sync-point
`op:time-emission-at-sync-point` · standard · FORM

Place sendChannelPayload at the synchronization point that keeps the app coherent — a deliberate structural act inside a trait method.

**Prior override:** Naive prior emits whenever data happens to be ready. Timing an emission is structural work; the sync point is chosen, not incidental.

**Example** _(from spyne-meme-gen)_:
```js
static memeGenerator$GetTxtAndImg() {
  this.mergeChannels(['CHANNEL_MEME_IMG', 'CHANNEL_MEME_TXT']).subscribe(
    this.memeGenerator$OnTxtAndImgReturned.bind(this),
  );
}

static memeGenerator$OnTxtAndImgReturned(e) {
  const { message, title } = e['CHANNEL_MEME_IMG'].payload;
  const { content, author } = e['CHANNEL_MEME_TXT'].payload;
  this.sendChannelPayload('CHANNEL_MEME_GENERATOR_UPDATE_EVENT',
    { message, title, content, author });
}
// the emission waits for the point that keeps the app coherent — here,
// both sources present — not for whenever data happens to arrive
```
**Refs:** ref:Channel.sendChannelPayload, 01:two-registers-structural-encoding-vs-pure-prior
