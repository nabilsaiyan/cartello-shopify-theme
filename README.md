# Cartello — Shopify Storefront (Custom Liquid Theme)

A custom Shopify theme for **Cartello**, a premium menswear brand — hand-coded in
**Liquid** on Shopify's **Online Store 2.0** architecture (no page builder). This is
a Shopify rebuild of my full-stack Next.js project, [cartello-shop.vercel.app](https://cartello-shop.vercel.app).

> **Live demo:** `nabil-practice.myshopify.com` — development store (storefront password available on request).

---

## Highlights

- **Custom, schema-driven sections** a merchant can edit in the theme editor:
  hero, brand marquee, category grid, featured collections, and an editorial section.
- **Custom product page** — image-swatch colour picker, size selector, **live price /
  discount updates** (vanilla JS), collapsible details, and metafields.
- **Fully styled** collection, search, cart, contact, page and 404 templates.
- **Responsive** throughout, with a mobile navigation drawer.
- Optimised imagery and clean markup — passes `shopify theme check`.

## Tech

- **Shopify Online Store 2.0**, Liquid, vanilla JavaScript, CSS
- Typography: Cormorant Garamond (display) + Inter (body)
- Palette: black `#0a0a0a` / white / gold `#c8a96e`
- Product catalogue imported via CSV (24 products with colour/size variants,
  compare-at pricing, and metafields); **Smart Collections** by product type

## Structure

```
assets/      cartello.css, brand imagery, favicon, icons
sections/    cartello-*.liquid custom sections + rebuilt store templates
snippets/    cartello-product-card + theme utilities
templates/   JSON page templates (Online Store 2.0)
config/ layout/ locales/ blocks/
```

Custom work is namespaced with the `cartello-` (files) and `c-` (CSS) prefixes.

## Local development

```bash
npm install    # dev tooling: Prettier + @shopify/prettier-plugin-liquid
shopify theme dev --store <your-store>.myshopify.com
```

## Author

Built by **Nabil Amhaouch** — full-stack & Shopify developer.
