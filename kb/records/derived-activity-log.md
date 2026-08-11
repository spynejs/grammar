### derived-activity-log
`record:derived-activity-log` · standard

**Recognize when:** "an activity feed," "audit trail," "history panel built from what already happens."

A persistent log view fed by ONE derived source: the domain channel acquires and conforms other channels (UI filtered, ROUTE), composes the human-readable line channel-side so every conformed payload carries msg, and the log view subscribes once with a family action label (CHANNEL_TOH_.*_EVENT), appending each msg (DomElement into a cached el$ handle); clear via a filtered UI listener.

**Composes:** op:acquire-and-conform, op:conform-incoming-data, op:match-action-labels-by-pattern, op:declare-action-listeners, op:domelement-vs-viewstream, op:assign-view-lifecycle-tier
