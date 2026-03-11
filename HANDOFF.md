# Laguna Resort Theme: Handoff & Continuity Document

This document captures the spirit, architecture, and specific prompting strategies used to build the `hotel-shopify-demo` ("Paradise Cove"). It is designed to be fed to an AI assistant (like Gemini/Antigravity) in a new repository/workspace to instantly align it with the established "World-Class" standard, while shifting the context to private resorts in Pansol, Calamba, and San Pablo, Laguna.

---

## 1. Project Context & Business Logic

**The Core Concept:**
We are building a Shopify theme tailored not for e-commerce products, but for **Hotel/Resort Room Bookings**.
*   **The Paradigm Shift:** A Shopify "Product" equals a "Room" or "Private Resort". A Shopify "Quantity" equals "Nights."
*   **Inventory Hack:** Shopify's native inventory is unit-based, not date-based. We capture dates using **Line Item Properties** (`properties[Check-in]` and `properties[Check-out]`) appended to the cart form.
*   **The Goal:** To replace cheap/generic Shopify templates with a high-conversion, premium UI that rivals dedicated travel platforms like Agoda, Airbnb, or luxury hotel sites.

## 2. The Laguna Pivot (New Business Context)

When beginning the new project, inform the AI of the new context:
> "We are adapting our world-class hotel theme for the **Private Resort market in Laguna (Pansol, Calamba, San Pablo)**. The aesthetic should shift from 'Eco-Rainforest Cove' to 'Modern Tropical Private Villa'—think hot spring pools, large group capacities, karaoke, and lush Mt. Makiling backdrops."

---

## 3. Design Language & Architecture

### Visual Standards (The "Anti-Cheap" Mandate)
*   **Typography:** Premium serif pairings for absolute elegance (e.g., `Playfair Display` for headings, `Inter` for body). No default browser fonts.
*   **Spacing:** Generous padding and margins. High `--max-width` (e.g., 1280px). Elements should breathe.
*   **Surfaces:** Use "Glassmorphism" (frosted glass blur effects) for navigation and sticky booking bars.
*   **Shadows:** Deep, soft shadow scaling (e.g., `0 16px 48px rgba(0,0,0,0.1)`) instead of harsh, tight borders.
*   **Micro-interactions:** Smooth hover effects (`transform: translateY(-8px)`) on cards and image pulsing (`scale(1.05)`) on hover.

### Technical Architecture
*   **CSS:** Pure, vanilla CSS variables (`assets/theme.css`). **No Tailwind** unless specifically requested. Define a strict color palette up top (Base, Alt-Background, Text, Accent, Accent-Hover, Error/Urgency).
*   **Shopify 2.0 JSON:** Use JSON templates (`templates/index.json`, `product.json`) linking to highly modular `.liquid` sections.
*   **No Hardcoding:** EVERY piece of textual content (Headings, "Book Now" buttons, Urgency text) MUST be editable via the **Shopify Theme Editor settings** (`{% schema %}`).
*   **Metafields:** Room-specific data (Size, Max Guests, Pool Temp, View) must pull from **Shopify Product Metafields** (e.g., `product.metafields.custom.guests`), falling back to editor block defaults if empty.

---

## 4. Key Features to Carry Over

1.  **The Agoda-Style Urgency Banner:** Dynamic banners that say "Only 2 left for your dates - High Demand!" pulling from `product.variants.first.inventory_quantity`.
2.  **Interactive Masonry Lightbox:** A pure CSS/JS responsive masonry grid on the product page that opens a full-screen, scroll-locked lightbox gallery when a user clicks "Show all photos".
3.  **Sticky Booking Bar:** A form at the bottom of the screen (on mobile) or side (on desktop) that captures Check-in, Check-out, and Guest count, passing them as `properties[]` to the cart.
4.  **Premium Navigation:** Transparent header over the hero image that transitions to a solid/frosted header upon scroll.

---

## 5. Recommended "Initial Prompts" for the New Workspace

Once you have copied the files into your new folder/repository and opened it with the AI, use these prompts sequentially:

### Prompt 1: Context Initialization
> "@workspace I have copied our hotel-shopify-demo into this new repository. Please read the `HANDOFF.md` [or link to this doc] to learn our architecture and standards. We are now building a theme for high-end Private Hot Spring Resorts in Laguna. Update the global CSS variables in `theme.css` to fit a 'Modern Tropical Villa' (warm stones, volcanic grays, lush tropical greens, and hot spring blues). Do not lose our premium spacing and glassmorphism effects."

### Prompt 2: Schema & Content Pivot
> "Review `index.json`, `hero.liquid`, and `main-product.liquid`. Update the default text, tagging, and schema labels from 'Eco-Retreat/Rooms' to fit 'Private Resorts/Villas'. For example, room attributes should now include things like 'Private Pool', 'KTV Access', and 'Max Capacity: 25 pax'."

### Prompt 3: Cart Math Implementation (The Next Step)
> "In our previous session, we established the UI. Now we need the logic. In our `main-cart.liquid` (or before it hits the cart), please implement the javascript necessary to calculate the number of nights based on the `Check-in` and `Check-out` line item properties, and dynamically update the cart item's `Quantity` field to equal that number of nights so pricing multiplies correctly."
