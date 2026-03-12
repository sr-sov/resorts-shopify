## 2024-05-23 - [Liquid Stored XSS in Cart]
**Vulnerability:** Liquid user-controlled properties (`item.product.title`, `property.first`, `property.last`, `cart.note`) rendered directly into HTML without being escaped in `sections/main-cart.liquid`. This allows for arbitrary script injection (XSS) if users submit malicious data in custom booking forms or cart notes.
**Learning:** In Shopify themes, object properties representing user input (like cart line item properties, note fields, and sometimes even product titles if fed by an external sync) must always be explicitly piped through the `escape` (or `strip_html`) filter. Liquid does NOT auto-escape output by default.
**Prevention:** Consistently apply `| escape` on all user-controlled data points rendered into DOM contexts.
