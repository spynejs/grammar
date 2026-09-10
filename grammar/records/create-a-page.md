### create-a-page
`record:create-a-page` · standard

**Recognize when:** "add an About page," "I need a new section/screen" — a new routed destination with content.

The canonical app's page mechanism: a route/app event carries {pageId, is404}; a stage trait (stage$OnRouteEvent) resolves the Page class from a sparse lookup with PageView as default and nests it into '.page-container' with the payload as data; PageView reads that data to compose children. Constituents consolidate from the annotation pass.

**Composes:** op:default-class-with-sparse-exceptions, op:data-driven-child-composition, op:route-as-data, op:dispose-as-unit, op:nest-view-without-handle, op:skip-replayed-birth-event, op:slice-traits-by-concern
