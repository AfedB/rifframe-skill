---
name: rifframe
description: >-
  Pull real, consistent website sections into a project instead of writing
  markup by hand. Use when building or assembling a landing page or marketing
  site and you want ready-made sections (hero, pricing, testimonials, FAQ,
  features, contact, footer, 30+ types in total) as clean Tailwind v4 HTML.
  Sections come from Rifframe's catalog of 250+ blocks that share one set of
  design tokens, so anything you pull stays consistent and restyles to any brand
  by overriding a few CSS variables.
---

# Rifframe

A catalog of 250+ website sections served over MCP and a REST API. Each section
is plain Tailwind v4 markup (no JS, no dependencies) and reads from one set of
semantic design tokens, so any combination stays consistent and restyles to a
brand by overriding the CSS variables once.

## Connect

```
claude mcp add --transport http rifframe https://rifframe.app/api/mcp
```

No API key during the beta. Works with any MCP client over Streamable HTTP
(Claude Code, Cursor, Windsurf, custom agents). Plain HTTP also works: the same
catalog is a REST API at `https://rifframe.app/api/v1/sections`.

## Tools

- `search_sections(query, type?)`: search by intent, in English (the index is
  English-only, so translate the user's intent first). Examples: "pricing with
  billing toggle", "social proof stats". Returns ids, titles, tags, the
  `elements` each section contains, and a live `preview` URL. An empty query
  returns a featured set, one section per type.
- `get_section(id, items?, anchors?)`: fetch one section as Tailwind HTML plus
  typed slots. Each text slot carries its current sample copy and a writing hint
  (length, tone); image slots carry an aspect ratio. `items=N` re-renders the
  main repeatable group (cards, FAQ rows, plans) with N items when the section
  is scalable. `anchors=true` keeps `data-slot` attributes for deterministic
  filling.
- `get_tokens()`: the CSS variable block every section consumes. Paste it once
  into the project's Tailwind v4 CSS entry, override the values with the brand
  colors, and every section pulled afterwards is on-brand.
- `compare_sections(ids)`: thumbnails of up to 4 candidates side by side, to
  pick visually instead of guessing from names.

## Workflow

1. Install the tokens once (`get_tokens`), override a few variables with the
   project's brand colors.
2. Search by intent (`search_sections`). When several candidates fit, show the
   human the top 2 or 3 previews and let them pick.
3. Pull (`get_section`) and drop the markup in. Convert to JSX if needed; it is
   plain classes, no JS.
4. Fill the copy. Each text slot lists its sample and a writing hint; with
   `anchors=true`, target `[data-slot="name"]` directly.
5. For more or fewer items in a list, pass `items=N` when the main group is
   scalable, otherwise clone an occurrence (the `groups` field gives the rule).

## The one rule

Sections are starting points, not locked templates. Rewrite text, add or remove
repeatable items, change the grid, reorder or drop parts. The only thing to keep
is the semantic token classes (`bg-background`, `text-foreground`, `bg-primary`,
`border-border`). They are what keeps every section consistent and restylable
through the token contract.

Full catalog, live previews and the visual editor: https://rifframe.app
