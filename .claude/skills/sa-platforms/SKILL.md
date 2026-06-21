---
name: sa-platforms
description: Systems-analysis step. Use when the user has an SRS (or needs one) and wants to split a product into platforms and usage flows before wireframing. Ingests the SRS as source of truth, identifies platforms, and scaffolds the platform-first folder structure under C-UX-Scenarios.
---

# Skill: SA — Platforms & Flows (SRS → platform/flow split)

Turn requirements into a platform-first scenario structure. Plan: `DESIGN-SKILL-WORKFLOW.md` §2, decision #7/#8.

## 1. Get the SRS (hybrid — decision #7)
- If the user has an SRS, ingest it as the source of truth.
- If not, GENERATE one from WDS artifacts: `A-Product-Brief/` + `B-Trigger-Map/` + the WDS
  `platform-requirements` template (`_bmad/wds/workflows/wds-1-project-brief/templates/`). Confirm with the user.
- Normalize to a single `SRS.md` in the project as the reference.

## 2. Identify platforms, split by usage
- From the SRS, list the platforms (e.g. mobile mini-app, web dashboard, marketing site, B2B API/admin).
- For each platform, list its usage flows (scenarios) and the personas served.

## 3. Scaffold platform-first folders (decision #8)
Structure: `C-UX-Scenarios/<platform>/<flow>/<page>/`. Use the WDS scripts so specs stay uniform:
- `node _bmad/wds/scripts/wds-init-scenario.js --scenario "<platform> <flow>" --description "..."`
- `node _bmad/wds/scripts/wds-init-page.js --page "<page>" --scenario "<platform> <flow>" --platform "<platform>" ...`
- `node _bmad/wds/scripts/wds-nav.js --all` to wire navigation.
Each page spec maps every value to a token from the central `design-system.md` (no raw hex/px).

## 4. Output
A platform map + the folder tree + per-page WDS specs. Then suggest `/wireframe` per page.
