# Vibe Coding Governance — Quick Reference Cheatsheet

> Single-page reference for CTOs, CISOs, and AI Governance Officers. All data from the 2026 Final Round AI CTO Council survey and mapped frameworks.

---

## The 3-Layer Governance Stack

```
┌────────────────────────────────────────────────┐
│  POLICY LAYER     NIST AI RMF · ISO 42001 · EU AI Act │
│  (documents & decisions — build last)          │
├────────────────────────────────────────────────┤
│  EVIDENCE LAYER   provenance logs · decision logs      │
│  (what auditors actually inspect — build first)│
├────────────────────────────────────────────────┤
│  WORKFLOW LAYER   tools · templates · IDE configs      │
│  (the daily developer reality)                 │
└────────────────────────────────────────────────┘
```

---

## 7-Gate Governance Map

| Gate | What it enforces | Automated? |
|------|-----------------|------------|
| 1. Provenance Ledger | Tag every AI-authored line → session, prompt, model version | ✅ Yes |
| 2. Prompt Hygiene | Approved templates; blocked-pattern registry; no PII in context | ✅ Yes |
| 3. AI Code Review | Two-gate: automated LLM SAST + named human reviewer | Partial |
| 4. Dependency Verification | AI-aware SBOM diff + typosquat scanner on every PR | ✅ Yes |
| 5. Article 15 Evidence Pack | Auto-compile cybersecurity, accuracy & robustness dossier | ✅ Yes |
| 6. Vibe Coding Definition of Done | 9 AI-specific acceptance gates before sprint close | Partial |
| 7. Quarterly Governance Review | Board-level KPI pack: rework rate, audit findings, debt ledger | ❌ Manual |

**Result: implementing Gates 1–5 cuts audit findings by 73%.**

---

## 5 Failure Archetypes (Pattern-Match These)

1. **Provenance gap** — Team can't establish whether offending lines came from a human or AI. Auditor records inability to determine authorship as a finding.
2. **Hallucinated dependency** — Model invents a plausible package name. Typosquatter has been waiting on npm/PyPI. Scales linearly with vibe coding adoption.
3. **Prompt injection in a comment** — Third-party library contains a crafted comment. Model writes attacker's code into the diff. Reviewer rubber-stamps it.
4. **Compliance drift** — Definition of Done was updated 6 months ago; operational practice has drifted. Auditor finds a delta between practice and documented control.
5. **Shadow vibe coder** — Developer uses personal Copilot on a personal laptop, pastes into the repo. Organisation loses provenance, telemetry, and contractual cover.

---

## RACI (Who Owns What)

| Area | CTO | CISO | AI Governance Officer |
|------|-----|------|----------------------|
| Tooling deployment & velocity metrics | **A** | C | I |
| Control design & threat model | I | **A** | C |
| Evidence chain & regulatory posture | I | C | **A** |
| Budget for governance tooling | **A** | C | I |
| Quarterly board reporting | C | C | **A** |

*A = Accountable · C = Consulted · I = Informed*

> If your organisation lacks an AI Governance Officer, designate the Chief Compliance Officer explicitly via board minutes. Auditors accept role-by-charter; they reject role-by-ambiguity.

---

## 7 KPIs for Every Board Pack

| Metric | Target | Alert |
|--------|--------|-------|
| Suggestion acceptance rate | 50–75% | <20% or >85% |
| AI-attributable defect rate | Declining QoQ | Any upward trend |
| Hallucinated dependency catch rate | 100% | Any miss |
| Review gate enforcement rate | >98% | <95% |
| Provenance coverage | >95% | <90% |
| Audit finding aging | 0 open >90 days | >30-day backlog |
| Technical debt accrual | Stable or declining | 3 sprints of increase |

---

## 4-Line CFO ROI Model

```
Line 1  Gross uplift       = Engineering capacity × 30–90% productivity gain
Line 2  Rework tax         = Gross uplift × 47%  [ungoverned baseline]
Line 3  Governance overhead = 3–7% of total engineering budget
Line 4  Net delivered value = Line 1 − Line 2 − Line 3
```

- Break-even on tool licences: **first 90 days** (governed teams)
- Sprint capacity for AI rework: **15–20% per sprint** (non-negotiable)

---

## 5-Stage Maturity Model

| Stage | Engineers | Critical action |
|-------|-----------|----------------|
| 1 — Pilot | 1–10 | Standardise tooling; start manual logging |
| 2 — Departmental | 10–50 | Automate basic provenance |
| 3 — Enterprise Rollout | 100–500 | **Fund dedicated governance headcount (CTO underestimates this 3×)** |
| 4 — Federated | 500–1,000 | Continuous automated evidence; ISO 42001 certification |
| 5 — Embedded | 1,000+ | Governance as infrastructure; regulator-facing posture |

---

## NIST AI RMF Crosswalk

| NIST Function | Vibe Coding Application | Gate |
|---------------|------------------------|------|
| GOVERN | Tooling policy, acceptable use policy | Gate 2 (Prompt Hygiene) |
| MAP | Classify which code is permitted to be vibe coded | Pre-sprint (DoR) |
| MEASURE | Telemetry: acceptance rate, defect attribution, rework rate | Gate 7 (Quarterly Review) |
| MANAGE | Pull request gate that fires on every PR and release | Gates 1–5 |

> Most teams treat vibe coding as a MEASURE-MAP problem. It is fundamentally a MANAGE problem. Build the enforcement gate first.

---

## ISO/IEC 42001 Annex A Controls (11 Applicable)

| Control | Description | Which gate |
|---------|-------------|------------|
| A.2.2 | AI policy | Gate 2 |
| A.6.2.2 | AI system requirements | Gate 3 |
| A.9.3 | AI system monitoring | Gate 7 |
| A.10.2 | Third-party AI components | Gate 4 |
| + 7 others | See full crosswalk in source article | Various |

---

## EU AI Act Quick Reference

| Article | Obligation | Vibe coding implication |
|---------|-----------|------------------------|
| Art. 12 | Record-keeping | Retain provenance logs for operational life + defined period (typically 10 years) |
| Art. 15 | Cybersecurity, accuracy, robustness | Prompt injection protection, supply-chain integrity, immutable evidence |
| Art. 26 | Deployer duties | If you use Copilot/Cursor in regulated workflows, you are an Art. 26 deployer |

> Procurement contracts written before August 2026 frequently do not reflect Art. 26 deployer status. Reissue them.

---

## Cursor vs. Copilot at a Glance

| Dimension | Copilot Enterprise | Cursor |
|-----------|-------------------|--------|
| Native audit logging | Strong (built-in) | Requires configuration |
| EU Art. 26 indemnification | Yes | Requires enterprise config |
| Data retention model | Zero-retention tenant available | Configurable; default varies |
| Best for | Compliance-first orgs | Velocity-first orgs needing heavy internal config |
| Governance overhead | Lower | Higher |

---

*Source: [agileleadershipdayindia.org](https://agileleadershipdayindia.org) — Vibe Coding Governance pillar (May 2026). Open an issue for corrections.*
