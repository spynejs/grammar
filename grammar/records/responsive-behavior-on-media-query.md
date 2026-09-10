### responsive-behavior-on-media-query
`record:responsive-behavior-on-media-query` · standard

**Recognize when:** "behave differently on mobile," "the drawer only below tablet width" — behavior (not just CSS) changing with viewport.

Behavioral (not just visual) response to viewport changes — driven by CHANNEL_WINDOW mediaQueries (matchMedia, CHANNEL_WINDOW_MEDIA_QUERY_EVENT with mediaQueryName) rather than resize math; CSS-only cases explicitly authored as pure prior.

**Composes:** op:window-event-via-channel, op:author-in-correct-register, op:dispose-as-unit, op:declare-action-listeners
