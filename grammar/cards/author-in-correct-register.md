### author-in-correct-register
`op:author-in-correct-register` · core · CHOOSE

While authoring, place each piece of code in its register deliberately: structural work (wiring, instances, rendering/nesting, channel parsing/combining, emission timing) on the structural side; self-contained computation (formatting, shaping, validation) as pure prior inside trait methods.

**Prior override:** Naive prior organizes by file type and lets structure and computation interleave freely inside methods. Authoring with the register line explicit is what makes the generated code legible to the codemap and durability classifier afterward.

**Specimens (both branches):** _[from whyBlocks — bracket pointers]_

- Generation-time counterpart of the tool-phase durability distinction: the generating agent authors code born correctly partitioned.
- Testability payoff grounded: spyne-ttt-canonical ships unit tests (game-traits.test.js) exercising the pure-prior GameState framework-free — the pure register is independently testable, with a test file as evidence.
- Second register payoff specimen (meme-gen v1): a pure trait static invoked UNBOUND as a plain function (MemeGeneratorTraits.memeGenerator$CheckAndReplaceWithThumb from a fetch map) — purity makes trait methods import-and-call utilities with no binding ceremony.
**Refs:** 01:two-registers-structural-encoding-vs-pure-prior
