---
name: wireframe
description: Turn a page spec into a themed HTML prototype built from the project's shadcn component kit. Use after sa-platforms when the user wants screens/wireframes. Spec-first, then renders a real in-browser prototype that inherits the design tokens and passes the gates.
---

# Skill: Wireframe (spec → themed HTML prototype)

Produce a real, gate-checkable screen from a page spec using the component kit. Plan: `DESIGN-SKILL-WORKFLOW.md` §2, decision #9.

## Steps
1. Read the page's WDS spec under `C-UX-Scenarios/<platform>/<flow>/<page>/` (sections, objects, states).
   If no spec exists, write it first (objects + sections), then continue.
2. Build the prototype HTML from the **component kit** (shadcn theme + composites), referencing
   `theme.css` / `shadcn-theme.css`. Every value comes from a token — no hardcoded hex/px/timing.
3. Use lucide icons (inline SVG, currentColor). No emoji.
4. Save as `C-UX-Scenarios/<platform>/<flow>/<page>/<page>.html`.

## Verify (definition of done)
- `node scripts/verify_responsive.mjs <file>` — no horizontal overflow at 280/320/414px.
- `node scripts/verify_states.mjs <file>` — contrast across default/hover/focus, light + dark.
- `node scripts/axe_audit.mjs <file>` — WCAG 2.2 A/AA.
- `python3 scripts/check_no_emoji.py` — no emoji.
Report real pass/fail; fix and re-run until green. The prototype is a dev-liftable artifact, not a throwaway mock.
