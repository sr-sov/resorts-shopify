# Shopify Theme Development — Verification Guide
For Paradise Cove Eco-Resort

This directory contains a **starter Shopify Liquid Theme** that you can use to prove to your client that the "Tabacon" style is fully editable within the Shopify Admin.

## How to Verify
1.  **Preparation**: Create a ZIP of the `shopify-theme-demo` folder (or push it to a new GitHub repo).
2.  **Upload**: In Shopify Admin, go to **Online Store > Themes > Add Theme > Upload zip file** (or Connect from GitHub).
3.  **Customize**: Once uploaded, click the **Customize** button.
    - You will see that the **Hero Section** text and image are fully editable in the sidebar.
    - You can move sections around or add new ones.
4.  **Booking Logic**:
    - Go to a Product Page (Room).
    - You will see a custom `main-product.liquid` section that includes "Check-in" and "Check-out" date pickers.
    - When a guest books, these dates are passed to the Shopify Cart as "Line Item Properties," exactly what you need for a hotel setup.

## Technical Structure
- `layout/theme.liquid`: The global wrapper (Master CSS, Fonts, Header/Footer).
- `sections/hero.liquid`: A custom section with a `{% schema %}` block. This is what makes it "Editable" in Shopify.
- `sections/main-product.liquid`: The "Agoda-style" room page with custom date inputs.
- `templates/*.json`: Modern Shopify "Online Store 2.0" architecture, allowing Sections everywhere.
