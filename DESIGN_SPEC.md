# Design spec — Source stage content area

Applies to the **main content area only**. Header and left nav are out of scope and must not change.

## Tokens

### Color
| Token | Value | Use |
|---|---|---|
| `bg-page` | `#F6F7F9` | Page background behind cards |
| `bg-surface` | `#FFFFFF` | Cards, tables, panels |
| `bg-subtle` | `#F9FAFB` | Table headers, inner panels, preview pane |
| `border` | `#E5E7EB` | Card and table borders |
| `border-row` | `#F1F2F4` | Row dividers inside cards and tables |
| `text` | `#111827` | Primary text |
| `text-muted` | `#4B5563` | Secondary text, labels |
| `text-subtle` | `#6B7280` | Helper text, meta |
| `accent` | `#B3121B` | Primary button, selected states |
| `accent-tint` | `#FBE9EA` | Selected row / selected tree node |
| `success` | text `#166534` on `#DCFCE7` | "Ready", ACTIVE, done ticks |
| `warning` | text `#92400E` on `#FEF3C7` | PROPOSED, "Code" role |
| `info` | text `#1E40AF` on `#DBEAFE` | "Identifier" role, source tags |

Completeness bar fill: `#16A34A` (≥ 99%), `#65A30D` (90–99%), `#D97706` (< 90%). Track `#F3F4F6`.

Suggested-role chips: Identifier `#1E40AF/#DBEAFE`, Code `#92400E/#FEF3C7`, Flag `#6B21A8/#F3E8FF`, Timestamp `#0F766E/#CCFBF1`, Name / label `#374151/#F3F4F6`.

### Type
- UI: **Inter** 400/500/600/700. Identifiers (table, column, schema names, code): **JetBrains Mono** 500/600.
- Page title 28px/700, letter-spacing −0.015em. Section title 16px/700. Body 13–14px. Labels 11–12px, 700, uppercase, +0.05em tracking.
- Numbers use `font-variant-numeric: tabular-nums`.

### Spacing & shape
- Content padding 28px top/bottom, 36px sides. Gap between sections 20px; inside cards 12–16px.
- Card radius 12px, 1px `border`. Buttons and inputs 8px radius, **44px tall**. Chips 24px tall, fully rounded.
- Icons: 16–18px stroke icons, 1.8px stroke, `currentColor`.

## Reusable components

| Component | Where | Notes |
|---|---|---|
| **Page header** | All | Breadcrumb `Source › <page>`, title, one-line description, optional actions on the right (e.g. Upload DDL / View DDL). |
| **Context bar** | Pages 2–5 | Table icon, table name (mono), `title · source › schema`, *Change table* link. Shows the table picked in Onboard. |
| **Stat card** | All | Label, big number, sub-text, optional progress bar. Usually 4 in a row. |
| **Chip** | All | Status, type and role labels (colors above). |
| **Data table** | Catalog, Physical | Uppercase header row on `bg-subtle`; scrolls horizontally inside its own box on narrow screens. |
| **Source tree** | Onboard | Source › schema › table, guide lines per level, expand/collapse, checkbox per table, count on the right, selected row tinted. |
| **Selected-table preview** | Onboard | Name, path, 2×2 stat tiles, summary. Sits beside the tree in one panel. |
| **Column list + detail** | Catalog | Left: filterable column list. Right: description and column fields. |
| **Column profile card** | Physical | Name + type, role chip, completeness bar, nulls / distinct / uniqueness, top 3 values with share bars. 3 per row. |
| **Term list + editor** | Ontology | Filters, bulk Keep / Discard, term rows (term, type, status, source); editor panel for the selected term. |
| **Step footer** | All | Back · Step N of 5 · Continue to <next>. Same position on every page. |

## Data mapping (generic)

| Page | Field in the design | Comes from |
|---|---|---|
| Onboard | Sources, schemas, tables, row counts | Registered sources + warehouse metadata |
| Onboard / Catalog | Table title, description, glossary | Glossary service / metadata catalog |
| Catalog | Column name, type, description, business term, term description | Metadata catalog + glossary service |
| Physical | Total rows, null count, non-null count, distinct count, top values | Profiling results |
| Physical | Completeness % | non-null ÷ total rows |
| Physical | Uniqueness % | distinct ÷ non-null |
| Physical | Suggested role | Rule on type + distinct count (TIMESTAMP → Timestamp; 2 distinct → Flag; ≤ 20 → Code; many distinct → Identifier or Name/label). Shown as a suggestion only. |
| Ontology | Terms, types, status, source file, Turtle output | Ontology store / loaded files |
| Review | Inventory counts, source graph | Aggregates of the four previous steps |
