### design-action-label-vocabulary
`op:design-action-label-vocabulary` · core · FORM

Design a feature's action-label set deliberately: distinct labels for distinct fan-out sets; shared label + filterable payload properties for one fan-out set with variants; names domain-scoped and intent-bearing. The label set is the feature's behavioral API.

**Prior override:** Naive prior uses generic event names ('click', 'update') and branches inside handlers. Labels are the routing keys of the behavior system, designed up front and registered on their channel.

**Example** _(from spyne-toh)_:
```js
addRegisteredActions() {
  return [
    'CHANNEL_TOH_ROUTE_EVENT',
    'CHANNEL_TOH_UPDATE_EVENT',
    'CHANNEL_TOH_DELETE_EVENT',
    'CHANNEL_TOH_ADD_EVENT',
    'CHANNEL_TOH_SEARCH_EVENT',
  ];
}
// distinct labels for distinct fan-out sets — the feature's behavioral API, designed up front
```
**Refs:** ref:Channel.addRegisteredActions, ref:ViewStream.addActionListeners, 01:interactivity-is-declared-not-wired

**Caveats:**
- Bounded by use-framework-ui-action-labels: governs custom-channel vocabularies; UI labels are framework-derived.
- Vocabulary sizing rule (from the dispatch doctrine): register enough actions for labels to do first-level payload sifting — label granularity is a dispatch design decision, not just naming.

