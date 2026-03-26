## 2024-03-11 - XSS in Shopify Liquid Templates
**Vulnerability:** Unescaped user-controlled inputs in Liquid templates (`cart.note`, `item.properties`, `product.title`).
**Learning:** Shopify Liquid automatically executes unsanitized HTML if variables like `cart.note` or `item.properties` are rendered directly without filters. This allows users to inject malicious scripts into the cart page, leading to a Cross-Site Scripting (XSS) vulnerability.
**Prevention:** Always apply the `escape` filter to variables rendering dynamic or user-controlled content (e.g., `item.properties`, `cart.note`, `product.title`) in Liquid templates.
