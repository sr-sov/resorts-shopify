## 2024-05-24 - Default Shopify Hero Image `loading="lazy"`
**Learning:** By default, Shopify's image tags on main heroes often include `loading="lazy"`, which severely degrades Largest Contentful Paint (LCP) because the browser waits until it thinks the user needs it before fetching the asset. This is a common performance anti-pattern.
**Action:** Always ensure above-the-fold images (like Hero banners) use `fetchpriority="high"` and specifically DO NOT use `loading="lazy"`.
