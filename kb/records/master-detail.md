### master-detail
`record:master-detail` · standard

**Recognize when:** "click an item to see its details," "list on the left, detail on the right," "product page per item."

A list view and a detail view coordinated through route + selection: selecting an item updates the route (dataset link or transmitted action); the detail view fetches and renders the selected entity.

**Composes:** op:design-route-config-tree, op:author-navigation-as-dataset-links, op:route-as-data, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:declare-action-listeners, op:admit-by-payload-filter, op:dataset-as-payload, op:design-action-label-vocabulary, record:gate-render-on-data
