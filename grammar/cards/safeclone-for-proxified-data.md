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
- NESTED VALUES FROM PROXIFIED DATA: when a template needs a nested value, do not derive/flatten it in code — bind the dot-path in the template. Deriving replaces a proxified node with an untagged value (an overwrite breaks the data panel's parse; a fallback-empty writes untagged strings into stub items); dot-path binding preserves pairing for present values and degrades to empty-with-no-panel for absent ones. This extends the presence model in `shape-data-for-logicless-template` with a fourth, leaf tier: VALUE presence = bind the dot-path, let absence render empty.
- RENDER-SURFACE HALF OF THE CONTRACT: the CMS emits its own DOM inside every bound element — `spyne-cms-item` wrapping a hitbox and a text node — INCLUDING for absent values, where the text node is empty and the hitbox is how an author fills the field in. Application CSS must never target, hide, or restyle that structure. Two traps in the order an author hits them: `:empty` silently stops matching a bound element under the CMS (it always has an element child), so a rule written against the plain render changes meaning when the CMS loads; and any rule that does hide the empty slot deletes the authoring affordance. An empty bound field is signal — it shows where copy is still required — not a stub to suppress. When absence must genuinely change the render, reshape the DATA (safeClone; add derived keys; never overwrite authored ones) and leave the CMS's formatting alone.

