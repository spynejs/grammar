### error-as-conformed-payload
`op:error-as-conformed-payload` · standard · FORM

Fetch failures enter the channel system as conformed, flat, filterable ChannelPayloads under the derived {CHANNEL_NAME}_ERROR_EVENT action: isChannelFetchError (always true), errorType (FETCH_HTTP_ERROR | FETCH_RESPONSE_PARSE_ERROR | FETCH_UNSUPPORTED_RESPONSE_TYPE | FETCH_UNKNOWN_ERROR), message, status/statusText, url/channelName/responseType, rawBodyPreview, originalErrorMessage. The map function is never called for error payloads. Failure = rejected fetch, non-OK HTTP, unparseable body, unsupported responseType, or throwing map.

**Prior override:** Naive prior is try/catch at the call site and treating errors as exceptional control flow. Errors are behavior: registered actions, narrowed with addActionListeners + ChannelPayloadFilter (e.g. errorType/status for 401 handling), declared structure like any outcome.

**Example:** _pending — no specimen listens for *_ERROR_EVENT yet; surface documented in REFERENCE. Adding an error listener to a public app would ground this and strengthen the fetch cards._
**Refs:** ref:ChannelFetch.constructor
