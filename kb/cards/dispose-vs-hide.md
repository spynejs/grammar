### dispose-vs-hide
`op:dispose-vs-hide` · standard · CHOOSE

Choose structural teardown (disposeViewStream) vs visibility toggle (pure-prior CSS) by whether the behavior should stop existing. appendToNull is the third option: active behavior, no visible presence.

**Prior override:** Naive prior toggles display:none for everything. Hidden views still subscribe and react; if the behavior should be gone, dispose — the choice is structural, not cosmetic.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Choose hide only for persistent and static UI components such as sidedrawer menu and hamburger components
**Refs:** ref:ViewStream.disposeViewStream, ref:ViewStream.appendToNull
