# vibe-coding-governance-enterprise

Governance gates, security checklists, KPI stacks, and audit-ready templates for engineering teams running AI coding assistants (Cursor, Copilot) at enterprise scale. Built from real CTO case studies and mapped to NIST AI RMF, ISO/IEC 42001, and EU AI Act Article 15.

**Last updated: May 2026** | **Audience: Engineering leaders, CISOs, AI Governance Officers**

---

## What's in this repo

| File | What it gives you |
|------|-------------------|
| [CHEATSHEET.md](./CHEATSHEET.md) | One-page reference: 7-gate governance map, 5-failure archetypes, RACI, KPI stack |
| [checklist-ai-code-review.md](./checklist-ai-code-review.md) | 12-step pull request checklist for AI-generated code, grouped by phase |
| [data/governance-metrics.csv](./data/governance-metrics.csv) | Benchmark numbers from the 2026 Final Round AI CTO Council survey and industry data |
| [data/README.md](./data/README.md) | Column definitions and source notes for the CSV |
| [README.md](./README.md) | This file — full breakdown of every governance layer |

---

## 1. Why vibe coding governance exists

Vibe coding — where developers prompt Cursor, Copilot, Cline, or Windsurf and accept suggestions in flow — now accounts for an estimated **40% of enterprise feature work**. Andrej Karpathy popularised the term in early 2025.

The 2026 Final Round AI CTO Council survey found that **16 out of 18 CTOs (89%) reported a production disaster traceable to vibe coding workflows**. Of those 16 failures, only 3 were caused by genuinely insecure AI code. The other 13 failed for governance reasons: missing provenance, hallucinated dependencies, shadow tooling, or the absence of a defensible evidence chain.

Modern regulators treat a missing evidence chain exactly the same as a missing security control.

**Three layers every real governance program needs:**

1. **Workflow layer** — approved tools, prompt templates, IDE configs, model versions, data classification rules
2. **Evidence layer** — immutable trail of who prompted what, which model responded, which lines were accepted, which reviewer signed off *(build this first — auditors inspect this layer)*
3. **Policy layer** — documents mapping workflow and evidence to NIST AI RMF, ISO/IEC 42001, EU AI Act, SOC 2

> **Pro tip:** Most teams build the policy layer first because it produces a PDF. Build the evidence layer first. A perfect policy with no telemetry is theatre; minimal telemetry with a stub policy is a defensible starting position.

**Full breakdown:** [Vibe Coding Governance and Enterprise Risk Management — The Complete 7-Gate Playbook](https://agileleadershipdayindia.org/blogs/vibe-coding-governance-enterprise-risk-management/vibe-coding-governance-enterprise-risk-management.html)

---

## 2. The 5 failure archetypes

Pattern-match your organisation against these before your CISO does:

| Archetype | What happens | Scale factor |
|-----------|-------------|--------------|
| **Provenance gap** | Incident occurs; team can't establish whether offending lines came from a human, Cursor, or Copilot. Auditor records inability to determine authorship as a finding. | High |
| **Hallucinated dependency** | Model invents a plausible package name. Developer doesn't check. A typosquatter has been waiting. | Scales linearly with vibe coding adoption |
| **Prompt injection in a comment** | Third-party library file contains a crafted comment. Model writes attacker's code into the diff. Reviewer rubber-stamps it. | High in open-source-heavy repos |
| **Compliance drift** | Team's Definition of Done was updated for AI code 6 months ago, but operational practice has drifted. Auditor finds a delta between practice and documented control. | Universal at Stage 3+ scale |
| **Shadow vibe coder** | Developer uses a personal Copilot subscription on a personal laptop, pastes output into the repo. Org loses provenance, telemetry, and contractual cover. | Very high — nearly universal without tooling enforcement |

> **PMO warning:** If your CTO presents a vibe coding ROI deck without an accompanying governance maturity score, the board will discount the productivity number by 30–60%. Lead with the governance posture, not the velocity gain.

**Full breakdown:** [5 Failure Archetypes Every CTO Must Pattern-Match Against](https://agileleadershipdayindia.org/blogs/vibe-coding-governance-enterprise-risk-management/vibe-coding-governance-enterprise-risk-management.html)

---

## 3. The 7-gate governance map

These 7 gates are the operational backbone. Each replaces a specific governance gap:

| Gate | Replaces | Done looks like |
|------|----------|----------------|
| **1. Provenance Ledger** | Untracked Cursor & Copilot edits | Every AI-authored line tagged to a session, prompt, and model version |
| **2. Prompt Hygiene Policy** | Ad-hoc prompting culture | Approved prompt templates and a blocked-pattern registry |
| **3. AI Code Review Gate** | Single human reviewer rubber-stamp | Two-gate review: automated SAST + named human accountable |
| **4. Dependency Verification** | Trusting hallucinated package names | SBOM diff on every PR plus typosquat scanner |
| **5. Article 15 Evidence Pack** | Ad-hoc audit response | Pre-built cybersecurity, accuracy & robustness dossier |
| **6. Vibe Coding Definition of Done** | Standard Scrum DoD | Sprint cannot close without 9 AI-specific acceptance gates met |
| **7. Quarterly Governance Review** | Annual policy refresh | Board-level KPI pack with rework rate, audit findings, debt ledger |

Implementing all 5 mandatory CI/CD gates (Gates 1–4 plus 5) demonstrably **cuts compliance and security audit findings by 73%**. Gates 1, 2, 4, and 5 are entirely automated — they do not slow sprint delivery.

**Full breakdown:** [Vibe Coding Governance Framework: 5 Gates That Cut Risk 73%](https://agileleadershipdayindia.org/blogs/vibe-coding-governance-framework-cto/vibe-coding-governance-framework-cto.html)

---

## 4. The 7 OWASP LLM gaps standard policies miss

The NIST AI RMF maps broad generative AI risks but fails to address granular, workflow-specific vulnerabilities inside the developer IDE. Here are the 7 gaps your AI security policy is likely missing:

| # | Gap | Mechanism | Compliance trigger |
|---|-----|-----------|-------------------|
| 1 | **IDE Prompt Injection** | Attacker embeds malicious instructions in open-source library comments; model writes attacker-controlled code into the diff | EU AI Act Art. 15(5) |
| 2 | **Hallucinated Dependency Attack** | LLM suggests non-existent packages; typosquatters register them on npm/PyPI | SOC 2 supply chain |
| 3 | **LLM Data Exfiltration** | Developer feeds API keys/proprietary code into a non-enterprise-ringfenced tenant | GDPR, IP law |
| 4 | **Insecure Output Handling** | AI code compiles perfectly but contains flawed logic that bypasses standard SAST | SOC 2 processing integrity |
| 5 | **Developer Overreliance** | Complex AI algorithm accepted without comprehension; future maintainers can't audit or secure it | Technical debt + incident risk |
| 6 | **Model Denial of Service** | Excessive context window usage triggers rate-limiting; developer productivity halts | Business continuity |
| 7 | **Training Data Poisoning** | Developer highlights malicious external code for AI explanation; data bleeds into model suggestions | Systemic risk |

> EU AI Act Article 15 cybersecurity obligations mandate that high-risk AI systems be resilient against exploitation. Prompt injections and hallucinated dependencies are direct violations of these robustness requirements.

**Full breakdown:** [Vibe Coding Security Risks: 7 OWASP Gaps NIST Skipped](https://agileleadershipdayindia.org/blogs/vibe-coding-enterprise-security-risks/vibe-coding-enterprise-security-risks.html)

---

## 5. The 12-step AI code review checklist (summary)

The full checklist is in [`checklist-ai-code-review.md`](./checklist-ai-code-review.md). Here is the phase structure:

**Phase 1 — Provenance & Authorship Validation** (Steps 1–3): Verify AI provenance tags, check data exfiltration boundaries, validate approved tooling.

**Phase 2 — Vulnerability & Hallucination Scanning** (Steps 4–7): Prompt injection SAST, dependency existence verification, hallucinated API scan, insecure output handling check.

**Phase 3 — Architectural & Logic Validation** (Steps 8–10): Overreliance test, minimum test coverage enforcement, technical debt assessment.

**Phase 4 — Compliance & Evidence Archival** (Steps 11–12): Log the review decision with named reviewer, archive evidence chain to immutable compliance vault.

Automate Phases 1, 2, and 4 in CI/CD. The human reviewer focuses only on Phase 3 (Logic Validation) and the Phase 4 decision sign-off. This hybrid approach maintains developer speed while guaranteeing a mathematically provable compliance posture.

**Full breakdown:** [Your AI Generated Code Review Checklist Fails Audit](https://agileleadershipdayindia.org/blogs/ai-generated-code-review-checklist/ai-generated-code-review-checklist.html)

---

## 6. The AI code security policy: 11 required clauses

An enterprise AI code policy is not an Acceptable Use Policy. An AUP tells employees not to paste customer data into ChatGPT. An AI code security policy dictates exact CI/CD pipeline blocks for GitHub Copilot or Cursor.

Big 4 auditors look for these 11 clauses:

1. **Provenance and Authorship Definitions** — LLM-generated code blocks tagged with model version and original developer prompt
2. **Approved Tooling and Shadow IT Prohibitions** — exact inventory of enterprise-ringfenced tools; explicit ban on personal consumer subscriptions on corporate endpoints
3. **Restricted Domains and Data Classification** — which repositories are off-limits to AI assistance (e.g., core cryptographic modules); what level of proprietary data can enter the context window
4. **Mandatory Review and Automated Enforcement** — two-gate process: automated LLM-specific SAST then named human reviewer
5. **Threat Model — Prompt Injection** — explicit controls for indirect injection via third-party code
6. **Exception Handling** — who can authorise a gate bypass and what compensating control applies
7. **Vendor Management** — contractual basis for each AI tool, data retention policy, and indemnification scope
8. **Incident Response** — procedures for AI-attributable production incidents, including root-cause chain reconstruction
9. **Training and Awareness** — mandatory developer training on AI code vulnerabilities
10. **Regulatory Mapping** — explicit NIST AI RMF and ISO/IEC 42001 crosswalk in an appendix
11. **Review Cadence** — formal quarterly update by CTO and CISO, documented in board minutes

This template maps directly to the **NIST AI RMF MANAGE function** and **ISO/IEC 42001 Annex A controls A.2.2, A.6.2.2, and A.10.2**. Without a documented framework, passing a SOC 2 Type II audit involving AI-generated code is not achievable.

**Full breakdown:** [AI Code Security Policy Template Big 4 Auditors Accept](https://agileleadershipdayindia.org/blogs/ai-code-security-policy-template-enterprise/ai-code-security-policy-template-enterprise.html)

---

## 7. Context engineering vs. vibe coding: the 7-gate hybrid model

Andrej Karpathy declared vibe coding deprecated in 2026 because unstructured prompting fails under enterprise scale and security scrutiny. The pivot stems from the fundamental lack of reproducibility: if a critical bug emerges, the post-mortem stalls because the team cannot recreate the exact ad-hoc prompt that generated the vulnerable code.

**The difference:**

| Dimension | Vibe Coding | Context Engineering |
|-----------|-------------|---------------------|
| Context assembly | Developer's immediate working memory | Programmatic pipeline feeding verified state data and architectural constraints |
| Reproducibility | Impossible to recreate exact prompt | Full inputs logged by default |
| Audit readiness | Evidence must be retrofitted | Evidence generated automatically |
| Hallucination rate | High (ad-hoc context) | Lower (validated constraints fed to model) |
| Best fit | Low-risk internal tooling, isolated feature branches | Core architecture, cryptographic modules, anything touching PII |

The industry is not eliminating vibe coding — it is running a **7-gate hybrid model**: vibe coding restricted to low-risk tasks; context engineering mandated for regulated or customer-facing code.

**Full breakdown:** [Context Engineering vs Vibe Coding: Why Karpathy Quit](https://agileleadershipdayindia.org/blogs/context-engineering-vs-vibe-coding-production/context-engineering-vs-vibe-coding-production.html)

---

## 8. The ROI math: 4-line CFO model

The gross productivity spike from vibe coding is real — often 3.2× in initial pull request creation. The CFO problem is that this is a vanity metric. It measures the speed of creation, not the speed of deployment.

**The 4-line model CFOs sign off on:**

```
Line 1: Gross Engineering Uplift   = Engineering capacity × 30–90% productivity gain
Line 2: Ungoverned Rework Tax      = Gross uplift × 47% (empirical rework rate without governance)
Line 3: Governance Overhead        = 3–7% of total engineering budget
Line 4: Net Delivered Value        = Line 1 − Line 2 − Line 3
```

Without governance, a 47% rework rate obliterates the financial advantage. With governed pipelines, teams typically achieve **tool licence break-even within the first 90 days** of deployment. Governance overhead (3–7% of engineering budget) pays for itself by protecting the productivity gain — not by creating new value on top of a fragile foundation.

**Full breakdown:** [Vibe Coding ROI vs Traditional Development: The 3.2× Math](https://agileleadershipdayindia.org/blogs/vibe-coding-roi-vs-traditional-development/vibe-coding-roi-vs-traditional-development.html)

---

## 9. Technical debt: the 4-tier ledger

Ungoverned vibe coding inflates Q4 rework budgets by 47%. AI-generated technical debt is fundamentally different from human technical debt: it is almost entirely accidental, accumulates faster because LLMs optimise for immediate syntactic correctness over long-term maintainability, and has a shorter half-life before a mandatory refactor.

**CFO-approved 4-tier ledger structure:**

| Tier | Debt type | Tracking field in Jira/Linear |
|------|-----------|-------------------------------|
| T1 | Hallucinated/deprecated dependency | `ai-debt-dependency` |
| T2 | Architectural bloat / over-complex boilerplate | `ai-debt-architecture` |
| T3 | Logic flaws requiring human rearchitecture | `ai-debt-logic` |
| T4 | Compliance/audit remediations from AI gaps | `ai-debt-compliance` |

**Sprint capacity rule:** Mature agile teams must dedicate **15–20% of each sprint** exclusively to refactoring AI output. If you ignore this allocation, compounding debt will eventually paralyse feature delivery.

**Full breakdown:** [Vibe Coding Technical Debt Management: Cut Rework 47%](https://agileleadershipdayindia.org/blogs/vibe-coding-technical-debt-management/vibe-coding-technical-debt-management.html)

---

## 10. Scaling beyond 100 engineers: the 5-stage maturity model

Governance becomes exponentially harder between 50 and 200 engineers — where informal coordination breaks but enterprise GRC tooling is not yet justified. CTOs routinely underestimate Stage 3 effort by **a factor of three**.

| Stage | Engineers | Governance mode | Evidence collection | Milestone |
|-------|-----------|----------------|---------------------|-----------|
| 1 — Pilot | 1–10 | Named individuals | Manual | Tooling standardised |
| 2 — Departmental | 10–50 | Small governance team | Basic logging | Basic logging active |
| 3 — Enterprise Rollout | 100–500 | Full-time governance function | **Tooling investment required** | GRC tool integration |
| 4 — Federated | 500–1,000 | Central team + embedded liaisons | Automated, continuous | ISO/IEC 42001 certification |
| 5 — Embedded | 1,000+ | Governance as infrastructure | Continuous certification posture | Regulator-facing posture |

**GCC India note:** GCC operations often progress through early AI maturity stages faster than their parent companies due to aggressive tooling adoption. Audit GCC posture explicitly — not by inheritance.

**Full breakdown:** [Scaling Vibe Coding: Why Enterprise IT Governance Breaks](https://agileleadershipdayindia.org/blogs/scaling-vibe-coding-enterprise-it-governance/scaling-vibe-coding-enterprise-it-governance.html)

---

## 11. Scrum Definition of Done: 9 acceptance gates

The standard Scrum Guide was written for human developers. A vibe coding Definition of Done requires 9 distinct gates. A story is not "Done" until all 9 pass:

**Authorship & Provenance (Gates 1–3)**
- AI provenance logged and tagged in the repository
- Prompt history retained in ticket or immutable compliance vault
- Specific LLM and IDE version documented

**AI-Specific Security Validation (Gates 4–6)**
- Prompt injection scan passed (specialised LLM SAST)
- Hallucinated dependency check cleared (AI-aware SBOM diff)
- Two-gate code review completed (automated validator + human)

**Legal & Compliance Clearance (Gates 7–9)**
- Data exfiltration check confirmed (no PII/keys in context window)
- EU AI Act Article 26 alignment sign-off (for high-risk systems)
- Technical debt ledger updated (complex AI boilerplate logged)

**Who enforces this:** The Scrum Master blocks the Jira "Done" transition until CI confirms the provenance log and SBOM diff. For SAFe organisations, align these 9 gates at the ART level during PI Planning.

**Full breakdown:** [Vibe Coding Definition of Done: What Scrum Guides Hide From PMs](https://agileleadershipdayindia.org/blogs/vibe-coding-definition-of-done-scrum/vibe-coding-definition-of-done-scrum.html)

---

## 12. The KPI stack (7 board-ready metrics)

A framework that cannot be measured cannot be defended. These 7 metrics belong in every quarterly board pack:

| Metric | What it measures | Alert threshold |
|--------|-----------------|----------------|
| **Suggestion acceptance rate** | % of AI suggestions accepted; anomalies indicate dysfunction | >85% or <20% (both are red flags) |
| **AI-attributable defect rate** | Defects in production traced to AI-generated code paths | Any increase quarter-over-quarter |
| **Hallucinated dependency catch rate** | % of invented package names caught by SBOM diff | Target: 100% |
| **Review gate enforcement rate** | % of merges completing two-gate review without exception | Target: >98% |
| **Provenance coverage** | % of repository lines with attributable authorship | Target: >95% |
| **Audit finding aging** | Open vibe coding audit findings broken down by age | 0 findings >90 days old |
| **Technical debt accrual** | Debt introduced by vibe coding workflows per sprint | Stable or declining trend |

---

## Quick reference assets

- **[CHEATSHEET.md](./CHEATSHEET.md)** — Single-page reference covering the 7-gate map, failure archetypes, RACI, KPI definitions, and NIST/ISO crosswalk. Print-ready.
- **[checklist-ai-code-review.md](./checklist-ai-code-review.md)** — The complete 12-step pull request checklist with implementation notes for each step. Copy into your team wiki.
- **[data/governance-metrics.csv](./data/governance-metrics.csv)** — Benchmark data extracted from industry surveys. Use to calibrate your own KPI baselines.

---

## Sources & deeper reading

- [Vibe Coding Governance and Enterprise Risk Management](https://agileleadershipdayindia.org/blogs/vibe-coding-governance-enterprise-risk-management/vibe-coding-governance-enterprise-risk-management.html) — Master 7-gate playbook
- [Vibe Coding Governance Framework for CTOs](https://agileleadershipdayindia.org/blogs/vibe-coding-governance-framework-cto/vibe-coding-governance-framework-cto.html) — 5 gates, 73% risk reduction
- [Vibe Coding Enterprise Security Risks](https://agileleadershipdayindia.org/blogs/vibe-coding-enterprise-security-risks/vibe-coding-enterprise-security-risks.html) — 7 OWASP LLM gaps
- [AI Generated Code Review Checklist](https://agileleadershipdayindia.org/blogs/ai-generated-code-review-checklist/ai-generated-code-review-checklist.html) — 12-step audit-ready checklist
- [AI Code Security Policy Template Enterprise](https://agileleadershipdayindia.org/blogs/ai-code-security-policy-template-enterprise/ai-code-security-policy-template-enterprise.html) — 11-clause Big 4 template
- [Context Engineering vs Vibe Coding Production](https://agileleadershipdayindia.org/blogs/context-engineering-vs-vibe-coding-production/context-engineering-vs-vibe-coding-production.html) — Karpathy pivot analysis
- [Vibe Coding ROI vs Traditional Development](https://agileleadershipdayindia.org/blogs/vibe-coding-roi-vs-traditional-development/vibe-coding-roi-vs-traditional-development.html) — 4-line CFO model
- [Vibe Coding Technical Debt Management](https://agileleadershipdayindia.org/blogs/vibe-coding-technical-debt-management/vibe-coding-technical-debt-management.html) — 4-tier debt ledger
- [Vibe Coding Definition of Done Scrum](https://agileleadershipdayindia.org/blogs/vibe-coding-definition-of-done-scrum/vibe-coding-definition-of-done-scrum.html) — 9 acceptance gates
- [Scaling Vibe Coding Enterprise IT Governance](https://agileleadershipdayindia.org/blogs/scaling-vibe-coding-enterprise-it-governance/scaling-vibe-coding-enterprise-it-governance.html) — 5-stage maturity model
- [Cursor Copilot Code Quality Audit](https://agileleadershipdayindia.org/blogs/cursor-copilot-code-quality-audit/cursor-copilot-code-quality-audit.html) — 6-gate IDE audit

---

## Contributing / corrections

Numbers change. If you spot an outdated statistic, a broken link, or a framework version that has been superseded, please open an issue or submit a PR. This repo is maintained on a **quarterly cadence** (next update: August 2026).

Contributions welcome for: updated benchmark data, additional framework crosswalks (e.g., DORA, SABSA), and tool-specific implementation notes for Cursor, Copilot, Cline, or Windsurf.

---

## About the author

I’m Ayush Bisht, a Content Engineer and AI tools specialist passionate about building smart, scalable, and engaging digital experiences. Currently working with AgileWow, I blend content strategy with AI-driven workflows to create efficient, impactful solutions.

[LinkedIn](https://www.linkedin.com/in/ayush-bisht-92abb1315/).
