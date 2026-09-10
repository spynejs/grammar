### app-scaffold
`record:app-scaffold` · scaffold

**Recognize when:** "start a new SpyneJS app," "set up the project" — index.js, registrations, the shell, the folders.

The greenfield SPA skeleton: init config (route tree, window events, media queries, mode/strict posture), channel registrations, shell ViewStream, nav rendered from config, route-driven page region.

**Caveats:**
- Directory jurisdiction (refactor ruling): channels/ holds Channel classes ONLY; registration helpers and similar live in traits/utils/ (util-register-channel-server-tests.js). Bounded-surface findability, directory tier.

**Composes:** op:index-js-as-structural-spine, op:design-route-config-tree, op:author-navigation-as-dataset-links, op:render-nav-from-config, op:decompose-region-into-viewstreams, op:register-channel-upfront, record:route-driven-page-swap
