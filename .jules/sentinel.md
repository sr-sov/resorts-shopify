# Sentinel Journal

## Critical Learnings Only

## 2024-05-27 - XSS in Shopify Liquid Theme Files

**Vulnerability:** Unescaped user-controlled inputs in Liquid templates, particularly for cart features (`cart.note`, `item.product.title`, `item.properties`).
**Learning:** Even internal template properties that seem safe, like the titles of items in the cart or item properties set before checkout, can be manipulated by an attacker through client-side scripting before the server renders the cart page. Liquid does not automatically escape these outputs unless the `| escape` filter is explicitly used.
**Prevention:** Always append `| escape` when rendering any user-controlled text, including names, notes, and dynamic custom properties (`cart.note`, `property.first`, `property.last`). Avoid `strip_html` for user inputs unless data loss of valid symbols (like `<` or `>`) is acceptable.