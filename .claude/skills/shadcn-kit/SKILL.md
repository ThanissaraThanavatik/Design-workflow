---
name: shadcn-kit
description: Generate a themed shadcn component kit from a project's design tokens. Use after brand-intake, when the user wants ShadCN components covering all cases plus product-specific composites. Maps tokens to shadcn CSS variables (theming every primitive automatically) and hand-authors the composites shadcn lacks.
---

# Skill: ShadCN Kit (tokens → themed components)

Theme every shadcn component from the new project's tokens, then add the product composites shadcn doesn't ship. Plan: `DESIGN-SKILL-WORKFLOW.md` §2.

## 1. Theme = covers ALL shadcn primitives at once (decision #6)
- Run `node scripts/build_shadcn_theme.mjs --out components/shadcn-theme.css` — maps `tokens/*.json`
  → `--background/--foreground/--primary/--ring/...` for `:root` and dark. Import it once globally.
- Write `components.json` (shadcn config: cssVariables true, base color = neutral, point at the theme).
- Result: any `npx shadcn add <name>` lands pre-themed. Do NOT hand-edit each primitive.
- Icons: lucide (inline SVG, `currentColor`) per the template's icon rules. Never emoji.

## 2. Composites = only what shadcn lacks (hand-author .tsx)
Author these in `components/ui/`, built from shadcn primitives + tokens (no hardcoded values):
stat-card, status-badge, risk-bar, filters bar, empty-state, app-shell / sidebar, page-header
(the set the template's `design-system.html` documents). Each gets a spec in `components/specs/<name>.md`
with `source_of_truth: ../../design-system.md` and links to the exact tokens used.

## 3. Verify (definition of done)
- `node scripts/build_shadcn_theme.mjs` output passes WCAG contrast (extended `accuracy_report.mjs`).
- Composites pass states + responsive + axe + no-emoji.
Report real pass/fail. Then regenerate the central doc and suggest `/sa-platforms` or `/wireframe`.
