# Design Skill Workflow — Brand/Requirement → Design System → Wireframes

The standard, AI-driven design workflow for the team. Given a **new brand or requirement**, it produces
a **new project's** design tokens, themed component kit, central docs, platform/flow split, and wireframes —
**built to a fixed template**. It is gate-verified and plugs into the WDS strategy pipeline.

---

## 0. The core principle (read this first)

> **Roona is a TEMPLATE, not the target.** `Roona/` is one finished EXAMPLE of the standard. Its
> `tokens/*.json` structure, `design-system.html` layout, `roona-DESIGN.md` spec format, and `scripts/`
> gates are the PATTERN every new project copies. We never extend Roona and we ignore `liff-codebase`.
>
> **Every run starts from a NEW requirement or branding, then builds a NEW project that follows the
> Roona template.** Roona is the reference you point at; the output is a separate project folder.

```
NEW brand / requirement  ──▶  scaffold a NEW project FROM the Roona template  ──▶  fill with new content
        (input)                        (copy structure + tooling)                  (tokens, components, specs)
                                              ▲
                                     Roona/ = read-only template/example
```

---

## 1. Roles of the existing assets (as TEMPLATE)

| Asset (in `Roona/`) | Role in the workflow | Copied into new project? |
|---|---|---|
| `tokens/*.json` (DTCG 3-tier) | **structure template** for tokens | Yes — copied, then values replaced for the new brand |
| `scripts/*` (gates + the 2 new generators) | **tooling template** | Yes — the new project inherits the gates |
| `design-system.html` | **layout template** for the living kit | Yes — re-themed by new tokens |
| `roona-DESIGN.md` | **spec-format template** | Yes — pattern for the new project's spec |
| `CLAUDE.md` | the design rules (3-tier, no-emoji, WCAG, token-by-intent) | Referenced, not copied |
| `.claude/skills/brandkit`, `design-tokens`, ... | the engine the new skills wrap | Referenced |

The two generators added to the template toolkit:
- `scripts/build_shadcn_theme.mjs` — `tokens/*.json` → shadcn CSS-var theme (light+dark). One theme themes ALL shadcn components.
- `scripts/build_design_system_doc.mjs` — `tokens/*.json` → the central human-readable `design-system.md`.

---

## 2. The pipeline (skills, in order)

All skills live in `.claude/skills/` (workspace) so any new project can use them. They READ the Roona
template and WRITE to the active new-project folder. The umbrella `/design-system` routes based on what exists.

| Step | Skill | Input | Output (in the NEW project) |
|---|---|---|---|
| 0 | `/new-design-project <name>` | project name + type | new project skeleton scaffolded from the Roona template (tokens/ structure, scripts/, design-system.html shell, spec format) |
| 1 | `/brand-intake` | new brand identity / persona / position (WDS-aware) | `tokens/*.json` filled for the new brand + `theme.css` + `brand-tokens.md` + a light preview HTML |
| 2 | `/shadcn-kit` | the new tokens | shadcn theme (CSS vars) + `components.json` + product composites `.tsx` + per-component spec `.md` |
| 3 | (auto) | the new tokens | central `design-system.md` (generated; every other .md links here) |
| 4 | `/sa-platforms` | SRS (provided, or generated from WDS Brief+Trigger Map) | platform split: `C-UX-Scenarios/<platform>/<flow>/<page>/` |
| 5 | `/wireframe` | a page spec | themed HTML prototype built from the component kit |

Umbrella: `/design-system` — detects project state and suggests the next step (no-project → step 0; tokens-but-no-kit → step 2; etc.).

---

## 3. Output: what a NEW project looks like

```
<new-project>/                          (NOT inside Roona, NOT liff-codebase)
├── tokens/*.json                        ← from template; values = new brand        [machine SoT]
├── theme.css                            ← generated (build_tokens.mjs)
├── design-system.md                     ← generated central doc                     [human SoT]
├── design-system.html                   ← re-themed living kit (from template layout)
├── brand-tokens.md                      ← brand summary + token tables (dev handoff)
├── scripts/*                            ← gate + generator tooling (from template)
├── components/
│   ├── shadcn theme + components.json    ← every shadcn primitive themed
│   ├── ui/*.tsx                          ← product composites (the React app of THIS project)
│   └── specs/*.md                        ← component specs (link → ../design-system.md)
└── C-UX-Scenarios/
    └── <platform>/<flow>/<page>/         ← SA split + page specs + wireframe HTML
```

---

## 4. Central source of truth + .md references (decision #3)

- **Machine SoT:** `tokens/*.json` (gates validate it). Edit values here only.
- **Human SoT:** `design-system.md` — GENERATED from the json. Never hand-edit its token tables.
- **Every other .md references the central file**, never re-states token values:
  - frontmatter: `source_of_truth: ../design-system.md`
  - prose: link the exact token, e.g. "uses `action.primary` — see [design-system.md](design-system.md)".
- Change a brand value → edit `tokens/*.json` → re-run `build_design_system_doc.mjs` + `build_shadcn_theme.mjs` → every reference is current.

---

## 5. Definition of done (decision #12) — one command

A new project's design work is done when, from the new project root:

```bash
node scripts/accuracy_report.mjs
```

is green. The gate is EXTENDED to cover the new outputs:
- token JSON valid + aliases resolve (existing)
- WCAG contrast light+dark on token pairs (existing)
- **shadcn theme contrast** — generated `--primary/--foreground/--ring/...` pass WCAG (new)
- **composites** — states + responsive + axe + no-emoji (new)
- **wireframes** — no horizontal overflow + no-emoji (new)

Never claim a number you did not run (Roona CLAUDE.md rule 1).

---

## 6. How it plugs into the WDS strategy pipeline

This design skill is the concrete engine for **Freya's Phase 4 (UX Design)** and **Phase 7 (Design System)**:

```
Saga: Phase 1 Brief ─▶ Phase 2 Trigger Map     (WHY / WHO — already built for the Roona example)
                              │
Freya: Phase 3 Scenarios ─────┤
        Phase 4 UX Design ────┼─▶ /sa-platforms + /wireframe   (this workflow)
        Phase 7 Design System ┴─▶ /brand-intake + /shadcn-kit  (this workflow)
                                        │
                              Definition of done = accuracy_report.mjs green
```

- `/brand-intake` is **WDS-aware** (decision #4): if `A-Product-Brief/` + `B-Trigger-Map/` exist, it
  reads tone-of-voice, brand personality, and personas and asks only the gaps.
- Freya's Phase 4/7 workflows call this same skill suite, so the lightweight path (a non-technical user
  running `/brand-intake` for tokens) and the full WDS-agent path share one engine.
- Conflict precedence (from WDS-ROONA-INTEGRATION.md) still holds: no-emoji and WCAG gates win over templates.

---

## 7. Status / build order

- [x] Template tooling: `build_shadcn_theme.mjs`, `build_design_system_doc.mjs` (in `Roona/scripts/`, tested)
- [ ] Skill suite in `.claude/skills/`: `design-system` (umbrella), `new-design-project`, `brand-intake`, `shadcn-kit`, `sa-platforms`, `wireframe`
- [ ] `accuracy_report.mjs` extension (shadcn theme contrast + composites + wireframe checks)
- [ ] Product composites `.tsx` set + per-component specs
- [ ] First end-to-end dry run on a throwaway new brand to validate the template-copy step
