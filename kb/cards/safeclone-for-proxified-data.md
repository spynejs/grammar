### safeclone-for-proxified-data
`op:safeclone-for-proxified-data` · conditional · FORM

When the SpyneCMSPlugin is in play, its map method (installed as a ChannelFetch map) returns data in the original shape but 'proxified' — metadata with IDs on each nested object, which DomElementTemplate checks to inject non-displaying HTML content and the interactive UI elements that form the WYSIWYG system. Handling contract: pass the object to DomElementTemplate AS-IS when unmodified; when modifying it in code — adding properties, or even changing values — use safeClone (import { safeClone } from 'spyne'), which produces the updated object with proxy metadata intact. Property flow is one-way: code-added properties carry no proxy metadata and are invisible to the CMS (not editable, not persisted); only properties added via the CMS UI update the original ChannelFetch data source. Detection: proxified objects are identifiable via the __cms__isProxy flag (e.g. props.data.__cms__isProxy in a view, e.payload.__cms__isProxy on a channel emission) — the runtime check that tells code which mutation contract applies.

**Prior override:** Naive prior treats fetched data as plain JSON and reaches for spread, Object.assign, structuredClone, or a generic deep clone to modify it — every one of which silently strips the proxy metadata, breaking WYSIWYG editing with no error surfaced. The failure is invisible at modification time and appears only as dead editing UI. safeClone is the sanctioned mutation path; payload.clone() is for ordinary frozen payloads, not proxified CMS data.

**Example** _(from canonical-app)_:
```js
import { safeClone } from 'spyne';

props.data = safeClone(props.data);
props.data.href = SpyneAppProperties.getHrefFromData(props.data);
// modifying data that may be CMS-proxified: safeClone keeps proxy metadata
// intact; spread/structuredClone silently strip it and kill WYSIWYG editing
```
**Refs:** ref:ChannelFetch.constructor, ref:DomElementTemplate.constructor, ref:ChannelPayload.clone

**Caveats:**
- Currently local-JSON only; designed for future adapters carrying source-appropriate proxy info (NoSQL, SQL, external CMS sources) — the handling contract is intended to be source-agnostic.

