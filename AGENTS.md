# AGENTS.md — Cartello Shopify theme

Guidance for AI assistants (Claude Code, etc.) working on this theme.
`CLAUDE.md` imports this file via `@AGENTS.md`.

## What this is

A **custom Shopify Online Store 2.0 theme** for **Cartello**, a premium menswear
brand. Built on Shopify's minimal reference theme (token-driven, scoped
`{% stylesheet %}` / `{% schema %}`). No page builder — sections are hand-coded Liquid.

## Directory structure

```
assets/      cartello.css (global brand layer), brand imagery, favicon, icons, critical.css
sections/    cartello-*.liquid custom sections + rebuilt store templates (product, collection, cart, search, page, 404, header, footer)
snippets/    cartello-product-card.liquid + theme utilities (css-variables, image, meta-tags)
templates/   JSON page templates (Online Store 2.0), incl. page.contact.json
blocks/      theme blocks
config/ layout/ locales/
```

## Project conventions

- **Naming:** custom files are prefixed `cartello-`; custom CSS classes use the `c-` prefix
  (e.g. `.c-btn`, `.c-hero`, `.c-pdp`). Keep new work consistent with this.
- **Brand tokens** live in `assets/cartello.css` as CSS variables on `:root`:
  `--c-ink #0a0a0a`, `--c-bg #fff`, `--c-muted #737373`, `--c-border #e5e5e5`,
  `--c-accent #c8a96e` (gold), `--c-serif` (Cormorant Garamond), `--c-sans` (Inter).
  Reuse these — don't hardcode brand colours/fonts in components.
- **Full-bleed sections:** the theme wraps every section in a `.shopify-section` CSS grid
  that constrains children to a centre column. A section's root element **must** carry the
  `full-width` class to span edge-to-edge; inner content is centred with `.c-container`.
- **Section CSS/JS** go in the section's own `{% stylesheet %}` / `{% javascript %}` block
  (one of each per file). Global/shared styles go in `assets/cartello.css`.
- **Schema labels** use plain English strings (not `t:` translation keys) for custom
  sections, since this is a single-language store. Storefront-facing copy comes from
  section *settings* so merchants can edit it.
- **Images:** raw `<img>` tags need explicit `width` and `height` (Theme Check rule
  `ImgWidthAndHeight`). The `image_tag` filter adds them automatically. Brand images
  (hero/category/editorial) are optimised JPGs in `assets/`, referenced via `asset_url`.

## Key Shopify/Liquid rules

- `{{ }}` outputs, `{% %}` is logic; add `-` (e.g. `{%- -%}`) to trim whitespace.
- No parentheses in Liquid conditionals — nest `if` blocks for multiple conditions.
- Objects are context-specific (`product` only on product pages, `collection` on collections, etc.).
- `render` for snippets (sandboxed); pass variables explicitly. Snippets/blocks use a `{% doc %}` header.
- Guard optional data with `!= blank` so empty settings/metafields don't render broken markup.

## Dev workflow

```bash
npm install                                    # Prettier + @shopify/prettier-plugin-liquid
shopify theme dev --store <store>.myshopify.com   # local preview at 127.0.0.1:9292
shopify theme check                            # lint (keep it clean before pushing)
shopify theme push --live --allow-live         # publish to the live theme
```

- Prettier is configured (`.prettierrc.json`) with the Shopify Liquid plugin; format on save.
- Editing a `.liquid` file syncs to the dev theme automatically; theme-editor changes stay
  server-side until `shopify theme pull`.
