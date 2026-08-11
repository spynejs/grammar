### address-region-by-el$
`op:address-region-by-el$` · core · FORM

Address regions inside a view with el$(sel) — non-referenced, chainable, scoped to the view's root via its [vsid] attribute; accessors and methods hang off the invoked selector. Singular/plural contract: .el always resolves to a single element (first match with a debug warning when several; null when none, mirroring querySelector); .els is always an Array — empty when nothing matches, with Array methods (map, filter, find) available directly (.arr is the legacy alias — prefer els). Class methods (addClass, removeClass, setClass, toggleClass, addAnimClass) apply to every matched element and return the selector for chaining. setActiveItem(activeClass, elSel) removes the class from all matched elements and adds it to the one identity-matched element. exists is true when at least one element matches.

**Prior override:** Naive prior does querySelector and stores the reference. el$ creates no reference — memory-safe by construction, and scoped so a selector cannot escape the view's region.

**Example** _(from spyne-ttt-canonical)_:
```js
static game$UpdateBoard(e) {
  const { squares, winner, isWinner, nextSquareVal } = e.payload;
  this.props.el$('.status').el.innerText = isWinner
    ? `Winner: ${winner}`
    : `Next player: ${nextSquareVal}`;
  this.props.el$('.square').els.forEach((el) => {
    el.innerText = squares[el.dataset.squareNum] || '';
  });
}
// el$ is scoped to the view's root and stores no reference;
// .el is the single match, .els is always an Array
```
_modernized: .arr → .els (legacy alias)_
**Refs:** ref:ViewStream.el$

**Caveats:**
- el$.toggle is a thin alias delegating to toggleClass — both valid; toggleClass is the emitted canonical; .toggle is recognize-never-emit.
- Undocumented behavior (framework source, reference-note pending): omitted-bool toggleClass over MULTIPLE matches derives bool from the FIRST element's state and reuses it — all matches synchronize to the first match's inverted state, not per-element independent toggling.

