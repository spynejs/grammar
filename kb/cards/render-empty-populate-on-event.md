### render-empty-populate-on-event
`op:render-empty-populate-on-event` · standard · FORM

Persistent-tier containers commonly render EMPTY and generate their content on init or sync events (breadcrumb container populating on CHANNEL_APP_INIT_EVENT): the container captures behavior and data; content arrives when the app's state does.

**Prior override:** Naive prior couples existence to content — don't render until there's something to show, or render with placeholder content. Here the container's existence is scaffold-time (persistent tier), its content event-time; views stay stateless and logic stays dedicated and findable, close to the DOM unit it maintains.

**Example** _(from canonical-app)_:
```js
export class NavBreadcrumbContainer extends ViewStream {
  constructor(props = {}) {
    props.tagName = 'nav';
    props.class = 'breadcrumbs';
    props.template = BCTmpl;
    props.traits = [NavBreadcrumbContainerTraits];
    props.channels = ['CHANNEL_APP', 'CHANNEL_ROUTE'];
    super(props);
  }

  addActionListeners() {
    return [['CHANNEL_APP_INIT_EVENT', 'navBreadcrumb$OnAppInitEvent']];
  }
}
// exists at scaffold time, renders empty; content arrives when the app's
// state does — the init event's trait method appends the crumbs
```
**Refs:** ref:ViewStream.onRendered, ref:ViewStream.appendView

**Caveats:**
- TIER NOTE (Acme audit): this op is persistent-tier-scoped; PageItem containers legitimately move the other way even though the call-site shapes look identical — tier decides, not shape.

