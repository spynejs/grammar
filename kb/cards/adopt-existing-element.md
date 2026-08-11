### adopt-existing-element
`op:adopt-existing-element` · rare · GATED
**GATE:** Only when substantial DOM pre-exists and lazy behavior attachment beats re-rendering; adoption is ownership transfer.

A ViewStream can be attached to a pre-existing DOM element instead of rendering and appending: new SomeView({ el: existingElement }) — onRendered fires automatically. Adoption bypasses ONLY the element-rendering step; everything else is identical — parent-child observable chain, broadcastEvents, selectors, listeners, disposal. Adoption is OWNERSHIP TRANSFER: disposeViewStream (from itself or a parent) removes the adopted element and its tree from the DOM like any rendered view's. GATED: the default remains render-and-append; adoption applies when substantial DOM already exists (server-rendered, static, CMS-emitted) and it is more efficient to attach behavior lazily — on interaction or visibility — than to re-render. Adoption completes the four modes of view existence: rendered (default), hidden (CSS, behavior live), null-appended (behavior without presence), adopted (behavior joined to pre-existing DOM).

**Prior override:** Two-sided. (1) The mount-into-existing-root prior (React/hydration instinct) must NOT use adoption as a costume: the scaffold pattern is AppContainer appending to document.body with no authored mount div — adoption never overrides shell-owns-document-concerns-only. (2) Conversely, when large markup pre-exists, the naive move is re-rendering it through views; adoption attaches behavior without regenerating DOM. (3) The jQuery-plugin prior — enhance-and-leave — is wrong here: adopting an element makes its lifecycle the view's; dispose removes the pre-existing markup by design.
**Refs:** ref:ViewStream.constructor, ref:ViewStream.onRendered, ref:ViewStream.disposeViewStream, 01:lifecycle-is-structural-not-reconciled

**Caveats:**
- Disposal semantics: full ownership — adopted trees dispose identically to rendered ones.
- Interaction with dynamic-children-ingress: adopted views declare their own broadcastEvents at adoption, so lazy adoption is also an ingress recipe for pre-existing interactive regions.

