### gate-interactivity-via-class-and-filter
`op:gate-interactivity-via-class-and-filter` · standard · FORM

State-dependent interactivity enforced at ADMISSION: a state-derived class is toggled onto eligible elements (classList.toggle('empty', <state condition>)), and the listener's ChannelPayloadFilter admits by that selector — ineligible elements' events never reach the handler. The class doubles as the readable rule surface and styling hook (tic-tac-toe: filled squares and a won board are unclickable with zero handler checks).

**Prior override:** Naive prior guards inside the handler (if (filled) return; if (won) return) — rules buried in code, re-checked per event. Here the rule is declared once as class+filter; the handler only ever receives legal moves.

**Example** _(from spyne-ttt-canonical)_:
```js
// view trait: the state-derived class marks eligible squares
el.classList.toggle('empty',
  squares[squareNum] === undefined && isWinner === false);

// channel: the filter admits by that class — only legal moves arrive
this.getChannel(
  'CHANNEL_UI',
  new ChannelPayloadFilter({ selector: ['.empty', '.move-btn'] }),
).subscribe(this.gameChannel$OnBtnClicked.bind(this));
// the rule is declared once as class + filter; the handler never
// re-checks state, and the class doubles as the styling hook
```
**Refs:** ref:ChannelPayloadFilter.constructor, ref:ViewStream.el$, 01:interactivity-is-declared-not-wired
