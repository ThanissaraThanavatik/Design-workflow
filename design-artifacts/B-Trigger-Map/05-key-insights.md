# Key Insights & Strategic Implications

> How the Trigger Map informs design and development decisions

**Document:** Trigger Map — Key Insights
**Created:** 2026-06-21
**Status:** DRAFT

---

## The Flywheel: Activated Shops Drive Everything

**THE ENGINE (Priority 1):** 500 activated screening shops. Every time Nattaya screens a customer, the
system produces an audit log and reinforces that the shop is compliant. This drives all other objectives.

**ROONA Adoption (Priority 2):** Driven by satisfied activated shops — trial→paid conversion, 100%
audit-readiness, and (via Ploy) the B2B API/dashboard segment.

**Ecosystem Benefits (Priority 3):** SMEs avoid AMLO fines, transactions get faster, and sector-wide AML
compliance rises.

---

## Primary Development Focus

1. **Activate Thawee** — make the first successful check happen the day he adds the LINE OA, with no support ticket.
2. **Make it effortless for Nattaya** — photo → OCR → ~2.4s → unambiguous status, so she screens every time.
3. **Make the proof visible** — the PDF audit log is the product; show it, don't just list it.
4. **Earn trust through specificity** — name the 11 databases, the 24h refresh, the 2.4s, the regulation.
5. **Defer B2B complexity** — keep API/RBAC out of the SME LINE flow; serve Ploy in the dashboard tier.

---

## Critical Success Factors

- **Speed at the counter** — ~2.4s or the customer waits and Nattaya skips the check.
- **Unambiguous result** — PASS/REVIEW/HIT via icon + text, never color alone (WCAG + Nattaya's fear).
- **Defensible audit trail** — timestamped PDF acceptable to an AMLO auditor (Thawee's and Ploy's core need).
- **Zero-IT onboarding** — LINE-native, no install (removes Thawee's biggest barrier).
- **Thai-first language** — English only for AMLO/OFAC/PEP terms.

---

## Design Implications

**Landing page (index) must:**
- Prove 2.4s and show a real result example
- Show the PDF audit log artifact, not just mention it
- Name the 11 databases + 24h refresh + PDPA
- State price + 14-day free trial with no hidden conditions

**LIFF check flow must:**
- Open in LINE with no install; capture ID by photo (OCR) with manual fallback
- Return PASS / REVIEW / HIT as icon + Thai text (not color-only), within ~2.4s
- Generate and surface the PDF audit log per check
- Work on a budget Android at 360px, respecting prefers-reduced-motion

**Result / status must:**
- For HIT/REVIEW: show matches with similarity score + reason (Ploy's explainability need)
- Log the operator name (Nattaya's "not blamed" need)

**Merchant dashboard must (Consider tier):**
- Show screening history retrievable for audit; export PDF
- Gate RBAC/API behind the B2B tier so the SME flow stays simple

---

## Emotional Transformation Goals (first person)

- Thawee: "ร้านผมทำถูกกฎหมายเต็มร้อย และง่ายกว่าที่คิด"
- Thawee: "ถ้า ปปง. มาตรวจ ผมมีหลักฐานพร้อมโชว์ทันที"
- Nattaya: "ฉันตรวจได้เองทุกครั้ง ไม่ต้องกลัวทำผิด"
- Ploy: "coverage ระดับนี้ผมเอาไปอธิบายผู้ตรวจสอบได้"

---

## Design Focus Statement

The ROONA experience transforms an AMLO-obligated SME owner from someone who avoids screening because it
is slow, confusing, and expensive — into someone who screens every customer in seconds and can prove it,
without an app, an IT team, or a compliance department.

**Primary Design Target:** Thawee the Thong-Shop Owner

**Must Address (critical for conversion):**
1. FEAR fine/license risk → defensible PDF audit trail + 11-DB/24h coverage
2. FEAR too complex / need IT → LINE-native, no install, OCR
3. FEAR data leak / PDPA → PDPA end-to-end, RBAC, secure retention
4. WANT fast at counter → ~2.4s result
5. WANT affordable → SME pricing + 14-day trial

**Should Address (supporting):**
1. Nattaya needs zero-training simplicity + clear status → photo flow + icon/text status
2. Nattaya needs Thai-first copy → Thai primary
3. Ploy needs explainability → similarity score + reason
4. Ploy needs uptime/portability → 99.9% + export

---

## Development Phases

**First Deliverable (MVP): the LINE screening loop** — Must-Have features from the Feature Impact Analysis:
2.4s screening, OCR capture, PASS/REVIEW/HIT status, PDF audit log, 11-DB coverage, PDPA, fuzzy match.

**Future Phases:**
- Phase 2: Merchant dashboard history + export
- Phase 3: B2B tier — API + RBAC
- Phase 4: Quota/usage analytics
- Phase 5: Evolution from real usability testing

---

## Related Documents

- **[00 Trigger Map](trigger-map.md)** · **[01 Business Goals](01-business-goals.md)** · **[02 Thawee](personas/02-thawee-the-thong-shop-owner.md)** · **[03 Nattaya](personas/03-nattaya-the-counter-staff.md)** · **[04 Ploy](personas/04-ploy-the-compliance-pro.md)** · **[Feature Impact](feature-impact-analysis.md)**

---

_Back to [Trigger Map](trigger-map.md)_
