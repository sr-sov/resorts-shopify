# Shopify Liquid Architecture & Standards

Based on [Shopify's Liquid API Reference](https://shopify.dev/docs/api/liquid) and our internal "Wow Factor" Developer Profile, this document defines the specific conventions we use when writing and modifying `.liquid` files for this Modern Tropical Villa theme. 

## 1. Deprecated Tags and Filters to Avoid

Shopify routinely updates its templating syntax. Using legacy methods leads to slower rendering, console deprecation warnings, and an eventual mandate to rewrite. 

| Legacy / Deprecated Method | Modern Replacement | Reason |
| :--- | :--- | :--- |
| `{{ image \| img_url: '800x' }}` | `{{ image \| image_url: width: 800 }}` | `img_url` restricts format control. `image_url` automatically serves optimized WebP/AVIF formats based on browser support. |
| `{% include 'snippet-name' %}` | `{% render 'snippet-name' %}` | `include` shares variables across the entire template boundary, hurting performance and creating scope leaks. `render` has strict scoping. |
| `block.settings.product_handle` strings | `block.settings.product` object drops | We no longer pass product handles as strings. Use `type: "product"` in schemas, and Shopify instantly hydrates the entire object (e.g., `block.settings.product.title`). |
| `{{ collection.products.size }}` | `{{ collection.all_products_count }}` | Directly counting objects in memory is slow. Using the raw count object prevents loading massive arrays. |

## 2. Best Practices for Object Access

### Defensive Coding (The "Blank" Check)
Always check if an object is present before trying to pull its nested properties.
```liquid
{% if block.settings.product != blank %}
  <h2>{{ block.settings.product.title }}</h2>
{% else %}
  <h2>Default Title Preview</h2>
{% endif %}
```

### Escaping Data
Any data pulled from user input, product titles, or settings that isn't wrapped in HTML tags should ideally be cast with `escape` or `strip_html` to prevent accidental breakage.
```liquid
{{ product.title | escape }}
```

## 3. Current Project Audit Status

During a preliminary audit, our codebase is mostly compliant, utilizing modern `image_url` heavily in `hero.liquid`, `main-product.liquid`, and `featured-rooms.liquid`. 

However, `sections/welcome-split.liquid` was found using the deprecated `img_url` tag. This has been updated to use the standard `image_url: width: 1200` to maintain compliance.
