# Project Brief: ROONA (รู้นะ)

> Complete Strategic Foundation
> STATUS: SEEDED from `Roona/PRODUCT.md` on 2026-06-21 — needs Saga review/deepening (do not treat as final).

**Created:** 2026-06-21
**Author:** Thanissara
**Brief Type:** Complete (seeded, brownfield)

---

## Vision

ROONA (รู้นะ) is a RegTech platform that screens individuals against AML, PEP, and Sanctions
databases in under 5 seconds, delivered via LINE OA — no app install required. It exists because
Thai SMEs face AMLO compliance obligations but cannot afford enterprise KYC tools. Success looks
like a shop owner completing a check faster than they could Google the name, with a PDF they can
hand to an auditor.

Two surfaces: a brand landing page (`Roona/roona-website/index.html`) that converts SME owners to
sign up, and a product app (LINE LIFF + merchant dashboard, `Roona/liff-codebase/`) where screening
happens.

---

## Positioning Statement

For Thai SME owners legally required to screen customers against AML/PEP/Sanctions lists, who cannot
afford enterprise KYC tools, ROONA is a LINE-native compliance tool that returns an auditable
screening result in under 5 seconds — unlike manual Googling or enterprise platforms, it is built
for their size of business.

**Breakdown:**

- **Target Customer:** Thai SME owners — gold shops, jewelry stores, auto dealers, money-transfer businesses, financial services
- **Need/Opportunity:** AMLO legal obligation to screen customers, with no affordable, fast tool
- **Category:** RegTech / AML screening
- **Key Benefit:** Auditable screening result in seconds, on LINE, no install
- **Differentiator:** LINE-native, SME-priced, audit-trail-as-the-product (timestamped PDF)

---

## Business Model

**Type:** B2B (SMB) SaaS

### Buying Roles

| Role         | Description       |
| ------------ | ----------------- |
| **Buyer**    | SME owner / proprietor — pays, often non-technical |
| **Champion** | The owner themselves, or a compliance officer at mid-size fintech/leasing (secondary) |
| **User**     | Shop staff performing the check at point of transaction |

---

## Ideal Customer Profile (ICP)

Thai SME owners who are not technical, use LINE daily, have no in-house compliance team, and need a
fast check before transacting plus a result they can show an auditor. Speed and auditability are the
jobs to be done — not analytics, not dashboards.

### Secondary Users

Compliance officers and tech teams at mid-size Thai fintechs and leasing companies who need an API
or dashboard integration.

---

## Success Criteria

- A shop owner completes a check faster than they could Google the name (target screening ~2.4s).
- Every check produces a PDF audit log (timestamp, sources, result) acceptable to an AMLO auditor.
- Onboarding without churn: add LINE OA → first successful check with no support ticket.
- (To quantify with Saga in Phase 2 — conversion, activation, retention targets.)

---

## Competitive Landscape

Three alternatives the customer weighs (from the landing-page comparison): doing it manually,
building in-house, or ROONA — across time, cost, ease, database coverage, and licensing.

### Our Unfair Advantage

LINE-native delivery (no install, native to how Thai SMEs already work), SME pricing, and a curated
multi-source database (1,145,396 names across 11 databases incl. Thai PEPs, AMLO, Freeze-05,
UN/OFAC/EU) refreshed every 24h, with audit trail as the core deliverable.

---

## Constraints

- Users on budget Android devices, small screens — target 360px minimum viewport.
- Thai-language primary; English only for technical/regulatory terms (AMLO, OFAC, PEPs).
- PDPA compliance is a go-live gate.
- WCAG 2.2 AA minimum; respect `prefers-reduced-motion`.
- Brownfield: an existing design system + codebase already exists (`Roona/`) and is authoritative for
  tokens, components, and accessibility gates.

---

## Platform & Device Strategy

**Primary Platform:** LINE (LIFF mini-app) on mobile; secondary merchant dashboard (web).

**Supported Devices:** Budget Android phones first, then iOS; desktop for the dashboard.

**Device Priority:** Mobile-first, LINE-native.

**Interaction Models:** Send ID photo (OCR) or manual entry → read result message → export PDF.

**Technical Requirements:**
- **Offline Functionality:** None required (LINE-online flow).
- **Native Features:** Camera/photo for ID capture via LIFF.

**Platform Rationale:** The primary interaction is on a phone via LINE; the landing page must feel
native to that context, not a desktop-first SaaS site shrunk down.

**Design Implications:** Mobile-first specs, 360px floor, Thai typography (IBM Plex Sans Thai + Sora).

**Development Implications:** React 18 + Vite + Tailwind LIFF app (`Roona/liff-codebase/`); the
screening backend is currently MOCKED (`merchant/api.ts`) and is the main Phase 5 build target.

---

## Tone of Voice

**For UI Microcopy & System Messages**

### Tone Attributes

1. **น่าเชื่อถือ (Trustworthy authority)**: a purpose-built compliance tool that takes the legal obligation seriously.
2. **รวดเร็ว (Fast)**: speed is the brand's main promise — prove it, don't make reading feel like work.
3. **เป็นทางการ (Formal, not cold)**: precise language and clean layout — warmth and directness, not corporate distance or a government form.

### Examples

**Error Messages:**
- Good: "ต้องระบุเลขบัตรประชาชน 13 หลัก — ลองตรวจอีกครั้ง"
- Avoid: "Error: Invalid input"

**Button Text:**
- Good: "ตรวจ AML"
- Avoid: "คลิกที่นี่เพื่อเริ่มการตรวจสอบ"

**Empty States:**
- Good: "ยังไม่มีประวัติการตรวจ — เริ่มตรวจรายแรกได้เลย"
- Avoid: "No data"

**Success Messages:**
- Good: "ผ่าน — ไม่พบรายชื่อในฐานข้อมูล AML/PEP/Sanctions (บันทึก PDF แล้ว)"
- Avoid: "Success"

### Guidelines

**Do:** name the databases, name the time, name the regulation (specificity earns trust); frontload the verb.
**Don't:** use vague reassurances ("secure", "fast") with no proof; crypto/web3 hype; emoji (hard rule — see integration guide).

---

## Anti-references (from PRODUCT.md — keep through every phase)

- **Crypto/web3 hype** — no neon-on-black, gradient text, "powered by blockchain", or dark theme for aesthetics.
- **Generic SaaS (Notion/Linear)** — this solves a legal obligation, not a workflow preference.
- **Legacy government/banking portals** — authority without heaviness; not dated or bureaucratic.

---

## Business Context

- **Primary Goal:** Convert AMLO-obligated Thai SMEs to a fast, auditable, affordable screening tool.
- **Solution:** LINE-native AML/PEP/Sanctions screening with timestamped PDF audit logs.
- **Target Users:** Non-technical Thai SME owners; secondary fintech/leasing compliance teams.

*Full strategic analysis (business goals, personas, driving forces) is developed in [Phase 2: Trigger Mapping](../B-Trigger-Map/).*

---

## Next Steps

- [ ] **Saga review** — deepen this seeded brief (quantify success criteria, sharpen positioning, confirm business model).
- [ ] **Phase 2: Trigger Mapping** — map ปปง./AMLO pressure to SME psychology; build personas; score features.
- [ ] **Phase 3: UX Scenarios** — outline the core journeys.
- [ ] **Phase 4: UX Design** — page specs (LIFF check flow + dashboard).
- [ ] **Phase 7: Design System** — reconcile with the existing Roona token/component engine (mode: existing).

---

_Seeded for Whiteport Design Studio from Roona/PRODUCT.md — review before relying on it._
