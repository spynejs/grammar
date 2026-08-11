### discretize-continuous-input-at-source
`op:discretize-continuous-input-at-source` · standard · FORM

Continuous inputs (rAF loops, orbit angles, scroll physics, sensors) never reach the channel raw. Three components at the source: SAMPLING POLICY (when to read — per frame, on interaction end, on threshold), BUCKETING (continuous value → semantic name via thresholds; pure prior), CHANGE-GATING (emit only on transitions — return null when the bucket hasn't changed). The channel carries semantic events; everything downstream stays declarative and label-narrowed.

**Prior override:** Naive prior emits per-frame and filters downstream — flooding the channel and pushing gating logic into every consumer. Discretization is the SOURCE's job; the transmit is the boundary where physics becomes meaning.

**Example** _(from spyne-3js)_:
```js
checkAngle(radians) {
  const angleDeg = MathUtils.radToDeg(radians);
  const { index, angleName } = this.getAngleName(180 + angleDeg);
  if (angleName !== this.prevName) {
    this.prevName = angleName;
    return { index, angleName };
  }
  return null;
}
// bucket via thresholds, change-gate on the name — null until the bucket
// changes; the rAF caller transmits only non-null: one event per transition
```
_modernized: specimen's prevNameIndex renamed prevName (it stores the name); console.log dropped_
**Refs:** ref:ViewStream.sendInfoToChannel, 01:behavior-is-one-primitive-one-signature

**Caveats:**
- Sampling-policy sophistication observed: not sampling DURING interaction at all (terminal-frame sampling) — cheaper than per-frame gating when only the settled value matters.
- Companion hazard (grounded, v1 refactor): the continuous source itself (rAF chain) is a single-flight resource — guard against stacked concurrent loops; release the guard at the sampling/exit branch.

- When even one-event-per-transition cannot serve a consumer (a per-frame reader, e.g. WebGL reading a live DOM value), the raw continuous value may ride SpyneAppProperties for that constrained reader under the delivery-envelope exception — see spyneappproperties-vs-channel-state. The channel still carries the semantic transitions; the SpyneAppProperties lane is for the hot-path consumer only.
