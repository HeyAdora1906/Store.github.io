# El Perfumist catalog architecture

The canonical connected preview is the TanStack Start route `/` in `/home/team/shared/site`. It renders `FragranceHero` first, then mounts the preserved catalog document from `/catalog.html` into the same document flow through `CatalogExperience`. This keeps the collection pathways, fragrance guides, language/region controls, filters, product archive, and existing product data on one scrollable catalog page. The legacy hero node in the mounted catalog is retained as a hidden compatibility node for the catalog's existing reset/filter script; the visible hero is the React shader implementation.

`public/catalog.html` is the static catalog source used by that mount and remains a standalone branded fallback. Its inline fallback hero remains available when the document is served directly without the React route or when WebGPU is unavailable. The React hero keeps the verified shader tree and automatically falls back to its branded crimson/gold composition when the shader cannot initialize.

Hero navigation and CTAs use same-page anchors (`#collectionTitle`, `#fragranceGuide`, and `#controlsContainer`) so they do not leave the integrated catalog route. The demo intentionally does not include a floating or bottom WhatsApp CTA.
