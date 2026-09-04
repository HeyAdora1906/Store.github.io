# El Perfumist static-site audit (pre-fix)

Reviewed the `index.html` shipped on the default branch before making changes.

- **HTML/structure:** the page uses a large single-file document and inline script/style blocks. The region splash is a fixed dialog without dialog semantics, focus management, or a keyboard escape path. Product cards are links containing the entire card, which prevents adding a separate order action without invalid nested interactive controls.
- **Navigation/paths:** the logo/footer links use `#` and several footer/social links are placeholders. The menu/category controls depend on inline handlers. The script defines render functions but never calls an initial render, leaving the catalog empty behind the splash screen.
- **JavaScript:** no initialization call is present at the end of the script, so categories, brands, products, best sellers, and guide carousels are not populated. The page has no error fallback for failed product images. Search and filter handlers are not keyboard/state-announced.
- **Responsive behavior:** there is a mobile two-column layout, but carousel controls sit outside the padded track and can create clipped controls. Long product titles and controls are not consistently protected from overflow. Body-level `overflow-x:hidden` masks rather than prevents layout overflow.
- **Performance:** 48 remote Amazon image URLs and remote Google Fonts/flag images are loaded from third parties. Images are lazy-loaded, but no dimensions/fetch priority are provided and there is no image error fallback.
- **SEO/metadata:** title still says “MyStore Elite”; there is no description, theme color, canonical URL, Open Graph metadata, or favicon.
- **Accessibility/cross-browser:** the menu and region overlay lack complete ARIA state/labels and focus handling; close/menu buttons rely on visual symbols. Interactive elements use inline `onclick`, and `backdrop-filter` has no fallback. `innerHTML` is used for catalog data without escaping.
- **Forms/WhatsApp:** there is no contact form, WhatsApp number, WhatsApp URL, or product-specific order action. Existing product data contains Amazon links, prices, ratings, and image URLs, but no explicit availability field.

The repair keeps the existing catalog, guide, region/language sections, palette, and typography direction while making the initial render usable, improving metadata and responsive/accessibility behavior, and adding a WhatsApp share/order CTA that can be pointed at the verified business number when the owner supplies it. No WhatsApp number exists anywhere in the repository or history, so no number was invented.

## Redesign implementation (September 4, 2026)
- Added the editorial hero, featured collection pathways, dark product-image treatment, refined cards, and a product detail dialog while retaining the existing catalog data, guides, filters, regional selector, and language controls.
- Kept the approved black/crimson/gold/cream direction and made the intended values explicit in the redesign override: near-black `#0B0B0C`, crimson `#B5342E`, gold/cream `#D4B98C`, and off-white `#F2EFEA`.
- WhatsApp remains intentionally preview-only. `WHATSAPP_NUMBER` is the single configuration point; empty configuration renders disabled buttons and a disabled floating CTA rather than an invalid recipient link.
- No testimonials, scent notes, stock claims, business facts, or other product fields were invented. Detail content renders only existing product fields when present.
