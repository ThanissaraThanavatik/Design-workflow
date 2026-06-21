---
name: new-design-project
description: Scaffold a NEW design-system project FROM the Roona template. Use at the very start, before branding, when the user wants to begin a new product/brand's design system. Copies the template structure and tooling into a fresh project folder; does not invent brand values yet.
---

# Skill: New Design Project (scaffold from template)

Stand up a fresh project that follows the Roona template. Roona/ stays untouched.

## Steps
1. Ask for: project name (slug), project type (digital_product / landing_page / website), primary platform(s).
2. Create `<project>/` at the workspace root (NOT inside Roona, NOT liff-codebase).
3. Copy the TEMPLATE skeleton from `Roona/`:
   - `tokens/*.json` (structure kept; values will be replaced in `/brand-intake`)
   - `scripts/*` (gates + `build_shadcn_theme.mjs` + `build_design_system_doc.mjs`)
   - `design-system.html` (layout shell — will be re-themed)
   - copy `CLAUDE.md` as the design-rules reference (or link to Roona's)
   - create empty `components/`, `components/ui/`, `components/specs/`, `C-UX-Scenarios/`
4. Mark the project as "brand not set yet" in a `PROJECT.md` stub.
5. Tell the user the next step is `/brand-intake`.

## Rules
- Do NOT copy `liff-codebase/` or any Roona product content — only the template structure + tooling.
- Do NOT fill brand values here. This step only produces the skeleton.
- Keep the 3-tier token architecture and the gate scripts intact so the new project is verifiable from day one.
