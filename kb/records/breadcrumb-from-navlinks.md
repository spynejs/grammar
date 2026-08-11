### breadcrumb-from-navlinks
`record:breadcrumb-from-navlinks` · standard

**Recognize when:** "add breadcrumbs," "show where the user is in the hierarchy."

Breadcrumbs generated from navLinks: the container derives each level's route coordinates from the data (which keys each navLevel binds — vocabulary-agnostic), mints one route-scoped item view per level; each item derives visibility/active/selected purely from (route payload + coordinates), applies via el$, maintains aria-current on the terminal crumb, and keeps its own anchor a live dataset ROUTE link.

**Composes:** op:render-empty-populate-on-event, op:data-driven-child-composition, op:route-scoped-view-state, op:react-to-route-diff, op:match-action-labels-by-pattern, op:author-navigation-as-dataset-links
