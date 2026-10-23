# Exercise 8 - Web-augmented intelligence: build a live dashboard

**Duration:** ~25 min | **Level:** Advanced

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

Joule can reach beyond your SAP landscape. In this exercise you ask it to pull industry benchmark data from the web and combine it with live SAP data to build an intelligence dashboard, the kind of view that would normally take a team hours to assemble.

A working example of the dashboard this exercise produces is in `Joule_Dashboard_Exercise8_Example.html` (shared by your instructor). Use it as a reference for what the final output can look like.

## Exercise 8.1 - Get industry benchmarks from the web

Ask Joule to search for current procurement benchmarks:

```
What are the current 2026 benchmarks for procurement savings rate and PO accuracy for manufacturing companies?
```

Joule draws on established procurement research (JAGGAER, APQC, McKinsey, Varisource) and returns tiered benchmark tables. For manufacturing companies:

**Procurement Savings Rate (% of addressable spend):**
| Performance Level | Savings Rate |
|---|---|
| Under-performing | < 3% |
| Average / Developing | 3–5% |
| Strong / Mature | 5–10% |
| Top Quartile / World-Class | 10–15%+ |
| Transformation / AI-Enabled | Up to 15–20% on select categories |

**Purchase Order (PO) Accuracy:**
| Performance Level | PO Accuracy Rate |
|---|---|
| Below benchmark | < 90% |
| Median (APQC) | ~90% |
| Strong / Top Quartile | 95%+ |
| Best-in-Class (highly automated) | 99%+ |

Key takeaways: aim for 5–8% savings rate as a solid baseline, 95%+ PO accuracy for high performers. Pair savings rate with spend under management (target: 60%+), contract compliance (≥75%), and maverick spend (<5%) for a complete picture.

![Joule response showing 2026 procurement benchmarks for manufacturing: Procurement Savings Rate and PO Accuracy tables](images/08_01_0010.png)

## Exercise 8.2 - Compare to your own SAP data

Now layer in your live data:

```
Now compare our company's procurement activity from S/4HANA to those benchmarks.
```

Joule queries S/4HANA and returns live figures for three KPIs:

**1. PO Accuracy — 98.0%** (above top-quartile benchmark of 95%+): Joule counts 551,635 total PO line items, with only 4,653 anomalous items, giving a 98.0% clean-PO rate. This puts the company in the top quartile for automated PO processing.

**2. Contract-Backed Ordering — 0.8%** (well below the ≥75% benchmark): Only 4,653 of 551,635 PO items carry a direct framework contract reference in S/4HANA. Joule flags an important caveat: this reflects only contracts managed natively in S/4HANA. If strategic sourcing and contract management are handled in SAP Ariba, actual spend under management would be significantly higher.

**3. Procurement Savings Rate — Not measurable**: Price variance analytics in S/4HANA are not yet generating measurable data. Joule uses the very low contract-backed ordering rate as an indirect signal that savings rates are likely below the 5–10% benchmark.

The summary table Joule produces:

| KPI | Your Status | Vs. Benchmark |
|---|---|---|
| PO Accuracy | 98.0% | Top quartile |
| Contract-Backed Ordering (S/4HANA) | 0.8% | Well below benchmark |
| Procurement Savings Rate | Not measurable | Likely below average |

Joule recommends three next steps: validate contract data completeness in Ariba, activate price variance tracking in S/4HANA, and leverage the strong PO accuracy to push more volume through contracts.

![Joule response showing procurement KPI comparison: PO Accuracy 98.0% (top quartile), Contract-Backed Ordering 0.8% (well below benchmark), Savings Rate not measurable, with recommended next steps](images/08_02_0010.png)

## Exercise 8.3 - Add HR context

Bring in SuccessFactors data and a market salary range:

```
Add our Engineering Manager headcount from SuccessFactors and the industry benchmark salary range for Engineering Managers ($145K-$245K base, median ~$156K).
```

Joule queries SuccessFactors and returns **19 Engineering Managers globally**, spread across 5 pay grades (GR-07 to GR-13, with GR-10 being the largest cohort at 8) and 16 countries (US, DE, UK, FR, NL, AU, SG, IE, SE, AT, PT, ZA, RU, IN, BR, ID).

For the 3 US-based managers (the only ones directly comparable to the $145K–$245K US benchmark), Joule calculates:

| Employee | Annual Base | vs. Median | Status |
|---|---|---|---|
| 802983 | $151,834 | −$4,166 | Within range |
| GHAMILTON | $139,992 | −$16,008 | Below floor |
| MHOLDING | $139,992 | −$16,008 | Below floor |
| **US Average** | **$143,939** | **−$12,061** | **Below floor** |

Key finding: two of the three US Engineering Managers are $16K below the $145K benchmark floor, which may present retention risk. The 16 international managers are paid in local currencies (EUR, GBP, AUD, SGD, SEK, and others) so the US benchmark does not directly apply to them.

![Joule response showing 19 Engineering Managers from SuccessFactors with pay grade distribution and US salary comparison against the $145K–$245K benchmark](images/08_03_0010.png)

## Exercise 8.4 - Generate the HTML dashboard

Ask Joule to pull everything together into a visual file:

```
Create an HTML dashboard file showing: (1) my procurement KPIs vs industry benchmarks, (2) my team headcount, and (3) market salary context. Make it look professional.
```

Joule generates a self-contained `.html` file named `procurement_hr_dashboard.html`. Open it directly in any browser, no server required.

The dashboard has three sections plus an actions summary:

**Section 1 — Procurement KPIs** (from S/4HANA):
- 4 headline metric cards: PO count, items, accuracy, contract compliance
- Benchmark comparison table with RAG-status pills across all 5 KPIs
- Semi-donut gauges for PO Accuracy (98%) and Contract Compliance (0.8%)
- Horizontal bar chart showing on-contract vs. off-contract items (4,653 vs. 546,982)

**Section 2 — HR Headcount** (from SuccessFactors):
- 4 headline metrics: 19 total, 3 US, primary grade GR-10, grade span
- Pay grade distribution bar chart (GR-07 through GR-13)
- Geographic coverage map showing all 16 countries with regional groupings
- Regional doughnut chart (Americas / Europe / APAC & Africa)

**Section 3 — Salary Benchmark** (SuccessFactors + market data):
- Animated salary comparison bar chart: 3 US EMs vs. benchmark floor, median, and high
- Individual employee table with precise vs-floor and vs-median deltas
- Full international salary table for all 16 non-US Engineering Managers
- Highlighted action card recommending ~$32K total adjustment

**Actions Summary** — 3 colour-coded priority cards (Red / Amber / Blue)

![Joule response with HTML dashboard download link and table of dashboard sections](images/08_04_0010.png)

## Exercise 8.5 - Export to PDF

Convert the dashboard for a quarterly review pack:

```
Export that dashboard to a PDF for our quarterly review.
```

Joule generates a 3-page print-ready PDF named `SAP_Dashboard_Q4_2026.pdf`. Every page carries an SAP-branded dark-blue header with title and section context, plus a footer with data source attribution and "CONFIDENTIAL — Internal Use Only."

**Section 1 — Procurement KPIs** (~1.5 pages):
- 4 colour-striped metric cards (104,157 POs, 551,635 items, 98% accuracy, 0.8% compliance)
- Full 5-KPI benchmark comparison table with RAG status pills
- Animated visual benchmark bars for PO Accuracy and Contract Compliance
- Contract compliance deep-dive panel with the 330K-item opportunity callout

**Section 2 — Engineering Manager Headcount:**
- 4 metric cards (19 global, 3 US, GR-10 primary grade, GR-07 to GR-13 span)
- Pay grade horizontal bar chart (GR-07 through GR-13)
- Geographic distribution table (Americas / Europe / APAC & Africa)

**Section 3 — Market Salary Benchmark:**
- 4 metric cards including the $12K gap vs. median
- Visual salary positioning bar: 3 US EMs vs. $145K–$245K range and $156K median
- US employee detail table with exact vs-floor and vs-median deltas
- Recommended compensation action callout (~$32K adjustment for GHAMILTON & MHOLDING)
- Full 16-person international salary table in local currencies

**Recommended Actions** — three colour-coded action blocks (Contract Compliance / Comp Review / Savings Tracking) with embedded data source citations.

![Joule response confirming the Q4 2026 PDF export with download link and three-section content description](images/08_05_0010.png)

## Summary

You built a live intelligence dashboard by combining SAP system data with real-world market benchmarks, entirely through conversation. Continue to [Exercise 9 - Knowledge Graph: Explore Hidden Data Relationships](../ex9/README.md).
