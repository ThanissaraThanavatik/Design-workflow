---
name: design-system
description: Umbrella router for the brand-to-design-system workflow. Use when a user wants to start a new design system from a brand/requirement, or asks "where do I continue". Detects project state and routes to new-design-project, brand-intake, shadcn-kit, sa-platforms, or wireframe. Roona is the TEMPLATE, never the target.
---

# Skill: Design System (umbrella router)

Route the user to the right step of the design-skill workflow. Full plan: `DESIGN-SKILL-WORKFLOW.md`.

## Core principle (do not violate)
- **Roona/ is a read-only TEMPLATE/example.** Never edit it, never target `liff-codebase`.
- Every run **starts from a NEW brand/requirement** and **builds a NEW project folder** that follows the Roona template.

## On invocation
1. Ask the user which project folder is the target (or the new project name). If none exists, route to step 0.
2. Detect state in the target project and route:
   - No project skeleton → **`/new-design-project`** (step 0)
   - Skeleton but `tokens/*.json` still template-default / no brand → **`/brand-intake`** (step 1)
   - Tokens filled but no shadcn theme/components → **`/shadcn-kit`** (step 2)
   - Tokens changed → regenerate central doc: `node scripts/build_design_system_doc.mjs`
   - Has design system, needs platform/flow split → **`/sa-platforms`** (step 4)
   - Has page specs, needs screens → **`/wireframe`** (step 5)
3. Present the next 1–2 suggested steps, then hand off to that skill. Do not run a step the user didn't pick.

## Definition of done
From the new project root: `node scripts/accuracy_report.mjs` is green (see workflow doc §5).
