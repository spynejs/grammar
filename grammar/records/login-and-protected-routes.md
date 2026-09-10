### login-and-protected-routes
`record:login-and-protected-routes` · standard

**Recognize when:** "users log in," "members-only pages," "redirect to login when signed out."

Session state held in a channel; protected page-tier routes gated on it: a derived channel (or the stage trait consulting session state) checks auth on route events — unauthenticated navigation to a protected pageId redirects to /login (bridge transmit to ROUTE); login form (form-validate-submit) establishes the session; logout clears and redirects.

**Composes:** op:state-machine-in-channel, op:route-as-data, op:choose-derived-vs-merged-channel, op:bridge-channel-output-to-transmit, op:choose-replay-semantics, record:form-validate-submit, record:authenticated-fetch-flow
