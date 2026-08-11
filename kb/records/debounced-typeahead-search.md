### debounced-typeahead-search
`record:debounced-typeahead-search` · standard

**Recognize when:** "search as you type," "autocomplete," "suggestions after a pause in typing."

Input events debounced, in-flight requests cancelled in favor of the latest (switchMap), results conformed and rendered.

**Caveats:**
- Sibling variant grounded: LOCAL-SYNCHRONOUS search (in-memory collection, per-keystroke, no debounce — debounce exists to limit requests, and there are none) with cross-search delta rendering via dispose-by-negative-filter. The record as written is the FETCH variant.

**Composes:** op:declare-broadcast-events, op:escape-to-raw-rxjs, op:select-concurrency-operator, op:fetch-as-channel, op:pause-fetch-vs-autofire, op:conform-incoming-data
