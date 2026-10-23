# Exercise 7 - Chaining multiple capabilities

**Duration:** ~30 min | **Level:** Advanced

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking).
>
> **Skills required:** `s4hana-public-cloud`, `ariba-buyer`, `ariba-sourcing`, `successfactors-hr`, `docx`. Enable all five in Explore Skills before starting.

This exercise chains everything together: live S/4HANA data, SAP Ariba contracts, a file cross-reference, SuccessFactors HR data, and a generated Word document, all in one conversation. It mirrors a real quarterly procurement review.

Work through the five prompts in order, in the same Joule conversation. Don't start a new chat between steps — Joule carries context forward so each step builds on the last.

## Step 1 - Pull top suppliers from S/4HANA

```
Show me the top 10 suppliers by PO spend this quarter from S/4HANA.
```

Joule queries S/4HANA purchase orders for the current quarter (Q4: October–December) and returns a ranked table. In the demo system, Joule retrieves the full dataset (2,452 POs for Q4 2026):

| Rank | Supplier | Supplier ID | Q4 Spend | POs |
|---|---|---|---|---|
| 1 | Vendor V8005 | USSU_V8005 | $19,079,348 | 209 |
| 2 | Vendor V8006 | USSU_V8006 | $18,483,468 | 174 |
| 3 | Vendor V8007 | USSU_V8007 | $15,782,797 | 193 |
| 4 | EmployeePay Inc | USSU-VSF58 | $15,052,700 | 84 |
| 5 | Vendor V8003 | USSU_V8003 | $10,959,583 | 87 |
| 6 | Vendor V8004 | USSU_V8004 | $10,882,331 | 129 |
| 7 | WaveCrest Labs | USSU_V8001 | $9,418,398 | 161 |
| 8 | EV Parts Inc. | USSU_V8000 | $7,803,463 | 259 |
| 9 | CorpInMotion Inc | USSU-VSF57 | $3,374,745 | 402 |
| 10 | AdNotice | USSU-VSF59 | $2,773,717 | 12 |

The top 10 account for ~$113.6M, representing 92% of the total ~$123.5M Q4 spend across all suppliers.

![Joule response showing top 10 suppliers ranked by Q4 2026 PO spend, with supplier IDs, total spend, and PO count](images/07_01_0010.png)

## Step 2 - Check contracts for each supplier

```
For each of those suppliers, show me if we have an active contract.
```

> **Allow 10–15 minutes for this step.** Joule checks each supplier individually against both S/4HANA purchase contracts and SAP Ariba strategic contract workspaces. With 10 suppliers to check, this takes longer than the other steps.

In the demo system, all 10 suppliers return no active contract in S/4HANA. Joule reports that S/4HANA holds 13 active purchase contracts, but all are with different suppliers (Garrett Motion Inc., AV Parts Inc., NPN Electricals Ltd., ABS Labs, TS-Tech, and others), not the high-spend ones. Joule adds the key finding unprompted:

> **100% Uncontracted Spend** — None of the top 10 suppliers, representing $113.6M in Q4 PO spend (92% of total quarter volume), have an active contract on record in S/4HANA.

Joule recommends checking Ariba Sourcing separately, as there may be strategic contracts or sourcing events in progress not yet linked to S/4HANA purchase contracts. It also flags EmployeePay Inc: a payroll-related vendor at $15M with no contract in place is an unusual finding worth investigating.

![Joule response showing all 10 suppliers with no active contracts found in either S/4HANA or SAP Ariba](images/07_02_0010.png)

## Step 3 - Cross-reference with the preferred vendor list

Upload `preferred_vendors.csv` from the `exercises/ex6/` folder using `+` → **Upload a File or Image**, then ask:

```
I've uploaded our preferred vendor list. Which of the top 10 are on it?
```

Joule checks both by SAP Vendor ID and by company name, including partial matching. In the demo system, none of the 30 vendors on the preferred list appear in the top 10. Joule combines this with the contract findings from Step 2 and surfaces the combined risk picture unprompted:

| Issue | Suppliers Affected | Spend at Risk |
|---|---|---|
| Not on preferred vendor list | All 10 | $113.6M |
| No purchase contract in S/4HANA | All 10 | $113.6M |

This is the intended result. The demo data is designed so that actual purchasing has drifted from the preferred supplier strategy — none of the vendors receiving the most spend this quarter are the ones the procurement team designated as preferred. Joule also suggests the vendor IDs may not match (preferred list uses format USSU-V100, while active purchases use USSU_V8000) and offers to check the broader Q4 dataset for any preferred vendor spend.

![Joule response showing combined preferred vendor and contract status columns, plus the Triple Risk summary table](images/07_03_0010.png)

## Step 4 - Find the procurement team in SuccessFactors

```
Who are the purchasing managers or buyers responsible for these suppliers? Look in SuccessFactors for employees in the Procurement department.
```

Joule queries SuccessFactors HR and returns a procurement team directory: 39 people across 4 groups (Sourcing & Procurement Leadership, Managers, Buyers & Purchasers, Contract Roles), organised by role level.

SuccessFactors holds the team structure but not a supplier-to-buyer mapping, so Joule returns the full procurement directory rather than a per-supplier owner. It identifies the contacts most relevant to the uncontracted spend:

- **Rosa Villa** (Procurement Manager, Procurement US) — overall accountability for the spend gap
- **William Blair** (Service Procurement Manager) — particularly relevant for EmployeePay Inc and service-type vendors
- **John Graham** (Contract Manager Jr) and **William Lee** (Contract Administrator Jr) — the people to execute missing contracts

![Joule response showing 24 procurement professionals from SuccessFactors, organised by role level with names, titles, departments, and email addresses](images/07_04_0010.png)

## Step 5 - Generate the review document

```
Create a Word document summarising all of this as a formatted supplier spend review report.
```

Joule generates a downloadable `.docx` file — **Supplier Spend Review — Q4 2026.docx** — and lists what it contains:

| Section | Content |
|---|---|
| 1. Executive Summary | High-level narrative + KPI table highlighting the 0% contract and preferred vendor coverage |
| 2. Top 10 Suppliers | Full ranked table with supplier IDs, names, PO counts, spend, and % of total; alternating row shading |
| 3. Contract Coverage | Supplier-by-supplier contract status with colour-coded risk ratings (High / Medium) |
| 4. Preferred Vendor List | Alignment summary, match results, and three root-cause hypotheses |
| 5. Procurement Team | Two tables from SuccessFactors — leadership/managers and buyers/contract roles with emails |
| 6. Risk & Recommendations | Six prioritised action items with severity, recommended action, and named owner |
| 7. Data Sources | Audit trail of systems and entities used |

Click the document link in Joule's response to download the file.

![Joule response showing a clickable link to Supplier Spend Review Q4 2026.docx and a table of the seven sections in the document](images/07_05_0010.png)

## What to notice

- Joule carries context from step to step — you never need to re-specify the supplier list or company code.
- Each step adds a new data layer: S/4HANA, Ariba contracts, uploaded file, SuccessFactors HR, generated document.
- The Word document draws on everything in the conversation, not just the last prompt.
- The combined risk pattern — off-preferred-vendor, uncontracted, and high-spend — emerged from combining three separate data sources. No single step would have revealed it on its own.

## Summary

You've run a full Q4 procurement review across two SAP systems, an uploaded file, and a generated report, entirely through conversation. Continue to [Exercise 8 - Web-Augmented Intelligence: Build a Live Dashboard](../ex8/README.md).
