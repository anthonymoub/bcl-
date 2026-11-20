# Source stage redesign — build instructions

This folder contains the approved design for the five **Source** pages of the app. All names, tables, columns and numbers in it are **fictional sample data** (a retail-orders example). Use them only to understand layout and behavior. Never hard-code them.

## How to use this design (read first)

**This is a visual redesign of pages that already exist and already work. It is not a spec to rebuild them from scratch.**

1. **Keep all existing functionality.** Every feature, action, filter, data source and behavior the current Source pages have today must keep working. Restyle and re-lay them out to match the design; do not remove or rewrite them.
2. **Design shows something the app doesn't do yet?** Skip it, or leave a clearly marked placeholder, and list it in your summary. Do not build new functionality just to match the mockup.
3. **App has something the design doesn't show?** Keep it, and style it in the same visual language (colors, type, spacing, components in `DESIGN_SPEC.md`).
4. **Use the HTML as styling and layout guidance, not as code to paste in.** Wire the design into the app's existing components, state, routing and data. All values in the screens are mock data. Replace them with the real data the app already loads.

## What's here

| Path | What it is |
|---|---|
| `screens/*.html` | The **main content area** of each page, as plain HTML with inline styles. Open in a browser. This is the source of truth for layout, spacing, colors and type. |
| `screenshots/*.png` | Full-page images including the header and left nav, so you can see where the content sits. Reference only. |
| `DESIGN_SPEC.md` | Colors, type, spacing, reusable components, and how each page gets its data. |

## Prompt for the coding agent

> Rebuild the content area of the five Source pages in the existing app so they match `screens/*.html` exactly (layout, spacing, colors, font sizes, component styles). Use `screenshots/*.png` to see how each page sits inside the app shell, and `DESIGN_SPEC.md` for the shared components and data mapping.
>
> **Hard rules**
> 1. **Do not modify the app header or the left navigation in any way.** No edits, no restyling, no reordering, no new items, no new icons. They already work. The screenshots show them only for context.
> 2. Only change the main content area of these routes, using the existing left-nav entries as the entry points:
>    - Source › Onboard your data source → `screens/01-onboard.html`
>    - Source › Data Catalog → `screens/02-data-catalog.html`
>    - Source › Physical data → `screens/03-physical-data.html`
>    - Source › Ontology → `screens/04-ontology.html`
>    - Source › Review & hand off → `screens/05-review-handoff.html`
> 3. All values shown in the screens are sample data. Bind every field to the data the app already loads (catalog metadata, glossary terms, physical profile, ontology). Do not hard-code any sample names or numbers.
> 4. Build the shared pieces once as reusable components (see `DESIGN_SPEC.md`): context bar, stat card, chip, data table, step footer, column profile card.
> 5. Don't change existing backend services, APIs or data models unless a field the design needs is missing. If it is, list what's missing instead of inventing it.
> 6. Keep the existing routing and state. The table picked in Onboard must stay selected across all five pages (shown in the context bar).
>
> **Definition of done:** each page visually matches its `screens/*.html` at 1440px wide, works at narrower widths (cards wrap, wide tables scroll inside their box), and the header and left nav are byte-for-byte unchanged.

## Page flow

1. **Onboard** — pick a table from the source tree; its details show on the right. Primary action: *Onboard and continue*.
2. **Data catalog** — table description card from the glossary service, then a column list with a detail panel.
3. **Physical data** — one profile card per column (completeness, nulls, distinct, uniqueness, top values, suggested role).
4. **Ontology** — tabs for Terms / Sources & files / Turtle output; term list with an editor beside it.
5. **Review & hand off** — inventory per source plus the pre-curation source graph. Primary action: *Send to Curate*.

Every page ends with the same footer: **Back** (left) · **Step N of 5** (center) · **Continue to <next step>** (right).
