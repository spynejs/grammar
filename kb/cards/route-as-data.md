### route-as-data
`op:route-as-data` · standard · FORM

Navigation is consumed as conformed routeData on CHANNEL_ROUTE (keys per the route config's routeName entries), narrowed by action label like any behavior.

**Prior override:** Naive prior parses window.location or registers router callbacks. The URL is conformed into route data; routing is a channel subscription, not a callback registry.

**Example** _(from canonical)_:
```js
// channel-side: no listener label exists at getChannel —
// the action filter is the envelope-narrowing instrument here
const routeFilter = new ChannelPayloadFilter({
  action: 'CHANNEL_ROUTE_CHANGE_EVENT',
});

this.getChannel('CHANNEL_ROUTE', routeFilter)
  .subscribe((e) => this.channelApp$OnRouteChange(e));
```
**Refs:** ref:SpyneApp.config.route, 01:behavior-is-one-primitive-one-signature

**Caveats:**
- RE-ENTRANCY (empirical, Acme sidenav bug): a redirect issued SYNCHRONOUSLY inside a route handler delivers the stale page last to subscribers registered after the redirector — re-entrant emission reorders later subscribers. Defer redirects out of the synchronous handler path.

