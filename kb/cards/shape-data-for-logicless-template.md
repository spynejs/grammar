### shape-data-for-logicless-template
`op:shape-data-for-logicless-template` · core · MULTI-FORM

Templates carry no logic by design — no if/else, no computed expressions, no helpers, no inverted sections, no partials. All decisions and derivations are pre-computed in SpyneTrait methods; the template receives resolved data.

**Prior override:** Naive prior writes conditionals, ternaries, and helpers in templates. The engine has no syntax for them; each has an idiomatic replacement — object-section conditionals, pre-computed flags, trait-derived values, nested ViewStreams for composition.

**Forms:** _(inventory below; each line links to its REFERENCE example)_

- 'Templates are data files, not code' — the enforcement is by omission: the engine cannot express logic.
- Performance, reasoning and encapsulation is degraded when logic is mixed into data files. Logic is expressed in SpyneTraits.
**Refs:** ref:DomElementTemplate.constructor, ref:SpyneTrait.constructor

**Caveats:**
- TWO-TIER PROFILE (revised per ruling + docs grounding): DomElementTemplate proper allows one level of NESTED ARRAY iteration; the CMS-authored profile is the conservative subset — no loop-inside-loop — so generating models never attempt novel templating syntax. Conditional OBJECT SECTIONS are NOT part of the restriction: element-wrapping sections inside loops are canonical at both tiers ({{#eyebrow}} inside {{#items}} — the documented example).
- Presence model, three data-driven levels: ITEM presence = shape the array (never conditionalize the main loop); BLOCK presence = object section wrapping an element; ATTRIBUTE presence = pre-computed flags with element-level variants (the dynamic-tag flag pattern) — section blocks NEVER appear mid-tag emitting attribute fragments.
- RULED: {{.}} is the canonical current-item token in string-array loops; {{.*}} is an interchangeable alias — recognize, never emit.

