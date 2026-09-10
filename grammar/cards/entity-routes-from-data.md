### entity-routes-from-data
`op:entity-routes-from-data` · standard · FORM

Routes whose identity values come from ENTITY DATA, not authored app-model nodes (heroes/{id}, invoices/{invoiceId}). ONE architecture: the domain channel is a state machine — trait methods combine CHANNEL_ROUTE (and UI/WINDOW as needed) with entity data, resolve the entity per route event, conform (labels like nameUpperCase stamped channel-side), and DELIVER IT IN THE PAGE'S BIRTH PAYLOAD. Two acquisition modes within it: (A) HELD COLLECTION — data already in channel state (seeded statically or by a prior fetch); resolution is a synchronous lookup (ToH). (B) PER-NAVIGATION ACQUISITION — the channel trait acquires on route events via ChannelFetchUtil (the channel-side fetch: channels cannot push into a ChannelFetch, so the util IS the sanctioned in-channel acquisition), composed with select-concurrency-operator, conformed and emitted on response. In both modes the page never fetches for itself. Entity collections generate their own dataset ROUTE links from entity data in template array sections.

**Prior override:** Naive prior either stuffs entities into the authored content model or invents ad-hoc param parsing. The route-only state is not an error — it is the designed seam where authored-content routing hands off to entity-data routing.

**Example** _(from spyne-toh)_:
```js
static tohChannel$GetPageData({ pageId, id }, heroesData = this.props.heroesData) {
  const dataHashObj = {
    heroes: () => heroesData.heroes,
    dashboard: () => heroesData.getTopHeroes(),
    detail: () => {
      const o = heroesData.getHero(id);
      o.nameUpperCase = String(o.name).toUpperCase();
      return o;
    },
  };
  return dataHashObj[pageId]();
}
// mode A (held collection): the channel resolves the entity per route event,
// stamps labels channel-side, and delivers it in the page's birth payload
```
_modernized: dropped specimen's underscore-prefixed local and 404 row_
**Refs:** ref:SpyneApp.config.route, ref:ChannelFetchUtil.constructor, ref:Channel.getChannel, 01:behavior-lives-in-channels-and-their-traits

**Caveats:**
- Breadcrumb/nav labels for entity routes derive from entity data, not navLinks — confirmed (no navLinks in ToH; title via {{heroesArr.nameUpperCase}}).

