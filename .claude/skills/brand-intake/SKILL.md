---
name: brand-intake
description: Guided brand intake for a NON-TECHNICAL user. Use when someone describes a brand (identity, persona, positioning, mood) and wants design tokens to hand to developers — without asking ChatGPT. Asks plain-language questions, then drives the brandkit engine to emit verified DTCG tokens + theme.css + a brand-tokens.md + a light preview. WDS-aware.
---

# Skill: Brand Intake (brand → design tokens, for a non-technical user)

Turn a plain-language brand description into a verified token kit a developer can use directly.
Wraps the `brandkit` engine; output stops before components (those are `/shadcn-kit`). Plan: `DESIGN-SKILL-WORKFLOW.md`.

## 0. WDS-aware pre-fill (decision #4)
If `design-artifacts/A-Product-Brief/` or `B-Trigger-Map/` exist, READ them first (tone of voice, brand
personality, anti-references, personas). Pre-fill answers and only ask the gaps. Otherwise ask all from scratch.

## 1. Guided intake — ask ONE question at a time, plain language, give examples
Map non-technical answers to what `brandkit` needs (industry, audience, one mood adjective, motion depth, archetype):
1. "ธุรกิจนี้ทำอะไร ขายให้ใคร?" → industry + audience
2. "อยากให้แบรนด์รู้สึกยังไงในคำเดียว?" (เช่น น่าเชื่อถือ / สนุก / หรูหรา) → mood adjective
3. "มีสีหลักในใจไหม หรือโลโก้สีอะไร?" → brand hue seed (optional; else derive from mood)
4. "เป็นทางการแค่ไหน / เคลื่อนไหวเยอะไหม?" → motion depth + formality
5. "มีแบรนด์ที่ชอบเป็นตัวอย่างไหม?" → anchoring archetype (`taste/aesthetic-systems.md`)
Confirm a one-paragraph brand summary back to the user before generating.

## 2. Generate (drive brandkit)
- Generate the brand color ramp in OKLCH (11 shades) + neutrals; verify 500 ≥ 4.5:1 on white, 600 ≥ 3:1.
- Build the semantic + component layers and the DARK overrides (designed, not inverted).
- Write into the NEW project: `tokens/*.json` (3-tier), `theme.css`, and a human `brand-tokens.md` (brand
  summary + a readable token table for the dev).
- Generate the central doc: `node scripts/build_design_system_doc.mjs`.
- Generate a light **preview HTML** (color swatches, type scale, spacing) so the non-technical user can SEE it.

## 3. Verify (definition of done for this step)
From the project root:
- `python3 scripts/validate_tokens.py` (valid JSON + aliases resolve)
- `python3 scripts/validate_contrast.py` (required pairs pass WCAG AA, light AND dark)
Report the real pass/fail. If red, fix tokens and re-run. Never claim a number you didn't run.

## Output to hand the developer
`tokens/*.json` + `theme.css` + `brand-tokens.md` + preview HTML. Then suggest `/shadcn-kit`.
