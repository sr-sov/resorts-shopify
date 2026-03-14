## 2026-03-14 - Unescaped User Content in Liquid Templates
**Vulnerability:** User-controlled inputs like `cart.note`, `item.properties`, and `product.title` were rendered in HTML without escaping or sanitization, leading to potential Cross-Site Scripting (XSS).
**Learning:** Liquid templates in Shopify themes do not auto-escape output unless explicitly filtered. Attributes like `alt` and HTML text content can execute arbitrary scripts if injected.
**Prevention:** Always apply `escape` to dynamic or user-controlled content (`cart.note`, `item.properties`) and `escape` to safe but dynamic text (`product.title`) in `.liquid` templates. Avoid `strip_html` for user inputs where characters like `<` or `>` may be used in valid input.
