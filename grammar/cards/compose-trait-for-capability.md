### compose-trait-for-capability
`op:compose-trait-for-capability` · core · FORM

Add capability to a ViewStream or Channel by composing another trait, declared in props, readable in place.

**Prior override:** Naive prior subclasses to add capability. Richness is breadth (many traits/channels), not depth; composition is inspectable, inheritance is opaque.

**Example** _(from canonical-app)_:
```js
export class ChannelApp extends Channel {
  constructor(name, props = {}) {
    name = 'CHANNEL_APP';
    props.traits = [AppStatusTraits, AppSettingsTraits];
    super(name, props);
  }
}
// capability is composed, declared in props, readable in place — never subclassed
```
_modernized: dropped specimen's sendCachedPayload (deprecated alias; not this op's subject)_
**Refs:** ref:SpyneTrait.constructor, ref:ViewStream.constructor, ref:Channel.constructor, 01:why-the-trace-is-possible

ASSIGNMENT FORM (ruled): assign the array literal — props.traits = [XTraits] — never defensive defaults (props.traits = props.traits || [XTraits]). The ViewStream owns its props; a missing traits array should fail loudly, not silently self-heal.
