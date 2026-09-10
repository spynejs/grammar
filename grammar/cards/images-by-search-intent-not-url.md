### images-by-search-intent-not-url
`op:images-by-search-intent-not-url` · standard · FORM

Generated content never contains invented image URLs. The model authors SEARCH INTENT (imgSearchInput: descriptive query strings, location+subject clues) as a content field; a deterministic pipeline step resolves intent against the image source (Pexels/Unsplash) and writes the real attrImageSrc. Model authors intent; tools resolve resources.

**Prior override:** Naive prior fills src attributes with plausible URLs — a hallucination class with a 100% failure rate. Splitting authoring (intent) from resolution (tool) deletes the class by design rather than policing it.

**Example:** _pending — specimen is the app-builder model (imgSearchInput); follow-up when that repo joins the workspace._
**Refs:** ref:DomElementTemplate.constructor
