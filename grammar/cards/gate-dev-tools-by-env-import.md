### gate-dev-tools-by-env-import
`op:gate-dev-tools-by-env-import` · scaffold · FORM

Dev-only modules (debug plugins, dev channels, test relays) load via environment-gated DYNAMIC import: if (process.env.NODE_ENV === 'development') { import('./dev-tools.js') } — a separate module the bundler code-splits, so development tooling never enters the production bundle.

**Prior override:** Naive prior imports dev tooling statically and gates registration at runtime — the code ships to production anyway. The gate must be at the IMPORT, and dynamic, for the bundler to exclude it.

**Example** _(from canonical-app)_:
```js
if (process.env.NODE_ENV === 'development') {
  import('./dev-tools.js');
}
// the gate is at the IMPORT and dynamic — the bundler code-splits it,
// so dev tooling never enters the production bundle
```
**Refs:** ref:SpyneApp.registerPlugin, ref:SpyneApp.registerChannel
