### global-loading-indicator
`record:global-loading-indicator` · standard

**Recognize when:** "a spinner/progress bar while anything is loading," "the app-wide busy state."

One indicator view derived from the union of in-flight fetch channels; shows while any request is pending.

**Composes:** op:choose-derived-vs-merged-channel, op:choose-merge-emission-mode, op:conform-incoming-data, op:state-machine-in-channel, op:declare-action-listeners
