### match-action-labels-by-pattern
`op:match-action-labels-by-pattern` · core · MULTI-FORM

addActionListeners is an ORDERED DISPATCH TABLE with first-match short-circuit: per payload, an EXACT action name takes precedence over patterns REGARDLESS of position (empirically confirmed: pattern declared first, exact second — exact wins every time); each payload triggers one match. Among overlapping PATTERNS, precedence is unpinned — never rely on it; the doctrine's dedup rule (payload filter on overlap) makes the question unreachable. Ordering specific-entries-first is a readability practice, not a mechanic. Short-circuit holds PER SUBSCRIPTION PATH; co-firing across paths (multiple channel subscriptions; extended-streams fallback) has been observed and is a separate phenomenon — one method per payload per subscription, not per view. Matching per entry: exact-key fast path, then the pattern as an UNANCHORED RegExp (matches anywhere — a bare prefix matches its whole family; the .* is documentary; regex-special characters in labels are live syntax). Guidance: write patterns specific enough that ordering never matters; when layering, declare specific entries BEFORE catchalls — an early broad pattern silently shadows every later specific one. DOCTRINE (three rules that make the dispatch fine print unreachable): (1) register enough actions that labels do the first-level sifting of payloads, for ViewStreams and custom channels alike; (2) match as precisely as possible — precision, not ordering, is the primary tool; (3) where two patterns could match the same action, add a payload filter as the dedup guard.

**Prior override:** Naive prior names labels ad hoc, making glob patterns either useless or dangerously over-matching. Family-prefixed naming makes a glob listener a deliberate, bounded subscription.

**Forms:** _(inventory below; each line links to its REFERENCE example)_

- Some DomElements require methods to execute on multiple behavioral payloads.
- Infix wildcard grounded (spyne-ttt-canonical): 'CHANNEL_TIC_TAC_TOE.*_CHANGE_EVENT' — family patterns are not prefix-only; mid-string wildcards narrow to a label KIND across the family.
- Family-handler pattern + its boundary (drawer vs ttt TODO): a family-subscribed handler may read e.action when members share logic and the action DERIVES a value (SHOW/HIDE → boolean → one toggle). When the handler becomes a per-label switch routing to different logic, split into per-label listeners — the tic-tac-toe game$UpdateBoard TODO marks exactly that threshold.
**Refs:** ref:ViewStream.addActionListeners

**Caveats:**
- Matcher grounded from framework source (findStrFromRegexArr): exact key → array membership → per-pattern unanchored RegExp test.

