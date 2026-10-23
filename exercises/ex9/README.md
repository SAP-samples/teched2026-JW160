# Exercise 9 - Knowledge Graph: explore hidden data relationships

**Duration:** ~20 min | **Level:** Advanced

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

The SAP Knowledge Graph is a semantic layer that connects data entities across your SAP landscape. Joule uses it to discover relationships you didn't know existed and to answer questions that span multiple systems, without having to name which API to call.

Use this exercise when you don't know where the data lives. Describe what you want and Joule works out the path.

## Exercise 9.1 - Discover what's available

Start by asking what data entities exist across all connected systems:

```
What data entities are available to me across all connected SAP systems?
```

Joule returns a full catalogue of every entity type accessible in your landscape, grouped by system:

**SAP SuccessFactors HR:** Core HR (User, PositionEntity, EmpJob, EmpEmployment, PerPersonal, FamilyEntity, and many more), plus Payroll, Time Management, Compensation, Performance, and Learning entities

**SAP S/4HANA Public Cloud & Private Cloud:** ERP entities across procurement, finance, logistics, and HR-adjacent domains (purchase orders, suppliers, cost centres, G/L accounts, employees, and others)

**SAP Ariba Buyer:** Catalog, Procurement Requisitions, Operational Contracts, Master Data (Platform)

**SAP Ariba Sourcing:** Sourcing Events (RFx events, bids, awards), Sourcing Projects, Strategic Contracts (contract workspaces, terms, NDA export), Supplier Management (questionnaires, certificates, workspaces)

![Joule response showing the full entity catalogue across SAP Ariba Buyer, Ariba Sourcing, S/4HANA, SuccessFactors HR, and SuccessFactors Learning](images/09_01_0010.png)

## Exercise 9.2 - Navigate a relationship path

Ask Joule to trace a live cross-system path starting from your own employee record:

```
Starting from my employee record in SuccessFactors, what is the path to the purchase orders that are linked to my cost centre in S/4HANA?
```

Joule executes a 3-hop traversal and returns actual live data at each step. The values below come from the instructor account (JW160-001); your result will show your own user ID and the cost centre assigned to your account.

Step 1: Your employee record (SuccessFactors)

| Field | Value |
|---|---|
| Name | JW160 001 |
| User ID | JW160-001 |
| Email | jw160-001@demo.cloud.sap |
| Job Title | Specialist |
| Department | 5000018 |
| Cost Centre | **US10_M1** |

**Step 2: The link.** Your SuccessFactors job record holds a cost centre code (`US10_M1`). The same code is stamped on purchase order line items in S/4HANA as the account assignment (the accounting object that bears the spend).

**Step 3: Purchase orders in S/4HANA.** **1,161 PO line items** are assigned to cost centre US10_M1, all with account assignment category **K** (= Cost Centre).

The data path in summary:

```
SuccessFactors                           S/4HANA
──────────────────────────               ──────────────────────────────────────
EmpJob (userId = JW160-001)
  └─ costCenter = "US10_M1"  ──────►   C_PurOrdAcctAssignmentTP
                                           └─ CostCenter = "US10_M1"
                                               └─ PurchaseOrder (1,161 items)
```

![Joule response showing the 3-hop path from employee JW160-001 to 1,161 PO line items on cost centre US10_M1](images/09_02_0010.png)

## Exercise 9.3 - Cross-LOB discovery (no system specified)

Ask about a supplier without telling Joule which system to check:

```
Show me everything linked to supplier TS-Tech across all my SAP systems.
```

Joule searches across all connected systems and returns a consolidated summary:

| System | Area | Finding |
|---|---|---|
| S/4HANA | Business Partner | Supplier USSU-VSF85, New Milford NJ, US (SAP S/4HANA Public Cloud) |
| S/4HANA | Purchase Orders | **4,744 POs** total (Standard NB type, Purchasing Org 1710) |
| S/4HANA | Supplier Invoices | **2,019,334 invoice line items** on record |

![Joule response showing cross-LOB summary for TS-Tech: 4,744 POs in S/4HANA and 2,019,334 supplier invoices](images/09_03_0010.png)

## Exercise 9.4 - Surface anomalies

Ask Joule to find inconsistencies between the two systems:

```
Are there any employees in SuccessFactors whose cost centre doesn't exist in S/4HANA cost centre master data?
```

Joule performs a cross-system set comparison across SuccessFactors and S/4HANA:

| Metric | Value |
|---|---|
| Total employees in SuccessFactors | 3,995 |
| Unique cost centres in SuccessFactors | 319 |
| Cost centres found in S/4HANA | 689 |
| Cost centres matched (SF found in S/4HANA) | 106 |
| Orphaned SF cost centres (not in S/4HANA) | **213** |
| Employees on orphaned cost centres | **1,687** |
| Employees with no cost centre at all | 124 |

Joule also provides a downloadable CSV with the full list of orphaned cost centres and affected employee counts. The "Top 20 Orphaned Cost Centres" table is shown inline, ranked by number of affected employees.

This is a real data quality finding: 1,687 employees in SuccessFactors are assigned to cost centres that have no match in S/4HANA, which means any spend or allocation against those employees would fail an ERP lookup. The 124 employees with no cost centre assignment at all represent a separate onboarding gap.

![Joule response showing cross-system cost centre comparison: 213 orphaned cost centres and 1,687 affected employees, with downloadable CSV](images/09_04_0010.png)

## Exercise 9.5 - Navigate without knowing the technical names

This one requires no SAP knowledge at all:

```
I don't know the technical name of what I need. I want to see who approves purchase orders and whether they are active employees. How would you find that?
```

Joule uses the Knowledge Graph to identify the relevant entities and field names, then executes the query and explains the result:

**What the technical fields are:**

| Concept | Technical field | What it means |
|---|---|---|
| PO Approver | `ApproverName` on `C_PurchaseOrderTP` | The person who approved (or auto-approved) the PO |
| PO Creator | `CreatedByUser` on `C_PurchaseOrderTP` | The user who raised the PO |
| In Approval | `ReleaseIsNotCompleted` (boolean) | Is the PO still waiting for someone to approve it? |

**What was found in S/4HANA** (102,951 purchase orders accessible):

| Finding | Detail |
|---|---|
| POs awaiting approval right now | **0**: no PO is currently pending a human sign-off |
| Approver names in sampled POs | All show `"Approved automatically"` (the flexible workflow is configured to auto-approve) |
| PO creator in sample | `CB9980000052`, a system/service user, not a named individual |
| Flexible workflow active? | Yes: all POs carry the flexible workflow flag |
| PR API (purchase requisitions) | **403 Forbidden** — not accessible with current permissions |
| Workflow task service | **403 Forbidden** — workflow task history not accessible |

**The identity mapping challenge:** S/4HANA PO creator IDs (`CB9980000052`) are in a different namespace than SuccessFactors user IDs (`JW160-000`, `aacar`). To cross-check approvers against active employees, the path would be:

```
Step 1: S/4HANA
  C_PurchaseOrderTP → ApproverName / CreatedByUser
  → S/4HANA Business User → email address

Step 2: SuccessFactors
  User entity → filter by email → check status (active/inactive)

Step 3: Flag any approver/creator whose SF status ≠ active
```

In this environment, all POs are auto-approved by a system user, with no human names to cross-check. This is worth flagging to a procurement team: if the intent is that a human manually approves POs, the workflow configuration may need adjusting.

![Joule response showing the PO approver field names, the finding that all POs are auto-approved, and the identity mapping path needed to cross-check against SuccessFactors](images/09_05_0010.png)

## When to use the Knowledge Graph

The Knowledge Graph is most useful when:

- You're not sure which system holds the data you need
- You want to discover relationships between entities you wouldn't normally connect
- You're looking for inconsistencies or gaps across systems
- You're exploring an unfamiliar part of your SAP landscape

## Summary

You used the SAP Knowledge Graph to discover data relationships, trace cross-system paths using live data, and surface anomalies, without specifying any APIs or system names. Continue to [Exercise 10 - Upload, Activate and Test a New Skill](../ex10/README.md).
