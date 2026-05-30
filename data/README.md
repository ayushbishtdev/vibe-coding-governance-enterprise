# data/README.md — Governance Metrics Data Dictionary

This CSV contains benchmark figures, survey data, and empirical rates extracted from the vibe coding governance article cluster published at [agileleadershipdayindia.org](https://agileleadershipdayindia.org).

---

## Column definitions

| Column | Type | Description |
|--------|------|-------------|
| `metric` | string | Snake-case identifier for the metric. Unique per row. |
| `value` | number | The numeric value. Interpret using `unit`. |
| `unit` | string | Unit of measurement: `percent`, `days`, `months`, `engineers`, `x` (multiplier), `controls`, `clauses`, `gates`, `gaps` |
| `source` | string | The originating study, standard, or benchmark. Where a specific study is cited (e.g., 2026 Final Round AI CTO Council Survey), the value is directly attributed. Where noted as "industry benchmark range" or "enterprise programme benchmark", the value represents a widely reported range across multiple practitioner sources synthesised in the articles. |
| `context` | string | Explanatory note: what the number measures, how it was derived, and any caveats. |
| `applies_to` | string | The scope or population this metric applies to. |

---

## Key figures quick reference

| Metric | Value | Source |
|--------|-------|--------|
| CTO pilot failure rate (vibe coding → production disaster) | 89% | 2026 Final Round AI CTO Council Survey |
| Failures attributable to governance (not bad code) | 81% of failures | 2026 Final Round AI CTO Council Survey |
| Estimated enterprise feature work now vibe-coded | 40% | Andrej Karpathy 2025 / industry 2026 |
| Gross productivity uplift (governed teams) | 30–90% | Industry benchmark range |
| Initial PR creation spike | 3.2× | Vibe coding benchmark |
| Ungoverned rework rate | 47% | Empirical baseline |
| Audit finding reduction (5-gate implementation) | 73% | Governance framework benchmark |
| Sprint capacity for AI rework | 15–20% | Agile team benchmark |
| Tool licence break-even (governed) | 90 days | Governed team benchmark |
| Governance overhead as % of engineering budget | 3–7% | Enterprise programme benchmark |

---

## Data limitations

- **Survey data (2026 Final Round AI CTO Council):** This was a council-level survey of 18 CTOs. The sample size is small enough that individual outliers affect percentages significantly. Treat as directional, not statistically definitive.
- **Benchmark ranges:** Figures reported as ranges (e.g., "30–90% productivity uplift") reflect the spread across different team maturity levels and governance quality. They are not a single study's point estimate.
- **Temporal validity:** AI tooling, regulatory requirements (EU AI Act), and enterprise practices are evolving rapidly. These figures reflect the state as of May 2026. Check the [source articles](https://agileleadershipdayindia.org) for updated figures after the quarterly review.

---

## Using this data

These figures are suitable for:
- Internal business case presentations (cite the specific source column)
- Engineering budget models (governance overhead rows)
- Board-level KPI baseline setting
- Academic or industry research (with attribution to original sources)

They are **not** suitable for:
- Legal or regulatory filings (use primary regulatory text)
- Vendor contract negotiations (use vendor-supplied benchmarks)
- Auditor-facing evidence (use your own telemetry from production systems)

---

*Last updated: May 2026. Submit a PR with updated figures and source citations.*
