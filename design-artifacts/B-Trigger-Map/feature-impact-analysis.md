# Feature Impact Analysis: ROONA (รู้นะ)

> Features scored against the three personas to scope the MVP. Strategic input for Phase 3/4 UX and Phase 5 build.

## Scoring

**Primary Persona (Thawee, *):** High = 5 | Medium = 3 | Low = 1
**Other Personas (Nattaya, Ploy):** High = 3 | Medium = 1 | Low = 0

**Personas:** 3 · **Max Possible Score:** 11 (Thawee 5 + Nattaya 3 + Ploy 3)
**Must-Have Threshold:** score ≥ 7, OR Primary = High (5)

---

## Prioritized Features

| Rank | Feature | Thawee* | Nattaya | Ploy | Score | Decision |
| ---- | ------- | :-----: | :-----: | :--: | :---: | -------- |
| 1 | ~2.4s screening via LINE | 5 | 3 | 1 | 9 | Must Have |
| 2 | PDF audit log (timestamp, sources, result) | 5 | 1 | 3 | 9 | Must Have |
| 3 | LINE OCR Thai-ID/passport capture | 5 | 3 | 0 | 8 | Must Have |
| 4 | 11-database coverage + 24h refresh | 5 | 0 | 3 | 8 | Must Have |
| 5 | PDPA consent capture + handling | 5 | 0 | 3 | 8 | Must Have |
| 6 | Clear PASS / REVIEW / HIT status (not color-only) | 3 | 3 | 1 | 7 | Must Have |
| 7 | Fuzzy match with similarity score + reason | 3 | 1 | 3 | 7 | Must Have |
| 8 | Thai-first UI copy | 3 | 3 | 0 | 6 | Consider (MVP) |
| 9 | Merchant dashboard — screening history | 3 | 0 | 3 | 6 | Consider |
| 10 | Manual entry fallback (no photo) | 3 | 1 | 0 | 4 | Consider |
| 11 | API access (B2B) | 1 | 0 | 3 | 4 | Consider (post-MVP) |
| 12 | RBAC (role-based access) | 1 | 0 | 3 | 4 | Consider (B2B tier) |
| 13 | Quota / usage tracking | 3 | 0 | 0 | 3 | Defer |
| 14 | Excel export | 1 | 0 | 1 | 2 | Defer |

---

## Decisions

**Must Have MVP (the LINE check loop + proof + coverage):**
- ~2.4s screening via LINE (9)
- PDF audit log (9)
- LINE OCR ID capture (8)
- 11-database coverage + 24h refresh (8)
- PDPA consent capture (8)
- Clear PASS/REVIEW/HIT status (7)
- Fuzzy match with similarity + reason (7)

**Consider for MVP (high value, not blocking):**
- Thai-first UI copy (6) — effectively mandatory for Nattaya; treat as MVP-default
- Merchant dashboard history (6)
- Manual entry fallback (4)

**Defer / later tier:**
- API (4) and RBAC (4) — the B2B/Ploy tier; build after the SME loop is proven
- Quota tracking (3), Excel export (2)

---

## Strategic Rationale

The MVP is the **LINE screening loop**: photo → OCR → ~2.4s result → clear status → PDF audit log,
backed by regulator-grade coverage and PDPA. This is exactly the set that activates Thawee (the ENGINE)
and is effortless for Nattaya (so the audit trail actually exists). Ploy's features (API, RBAC, dashboard
depth) are deferred to a B2B tier so they never complicate the SME flow — directly resolving the tension
noted in the Trigger Map.

> Build note: in `Roona/liff-codebase/`, items 1–7 currently run against a **mocked** `merchant/api.ts`.
> Phase 5 (Mimir) replaces that mock with the real screening backend; done = `accuracy_report.mjs` green.

---

## Related Documents

- **[00 Trigger Map](trigger-map.md)** · **[01 Business Goals](01-business-goals.md)** · **[05 Key Insights](05-key-insights.md)**

---

_Generated with Whiteport Design Studio — strategic input for Phase 4 UX Design and Phase 5 Development._
