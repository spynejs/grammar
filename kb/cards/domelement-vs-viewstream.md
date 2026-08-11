### domelement-vs-viewstream
`op:domelement-vs-viewstream` · standard · CHOOSE

Use DomElement for basic HTML/text generation (same constructor interface: tagName, attributes, template, data; renders a DocumentFragment) when the fragment needs no channels, traits, or lifecycle. Use ViewStream when reactive features are needed. DEPTH CLAUSE (merged): when template markup grows deep/repeating enough to carry behavior or lifecycle of its own, that depth is the signal a region has outgrown template/DomElement rendering and earns a ViewStream.

**Prior override:** Naive prior has one component primitive at every scale. SpyneJS has a lighter primitive; over-instantiating ViewStreams for static fragments is structural noise. REFERENCE states it directly: DomElement excludes channel/trait functionality — use ViewStream if reactive features are needed.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- FIRST SPECIMEN (spyne-meme-gen MemeElement): static figure fragment, no channels/lifecycle — DomElement per the criterion. Mechanics grounded: DomElement content enters via native DOM from a trait — this.props.el.appendChild(el.render()) — not appendView.
- loopIndex (0-based) and loopNum (1-based) are auto-injected in every array section — no computed indexing needed.
**Refs:** ref:DomElement.constructor, ref:ViewStream.constructor
