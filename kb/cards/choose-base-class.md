### choose-base-class
`op:choose-base-class` · core · CHOOSE

Given a need, choose which of the six base classes it extends: ViewStream (owns a DOM region), Channel (behavior/state), SpyneTrait (reusable logic), DomElement (static fragment), ChannelFetch (external data), SpynePlugin. The first structural decision of any greenfield feature.

**Prior override:** Naive prior makes 'a component' for everything — behavior, state, and logic all land in the view because the component is the only container the prior knows. In SpyneJS the need's layer (V, B, or L) selects the class, and each class is constrained to its layer.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Every downstream authoring decision is shaped by this one; misplacement cannot be patched later by discipline because the classes are capability-constrained.
**Refs:** ref:ViewStream.constructor, ref:Channel.constructor, ref:SpyneTrait.constructor, ref:DomElement.constructor, ref:ChannelFetch.constructor, ref:SpynePlugin.constructor, 01:vbl-the-spine
