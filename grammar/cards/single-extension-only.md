### single-extension-only
`op:single-extension-only` · standard · CHOOSE

A module extends one of six public base classes exactly once: ViewStream, Channel, SpyneTrait, DomElement, ChannelFetch, SpynePlugin.

**Prior override:** Naive prior treats inheritance hierarchies as normal design. Extension beyond the single base is an anti-pattern; every added layer is opacity.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_
**Refs:** 01:why-the-trace-is-possible
