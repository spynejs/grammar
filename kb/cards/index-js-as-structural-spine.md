### index-js-as-structural-spine
`op:index-js-as-structural-spine` · scaffold · FORM

Author index.js as the application's structural spine: SpyneApp.init config (route tree, window events, mediaQueries, debug/strict), registerChannel calls, registerPlugin calls, root render.

**Prior override:** Naive prior treats the entry file as boilerplate to copy. Registrations and config are the existence declarations of the behavior system; a greenfield feature's channel/route needs land here deliberately.

**Example** _(from canonical-app)_:
```js
SpyneApp.init(config);
SpyneApp.registerChannel(new ChannelApp());
SpyneApp.registerChannel(new ChannelLocalStorage());
SpyneApp.registerChannel(new ChannelMenuDrawer());
new AppContainer().prependToDom(document.querySelector('body'));
// the entry file is the behavior system's existence declaration:
// init config, channel registrations, root render
```
**Refs:** ref:SpyneApp.init, ref:SpyneApp.registerChannel, ref:SpyneApp.registerPlugin
