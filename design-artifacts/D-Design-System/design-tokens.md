# Design Tokens — POINTER (design_system_mode: existing)

> ROONA already has a complete, gated token system. WDS Phase 7 does **not** invent tokens here.
> This file points Freya (Phase 7) at the authoritative source and the rules that govern it.

## Source of truth

- **Token files (DTCG JSON):** `Roona/tokens/*.json`
  - `colors.json` (3-tier: primitive → semantic → component + dark mode), `typography.json`,
    `spacing.json`, `shadows.json`, `borders.json`, `breakpoints.json`, `motion.json`,
    `gradients.json`, `opacity.json`, `blur.json`, `sizing.json`, `states.json`, `theming.json`, `data-viz.json`
- **Compiled CSS variables:** `Roona/tokens.css` and `Roona/roona-tokens.css`
  (also `Roona/roona-website/assets/css/tokens.css` for the marketing site)
- **The rules that govern them:** `Roona/CLAUDE.md` → "Token System" (3-tier architecture, naming
  `{category}.{property}.{variant}-{state}`, dark-mode at the semantic level, single-theme consistency).

## Brand anchors (for reference only — edit at source, not here)

- Primary: emerald `#10b981` · Secondary: navy `#121b37`
- Fonts: IBM Plex Sans Thai (body) + Sora (display/numerics)

## How Phase 7 (Freya) works in this project

1. **Read** existing tokens + `CLAUDE.md` Request Router before proposing any component.
2. **Run the duplicate-detection flow** (WDS `wds-7-design-system/steps-c/step-01..07`) against
   `Roona/components/*` BEFORE creating anything new — reuse/extend over invent.
3. **Any new token** is added to `Roona/tokens/*.json` (the source), never duplicated here.
   Then rebuild: `cd Roona && node scripts/build_tokens.mjs`.
4. **Verify on the source** — a new/changed token must pass `cd Roona && python3 scripts/validate_tokens.py`
   and `python3 scripts/validate_contrast.py` (light + dark) before it ships.
5. WDS component specs (`components/*.md`) may be authored here as documentation, but the
   implementation + the gates live in Roona. The gate output is the definition of done — see
   `../../WDS-ROONA-INTEGRATION.md`.

## No-emoji rule (overrides WDS templates)

Roona's `CLAUDE.md` enforces a hard zero-emoji gate (`scripts/check_no_emoji.py`). Some WDS templates
use ✅/❌. In this integrated workflow, **Roona's rule wins**: use lucide icons or plain words
("Good:" / "Avoid:") in every artifact, spec, and UI string.
