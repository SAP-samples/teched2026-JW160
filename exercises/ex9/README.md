# Exercise 9 - Knowledge Graph: explore hidden data relationships

**Duration:** ~20 min | **Level:** Advanced

> [!TIP]
> **Goal:** You've discovered where data lives and navigated cross-system relationships using the Knowledge Graph, without needing to know the technical names in advance.
>
> If you want to try it yourself first, open a new Joule conversation and see how far you get. The step-by-step guide below is there when you need it.

> [!NOTE]
> Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> [!IMPORTANT]
> Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

The SAP Knowledge Graph is a semantic layer that connects data entities across your SAP landscape. Joule uses it to discover relationships you didn't know existed and to answer questions that span multiple systems, without having to name which API to call.

Use this exercise when you don't know where the data lives. Describe what you want and Joule works out the path.

## Exercise 9.1 - Discover what's available

Start by asking what data entities exist across all connected systems:

```
What data entities are available to me across all connected SAP systems?
```

Joule returns a full catalogue of entity types accessible in your landscape, grouped by system — SAP SuccessFactors HCM entities (employees, positions, org structure, performance, time, compensation), S/4HANA entities (procurement, finance, logistics, HR-adjacent), and any connected Ariba or Learning systems.

![Joule response showing the entity catalogue across connected SAP systems with entity names and what you can ask about each](images/09_01_0010.png)

## Exercise 9.2 - Navigate a relationship path

Ask Joule to trace a live cross-system path starting from your own employee record:

```
Starting from my employee record in SuccessFactors, what is the path to the purchase orders that are linked to my cost centre in S/4HANA?
```

Joule executes a multi-hop traversal and returns live data at each step:

- **Step 1:** Your employee identity from SuccessFactors (name, user ID, email)
- **Step 2:** Your job assignment in SuccessFactors, including your assigned cost centre code
- **Step 3:** Purchase order line items in S/4HANA that reference your cost centre as the account assignment object

The path in summary:

```
SuccessFactors                              S/4HANA
────────────────────────────────            ──────────────────────────────────────
EmpJob (userId = <your user>)
  └─ costCenter = <your cost centre>  ───►  C_PurOrdAcctAssignmentTP
                                               └─ CostCenter = <your cost centre>
                                                   └─ PurchaseOrder line items
```

![Joule response showing the 3-hop path from your employee record in SuccessFactors to purchase order line items on your cost centre in S/4HANA](images/09_02_0010.png)

## Exercise 9.3 - Cross-LOB discovery (no system specified)

Ask about a supplier without telling Joule which system to check:

```
Show me everything linked to supplier TS-Tech across all my SAP systems.
```

Joule searches across all connected systems and returns a consolidated summary for the supplier: its business partner profile, purchase order count and sample records from S/4HANA, and any invoice history on record.

![Joule response showing cross-system results for TS-Tech including business partner profile, purchase orders, and invoice count from S/4HANA](images/09_03_0010.png)

## Exercise 9.4 - Surface anomalies

Ask Joule to find inconsistencies between the two systems:

```
Are there any employees in SuccessFactors whose cost centre doesn't exist in S/4HANA cost centre master data?
```

Joule performs a cross-system set comparison: it retrieves all unique cost centres from SuccessFactors employee records, compares them against the cost centre master data in S/4HANA, and identifies orphaned cost centres — codes that exist in SuccessFactors but have no matching record in S/4HANA. The result shows how many employees are assigned to each orphaned cost centre, plus the count of employees with no cost centre assignment at all.

Joule also provides a downloadable CSV with the full list of orphaned cost centres and affected employee counts.

> [!NOTE]
> This is a data quality finding. Employees on orphaned cost centres would fail an ERP lookup if their work triggered a financial transaction against that code.

![Joule response showing the cross-system cost centre comparison with summary counts for matched, orphaned, and empty cost centres](images/09_04_0010.png)

## Exercise 9.5 - Navigate without knowing the technical names

This one requires no SAP knowledge at all:

```
I don't know the technical name of what I need. I want to see who approves purchase orders and whether they are active employees. How would you find that?
```

Joule uses the Knowledge Graph to identify the relevant entities and field names, then executes the query and explains the result:

| Concept | Technical field | What it means |
|---|---|---|
| PO Approver | `ApproverName` on `C_PurchaseOrderTP` | The person who approved (or auto-approved) the PO |
| PO Creator | `CreatedByUser` on `C_PurchaseOrderTP` | The user who raised the PO |
| In Approval | `ReleaseIsNotCompleted` (boolean) | Is the PO still waiting for someone to approve it? |

Joule then explains the cross-system path needed to check approvers against active employees in SuccessFactors: collect approver user IDs from S/4HANA, resolve them to email addresses via the Business User entity, then look up matching users in SuccessFactors and check their active status.

![Joule response showing the Knowledge Graph query approach and technical field names for PO approvers](images/09_05_0010.png)

## When to use the Knowledge Graph

The Knowledge Graph is most useful when:

- You're not sure which system holds the data you need
- You want to discover relationships between entities you wouldn't normally connect
- You're looking for inconsistencies or gaps across systems
- You're exploring an unfamiliar part of your SAP landscape

## Summary

You used the SAP Knowledge Graph to discover data relationships, trace cross-system paths using live data, and surface anomalies, without specifying any APIs or system names. Continue to [Exercise 10 - Upload, Activate and Test a New Skill](../ex10/README.md).
