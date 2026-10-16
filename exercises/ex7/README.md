# Exercise 7 - Chaining multiple capabilities

**Duration:** ~30 min | **Level:** Advanced

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking).
>
> **Skills required:** `s4hana-public-cloud`, `ariba-buyer`, `ariba-sourcing`, `successfactors-hr`, `docx`. Enable all five in Explore Skills before starting.

This exercise chains everything together: live S/4HANA data, SAP Ariba contracts, a file cross-reference, SuccessFactors HR data, and a generated Word document, all in one conversation. It mirrors a real quarterly procurement review.

Work through the five prompts in order, in the same Joule conversation. Don't start a new chat between steps — Joule carries context forward so each step builds on the last.

## Step 1 - Pull top suppliers from S/4HANA

```
Show me the top 10 suppliers by PO spend this quarter from S/4HANA.
```

Joule queries S/4HANA purchase orders for the current quarter (Q4: October–December) and returns a ranked table. In the demo system, based on the first 1,000 of 1,672 Q4 POs:

| Rank | Supplier | Supplier ID | Q4 Spend | POs |
|---|---|---|---|---|
| 1 | Vendor V8005 | USSU_V8005 | $9,415,765.90 | 105 |
| 2 | Vendor V8006 | USSU_V8006 | $7,704,116.50 | 75 |
| 3 | Vendor V8007 | USSU_V8007 | $6,650,087.80 | 84 |
| 4 | Vendor V8003 | USSU_V8003 | $5,026,232.75 | 40 |
| 5 | EmployeePay Inc | USSU-VSF58 | $5,017,566.70 | 28 |
| 6 | Vendor V8004 | USSU_V8004 | $4,715,245.42 | 55 |
| 7 | WaveCrest Labs | USSU_V8001 | $4,388,853.60 | 78 |
| 8 | EV Parts Inc. | USSU_V8000 | $3,640,178.04 | 119 |
| 9 | CorpInMotion Inc | USSU-VSF57 | $1,341,488.36 | 134 |
| 10 | AdNotice | USSU-VSF59 | $1,107,790.78 | 4 |

The top 3 suppliers (V8005, V8006, V8007) account for $23.8M — nearly half the total ~$49M.

![Joule response showing top 10 suppliers ranked by Q4 2026 PO spend, with supplier IDs, total spend, and PO count](images/07_01_0010.png)

## Step 2 - Check contracts for each supplier

```
For each of those suppliers, show me if we have an active contract.
```

> **Allow 10–15 minutes for this step.** Joule checks each supplier individually against both S/4HANA purchase contracts and SAP Ariba strategic contract workspaces. With 10 suppliers to check, this takes longer than the other steps.

In the demo system, all 10 suppliers return no active contract. Joule adds the key finding unprompted:

> **100% Uncontracted Spend** — None of the top 10 suppliers, representing ~$49M in Q4 PO spend, have an active contract on record in S/4HANA or SAP Ariba.

The top 3 suppliers alone (V8005, V8006, V8007) hold $23.7M in uncontracted spend. Joule also flags EmployeePay Inc: a payroll-related vendor at $5M with no contract in place is an unusual finding worth investigating.

![Joule response showing all 10 suppliers with no active contracts found in either S/4HANA or SAP Ariba](images/07_02_0010.png)

## Step 3 - Cross-reference with the preferred vendor list

Upload `preferred_vendors.csv` from the `exercises/ex6/` folder using `+` → **Upload a File or Image**, then ask:

```
I've uploaded our preferred vendor list. Which of the top 10 are on it?
```

Joule checks both by SAP Vendor ID and by company name, including partial matching. In the demo system, none of the 30 vendors on the preferred list appear in the top 10. Joule combines this with the contract findings from Step 2 and surfaces the "Triple Risk" pattern unprompted:

| Risk | Finding |
|---|---|
| Off-preferred-vendor spend | 100% of top 10 suppliers are outside the preferred vendor programme |
| Uncontracted spend | 0 of 10 have an active purchase contract in S/4HANA or SAP Ariba |
| Scale | ~$49M in Q4 PO spend is completely unmanaged |

This is the intended result. The demo data is designed so that actual purchasing has drifted from the preferred supplier strategy — none of the vendors receiving the most spend this quarter are the ones the procurement team designated as preferred.

![Joule response showing combined preferred vendor and contract status columns, plus the Triple Risk summary table](images/07_03_0010.png)

## Step 4 - Find the procurement team in SuccessFactors

```
Who are the purchasing managers or buyers responsible for these suppliers? Look in SuccessFactors for employees in the Procurement department.
```

Joule queries SuccessFactors HR and returns a procurement team directory: 24 people across 6 departments, organised by role level (Heads & Senior Managers, Purchasing Managers, Buyers, Contract roles).

SuccessFactors holds the team structure but not a supplier-to-buyer mapping, so Joule returns the full procurement directory rather than a per-supplier owner. It identifies the contacts most relevant to the uncontracted spend:

- **Rosa Villa** (Procurement Manager, Procurement US) — overall accountability for the spend gap
- **William Blair** (Service Procurement Manager) — particularly relevant for EmployeePay Inc and service-type vendors
- **John Graham** (Contract Manager Jr) and **William Lee** (Contract Administrator Jr) — the people to execute missing contracts

![Joule response showing 24 procurement professionals from SuccessFactors, organised by role level with names, titles, departments, and email addresses](images/07_04_0010.png)

## Step 5 - Generate the review document

```
Create a Word document summarising all of this as a formatted supplier spend review report.
```

Joule generates a downloadable `.docx` file — **Supplier Spend Review Q4 2026.docx** — and lists what it contains:

| Section | Content |
|---|---|
| KPI Summary Bar | $49M total spend · 0/10 contracted · 0/10 on preferred list · 10/10 at risk |
| 1. Executive Summary | Four-point overview across S/4HANA, Ariba, and SuccessFactors |
| 2. Top 10 Suppliers | Full ranked table with spend, PO count, contract status, and preferred vendor status |
| 3. Contract Coverage | Findings per system with a colour-coded risk table (Critical / High / Medium) |
| 4. Preferred Vendor Compliance | Gap analysis with preferred vendor utilisation notes |
| 5. Procurement Team | Sub-tables for Senior Leadership, Purchasing Managers, and Buyers |
| 6. Recommended Actions | Colour-coded action plan by timeframe (Immediate / 30-day / Q1 2027) |
| Appendix | Data sources, methodology, and API references |

Click the document link in Joule's response to download the file.

![Joule response showing a clickable link to Supplier Spend Review Q4 2026.docx and a table of the seven sections in the document](images/07_05_0010.png)

## What to notice

- Joule carries context from step to step — you never need to re-specify the supplier list or company code.
- Each step adds a new data layer: S/4HANA, Ariba contracts, uploaded file, SuccessFactors HR, generated document.
- The Word document draws on everything in the conversation, not just the last prompt.
- The "Triple Risk" pattern — off-preferred-vendor, uncontracted, and high-spend — emerged from combining three separate data sources. No single step would have revealed it on its own.

## Summary

You've run a full Q4 procurement review across two SAP systems, an uploaded file, and a generated report, entirely through conversation. Continue to [Exercise 8 - Web-Augmented Intelligence: Build a Live Dashboard](../ex8/README.md).
