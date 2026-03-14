## 2024-05-18 - Shopify LCP Lazy Loading Anti-Pattern
**Learning:** Found an above-the-fold Hero image configured with `loading="lazy"`. In Shopify themes, lazy loading the LCP (Largest Contentful Paint) image delays critical rendering since the browser waits until the layout is computed before requesting the image, violating the strict LCP < 2.5s metric.
**Action:** Always replace `loading="lazy"` with `fetchpriority="high"` for the primary hero or feature image on page templates to instruct the browser to prioritize the asset immediately.
