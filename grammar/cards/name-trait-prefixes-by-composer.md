### name-trait-prefixes-by-composer
`op:name-trait-prefixes-by-composer` · standard · FORM

A trait's prefix carries its COMPOSER'S identity: which class family it composes into and which host specifically — channelServerReconcile$ (a channel's trait), not reconcile$; channelServerTests$, not serverTests$. File names follow (channel-server-optimistic-reconcile-traits.js). Prefixes are API surface — every method name carries them — so the prefix is where a method self-locates.

**Prior override:** Naive prefixes name the CONCERN only (reconcile$, serverTests$): correct-looking, and a bare concern-prefix in a stack trace, search result, or generated citation requires forensics to place. The composer-qualified prefix answers 'whose method is this, channel or view, which host' at first glance.

**Example** _(from canonical-app)_:
```js
export class ChannelMenuDrawerTraits extends SpyneTrait {
  constructor(context) {
    let traitPrefix = 'channelMenuDrawer$';
    super(context, traitPrefix);
  }
}
// the prefix carries the composer — channel + which host — so every method
// self-locates in a stack trace, search hit, or citation
```
**Refs:** ref:SpyneTrait.constructor, 01:the-dom-is-meaningful-structure
