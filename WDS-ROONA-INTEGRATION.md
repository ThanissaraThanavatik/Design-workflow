# WDS × Roona — Integrated Design Workflow

How the **BMad Whiteport Design System (WDS)** methodology is wired to the **existing Roona
design-system engine**. WDS provides the upstream strategy + UX pipeline; Roona provides the
downstream token + gate + code engine. This file is the contract between them.

> **Two ways Roona is used.** (1) As the worked EXAMPLE in this repo (what this file documents).
> (2) As a read-only TEMPLATE for NEW projects — see **`DESIGN-SKILL-WORKFLOW.md`**: a new brand/requirement
> is scaffolded into a fresh project that COPIES Roona's token structure, gates, and spec format, then is
> filled with new brand content. The design-skill suite (`.claude/skills/`: `design-system`,
> `new-design-project`, `brand-intake`, `shadcn-kit`, `sa-platforms`, `wireframe`) is the concrete engine
> for Freya's Phase 4 (UX Design) and Phase 7 (Design System). `liff-codebase/` is out of scope.

```
Design-workflow/                 ← workspace root (this integration lives here)
├── _bmad/wds/                    WDS module (agents, workflows, scripts) — vendored
│   └── config.yaml               tuned for Roona: th, design_system_mode=existing, gate-wired
├── _bmad/custom/                 optional persona/menu overrides (empty)
├── design-artifacts/             WDS outputs (A–E + _progress design log)
├── Roona/                        the design + product engine (tokens, gates, code, CLAUDE.md)
└── bmad-method-wds-expansion/    upstream module source (reference only)
```

---

## 1. Why combine them — the gap each fills

| | Upstream: WHY / WHO / WHAT | Downstream: BUILD / VERIFY |
|---|---|---|
| **WDS** | Strong — 8 phases, Saga/Freya/Mimir, brief → trigger map → scenarios → specs, handoffs, design log | Weak — Phase 7 emits loose markdown tokens/specs |
| **Roona** | Missing — jumps straight to "build a component/page" | Strong — DTCG tokens, 19 gate scripts, code gen, 138 DS specs |

**The seam:** WDS phases 1–4 produce the strategy + specs Roona lacks. Roona's tokens + gates become
the *execution + definition of done* WDS Phase 5/7 lacks.

```
 Saga (Phase 1-2)         Freya (Phase 3-4, 7)            Roona engine
 Product Brief ─► Trigger ─► Scenarios ─► UX specs ─────► tokens/*.json  (single source of truth)
   ▲ seeded from              │                             + scripts/*.mjs  (gates)
   PRODUCT.md                 └── Phase 7 design system ──► design_system_mode = existing
                                                            │
 Mimir (Phase 5) ───────────── builds ──────────────────►  accuracy_report.mjs GREEN = DONE
```

---

## 2. Phase → Roona-gate mapping (the wiring)

Run gate commands from inside `Roona/`. These are Roona's real scripts (`Roona/scripts/`).

| WDS phase | Agent | Output (in `design-artifacts/`) | Roona gate / asset that verifies or executes it |
|-----------|-------|----------------------------------|--------------------------------------------------|
| 1 Product Brief | Saga | `A-Product-Brief/project-brief.md` | — (seeded from `Roona/PRODUCT.md`) |
| 2 Trigger Map | Saga | `B-Trigger-Map/` | — strategy only |
| 3 UX Scenarios | Freya | `C-UX-Scenarios/` | — |
| 4 UX Design (specs) | Freya | `C-UX-Scenarios/<scenario>/<page>/` | Map every spec value to a token in `Roona/tokens/*.json` (no raw hex/px). |
| 7 Design System | Freya | `D-Design-System/` (pointer) | `validate_tokens.py`, `validate_contrast.py`, `lint_hardcodes.py`, `build_tokens.mjs` |
| 5 Build | Mimir | code in `Roona/` | **`node scripts/accuracy_report.mjs`** = definition of done (all gates, light+dark) |
| 6 Assets | Freya | generated assets | `Roona/scripts/measure_render.mjs`, `taste_audit.mjs` |
| 8 Evolution | Freya/Mimir | updated artifacts | re-run `accuracy_report.mjs` after each change |

### The single rule that joins the two systems

> **A WDS deliverable is not "done" until the corresponding Roona gate is green.**
> For build/UI work that means, from `Roona/`:
> ```bash
> node scripts/accuracy_report.mjs      # tokens + contrast + spec + no-hardcode + no-emoji + real-render WCAG + responsive
> ```
> Report the actual `N/N` line — never claim a number you didn't run (Roona CLAUDE.md rule 1).

---

## 3. Conflicts resolved (precedence rules)

When WDS and Roona disagree, the resolution is fixed so the workflow stays consistent:

1. **Tokens** — Roona `tokens/*.json` is the single source of truth. WDS Phase 7 does **not** create a
   parallel token set; it consumes Roona's (`design_system_mode: existing`). New tokens go to the
   Roona source, then `build_tokens.mjs`. See `design-artifacts/D-Design-System/design-tokens.md`.
2. **Emoji** — Roona's hard no-emoji gate (`check_no_emoji.py`) **overrides** WDS templates that use
   ✅/❌. Use lucide icons or plain words everywhere.
3. **Accessibility** — Roona's WCAG 2.2 gates are authoritative and run on the real render; they
   outrank any "looks fine" claim in a WDS spec.
4. **Language** — Thai-first (WDS `config.yaml`: `communication_language: th`), English only for
   regulatory terms — matches `PRODUCT.md`.
5. **Decision framework** — Roona CLAUDE.md priority order (User Needs > Accessibility > Consistency >
   Aesthetics > DX) governs; WDS taste/visual choices serve tier 4 only.

---

## 4. How to use it (operating manual)

### Activate an agent
In this Claude Code session, tell Claude:
```
Read and activate _bmad/wds/agents/wds-agent-saga-analyst/SKILL.md
```
Agents available: `wds-agent-saga-analyst` (Saga, phases 1–2), `wds-agent-freya-ux` (Freya, phases
3–4/6–8), `wds-agent-mimir-builder` (Mimir, phase 5). On activation each agent reads
`_bmad/wds/config.yaml`, loads the design log, and offers next steps.

> Note: WDS's optional `~/.claude/` sync and BMAD-core `resolve_customization.py` are **not** required —
> each agent's SKILL.md has a documented fallback (read the three `customize.toml` files directly), and
> the sync step never blocks activation. Everything needed is vendored under `_bmad/wds/`.

### Typical first run (brownfield Roona)
1. **Saga** → review the seeded `A-Product-Brief/project-brief.md`, then run Trigger Mapping (Phase 2).
2. `/wrap freya` → **Freya** → UX Scenarios (Phase 3) for the LIFF check flow + dashboard.
3. Freya → UX Design specs (Phase 4), every value mapped to a Roona token.
4. Freya → Phase 7: run duplicate detection against `Roona/components/*`; add any new token to
   `Roona/tokens/`, then `cd Roona && python3 scripts/validate_tokens.py && python3 scripts/validate_contrast.py`.
5. `/wrap mimir` → **Mimir** → Phase 5 build (top target: replace the mocked
   `Roona/liff-codebase/merchant/api.ts` with the real screening backend). Done when
   `cd Roona && node scripts/accuracy_report.mjs` is green.

### WDS structure scripts (deterministic, optional)
`_bmad/wds/scripts/wds-init-scenario.js`, `wds-init-page.js`, `wds-nav.js`, `wds-add-object.js`,
`wds-add-spacing.js`, `wds-validate.js` — create/validate page-spec scaffolding. Agents invoke these
with CLI flags; they own folder/file structure so specs stay uniform.

---

## 5. Status

- [x] WDS module vendored → `_bmad/wds/` (647 files)
- [x] `config.yaml` tuned for Roona (Thai, `design_system_mode: existing`, gate-wired)
- [x] `design-artifacts/` A–E skeleton + design log seeded
- [x] Phase 1 Product Brief seeded from `Roona/PRODUCT.md` (needs Saga review)
- [x] Phase 7 design-tokens pointer → Roona token source
- [ ] Phase 2 Trigger Map (run Saga)
- [ ] Phases 3–4 Scenarios + UX specs (run Freya)
- [ ] Phase 5 build: real screening backend (run Mimir) → `accuracy_report.mjs` green
