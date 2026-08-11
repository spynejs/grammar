### state-machine-in-channel
`op:state-machine-in-channel` · standard · FORM

Durable state and state machines live in Channel trait methods; the channel is the designed home for long-lived state.

**Prior override:** Naive prior keeps state in the component that displays it. Nothing durable persists in a ViewStream instance; durable state lives in a Channel (or SpyneAppProperties).

**Example** _(from spyne-ttt-canonical)_:
```js
export class ChannelTicTacToe extends Channel {
  constructor(name, props = {}) {
    name = 'CHANNEL_TIC_TAC_TOE';
    props.replay = true;
    props.traits = [GameChannelTraits];
    props.stateMachine = GameChannelTraits.gameChannel$CreateStateMachine();
    super(name, props);
  }
}
// durable state rides the channel's props, driven by trait methods;
// replay hands current state to newly born views automatically
```
**Refs:** ref:Channel.constructor, ref:SpyneTrait.constructor, 01:behavior-lives-in-channels-and-their-traits
