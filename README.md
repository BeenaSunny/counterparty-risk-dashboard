# Counterparty Risk Dashboard

A Power BI dashboard for monitoring counterparty (third-party vendor) risk across the lifecycle — onboarding, ongoing assessment, risk flags, and watch-list review. Built end-to-end as a portfolio piece demonstrating risk analytics, DAX modeling, and executive reporting.

## Why this dashboard

Vendor risk management (VRM / TPRM) is one of the fastest-growing areas in GRC — driven by NYDFS 500.11, OCC third-party risk guidance, and DORA in the EU. The same skill set — data modeling, DAX, control mapping, executive storytelling — is what financial-services GRC teams pay $85-110/hr for.

This dashboard was built to demonstrate that workflow end-to-end without requiring access to a real bank's vendor inventory. The data is synthetic. The structure, measures, and reporting cadence mirror what a real TPRM program produces.

## What's in the report

Three pages, each targeting a different audience:

| Page                  | Audience           | What they get                                                     |
|-----------------------|--------------------|-------------------------------------------------------------------|
| **Executive Overview** | CISO, CRO, board   | Portfolio-level KPIs: total vendors, % high-risk, contract value at risk, top 3 risk drivers |
| **Risk Heatmap**       | Risk analysts      | Inherent vs. residual risk matrix, by vendor and by risk category  |
| **Risk Flags & Watch List** | Vendor managers | Vendors with open risk flags, by severity, with days-to-resolution and remediation owner |

## What this demonstrates

| Skill                                      | Where it lives in this dashboard                               |
|--------------------------------------------|-----------------------------------------------------------------|
| **Star-schema data modeling**              | Fact tables for risk events, dimensions for vendor / category / control |
| **DAX measures** (composite risk scoring)  | Risk score = weighted(Inherent Risk × Residual Risk × Exposure)  |
| **Time intelligence**                      | Trending, period-over-period, MTD/QTD/YTD                        |
| **Control mapping** (NIST CSF, ISO 27001)  | Control coverage % by domain                                     |
| **Executive storytelling**                 | Single-glance KPIs + drillthrough to source data                 |
| **Power BI native features**               | Bookmarks, drill-through, conditional formatting, what-if       |
| **DAX pattern fluency**                    | CALCULATE, FILTER, ALL, DIVIDE, RANKX, USERELATIONSHIP           |

## Stack

- **Power BI Desktop** (Microsoft, free)
- **DAX** for measures (no custom visuals — stock visuals throughout)
- **Power Query** for ETL (M language)
- Data source: synthetic CSV (provided for reference / reproducibility)

## How to open

1. Download `Counterparty_Dashboard.pbix` (156 KB)
2. Open with Power BI Desktop (latest version, August 2026 release or later)
3. The dashboard opens against its embedded sample data — no external connections required
4. To rebuild the data model from scratch, see `data/` for the synthetic CSV files

## Architecture (data flow)

```
Synthetic CSVs  →  Power Query (ETL)  →  Star schema
   ↓
   vendors (dim)        ←  fact_risk_events  →  fact_assessments
   categories (dim)     ←                    →  controls (dim)
   sites (dim)          ←                    →  calendar (dim)

Star schema  →  DAX measures  →  Report pages
```

## Related

- **SIEM data lake** (sibling repo) — same Power BI + Azure stack applied to security detection data
- **Counterparty Risk Dashboard** (this repo) — same stack applied to TPRM

## License

MIT — see `LICENSE`.