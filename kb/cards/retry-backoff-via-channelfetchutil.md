### retry-backoff-via-channelfetchutil
`op:retry-backoff-via-channelfetchutil` · standard · FORM

Retry/backoff and advanced fetch stream behaviors built on ChannelFetchUtil: an observable-wrapped fetch that NEVER errors out — every failure is caught and conformed into the same flat error payload (isChannelFetchError: true) delivered through the next path, so RxJS retry/backoff operators compose without error-channel plumbing. Map applies to successes only.

**Prior override:** Naive prior writes manual retry loops at the call site. Retry is behavior; ChannelFetchUtil is the documented substrate for it.

**Example:** _pending — pattern documented in REFERENCE (ChannelFetchUtil); no specimen composes retry/backoff yet. Specimen wanted._
**Refs:** ref:ChannelFetchUtil.constructor
