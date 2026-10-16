# kpi-health-score

## Description

Pulls live procurement data from S/4HANA and headcount data from SuccessFactors, evaluates both against configurable thresholds, and returns a RAG-coded (Red/Amber/Green) health scorecard.

Default company code: 1710. Specify a different code in your prompt if needed.

## Triggers

- kpi health check
- procurement health score
- run a kpi check
- health score for company
- show our kpis
- what is our procurement health

## Thresholds

Edit the values below to match your organisation's targets. After saving, re-import this file via **Explore Skills** to apply the changes.

```yaml
thresholds:
  po_accuracy:
    label: PO Accuracy
    description: Completed POs as a share of all POs in the period
    unit: ratio
    green: "> 0.98"
    amber: ">= 0.98"    # Track A: change this to 0.96
    red: "< 0.98"
  savings_rate:
    label: Procurement Savings Rate
    description: Negotiated savings as a share of total addressable spend
    unit: ratio
    green: "> 0.08"
    amber: ">= 0.04"
    red: "< 0.04"
  active_po_ratio:
    label: Active PO Ratio
    description: POs created in the current calendar month as a share of all POs
    unit: ratio
    green: "> 0.85"
    amber: ">= 0.70"
    red: "< 0.70"
```

## Instructions

When someone requests a KPI health check or procurement health score:

1. Ask for a company code if none was given. Use 1710 as the default.

2. Retrieve procurement data from S/4HANA for that company code:
   - Total purchase order count from `C_PurchaseOrderTP`
   - POs with `ProcessingStatus = "C"` (Completed) for the `po_accuracy` numerator
   - POs where `CreationDate` falls in the current calendar month for `active_po_ratio` numerator

3. Retrieve headcount data from SuccessFactors for the same company code:
   - Active employees: `EmpEmployment` where `active = true` and `company = <code>`
   - Engineering Managers: `EmpJob` where `jobTitle` contains "Engineering Manager" and `company = <code>`

4. Calculate:
   - `po_accuracy` = completed POs / total POs
   - `active_po_ratio` = current-month POs / total POs
   - `savings_rate` = report 0 and flag as unavailable if the data is not accessible

5. Score each KPI against the thresholds above:
   - GREEN: value meets the green condition
   - AMBER: value meets the amber condition but not green
   - RED: value falls below the amber threshold
   - INFO: no threshold applies (informational metrics)

6. Return a scorecard in this format:

| KPI | Value | Green threshold | Status |
|-----|-------|-----------------|--------|
| PO Accuracy | XX.X% | > 98% | 🟢 / 🟡 / 🔴 |
| Procurement Savings Rate | X.X% | > 8% | 🟢 / 🟡 / 🔴 |
| Active PO Ratio | XX.X% | > 85% | 🟢 / 🟡 / 🔴 |
| Active Employees | X,XXX | — | ℹ️ |
| Engineering Managers | XX | — | ℹ️ |

7. Add a 2-3 sentence interpretation below the table. Note any metrics that could not be retrieved and what impact that has on the score.

<!-- Track B: add your own KPI here

Copy one of the threshold blocks above into the thresholds section, then add the corresponding retrieval and calculation step.

Example: Employees per Active PO
  - id: employees_per_active_po
  - label: Employees per Active PO
  - description: Active headcount divided by current-month PO count (workload proxy)
  - unit: ratio
  - green: "> 0.02"
  - amber: ">= 0.01"
  - red: "< 0.01"
  - retrieval: active employees (EmpEmployment, active=true) / current-month POs (C_PurchaseOrderTP, CreationDate in current month)
-->
