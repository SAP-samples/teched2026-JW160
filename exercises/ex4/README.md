# Exercise 4 - Cross-system queries

**Duration:** ~25 min | **Level:** Intermediate

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

Joule can combine data from SAP S/4HANA and SuccessFactors in a single answer. This exercise runs five scenarios that cross the ERP/HR boundary.

The bridge between the two systems in this environment is **company code 1710**, which exists as a financial entity in S/4HANA and a company entity in SuccessFactors.

## Exercise 4.1 - Cost centre bridge

Link your HR identity to procurement activity:

```
I am Engineering Manager in company 1710 with cost centre US10_RDGEN. Show me the purchase orders raised in company code 1710 from S/4HANA and tell me how many team members I have from SuccessFactors.
```

Joule makes two API calls in parallel (one to S/4HANA for purchase orders, one to SuccessFactors for your team), then combines both into a single response. The result shows **62,296 purchase orders** in company 1710 (first 15 rows displayed, all Standard POs with supplier USSU-V100 under Purchasing Organisation 1710) and **41 direct reports** (JW160-001 through JW160-041, all Specialists in department 5000018).

![Joule response showing 62,296 POs in company 1710 and 41 team members listed](images/04_01_0010.png)

## Exercise 4.2 - Manager to procurement responsibility

Resolve a cost centre across both systems:

```
Who in SuccessFactors is assigned to the Purchasing & Store cost centre (10101201 in S/4HANA)? And how many POs ran through that cost centre?
```

Joule checks both systems and finds that cost centre 10101201 is labelled "Purch & Store 1 (DE)", a German legal entity cost centre. **No active employees** are assigned to it in SuccessFactors, and **0 purchase orders** ran through it in S/4HANA. Joule also surfaces the US equivalent, **17101201 (Purch & Store 1 US)**, which has 461 PO account assignment records and offers to check that cost centre instead.

This shows Joule reasoning across locale boundaries: the user asked about a DE cost centre, but the active activity is in the US equivalent.

![Joule response showing cost centre 10101201 (DE) has no employees or POs, and highlighting US equivalent 17101201 with 461 PO records](images/04_02_0010.png)

## Exercise 4.3 - Headcount vs. spend ratio

Ask Joule to do cross-system arithmetic:

```
For company code 1710, compare the number of active employees (from SuccessFactors) to the number of purchase orders this month (from S/4HANA). What is the PO-per-employee ratio?
```

Joule queries both systems in parallel and calculates the ratio. For company 1710: **2,224 active employees** (SuccessFactors) and **905 purchase orders** created so far in October 2026 (S/4HANA), giving a **PO-per-employee ratio of 0.41** — roughly 1 PO for every 2.5 employees in the month to date.

> **Note:** The PO count reflects orders created from 1 October to the date of the query, not a full month. Joule flags this in its response and projects the end-of-month total at ~1,800 POs (~0.81 per employee) assuming a linear creation pace.

![Joule response showing cross-system table: 2,224 active employees from SuccessFactors, 905 POs from S/4HANA in October 2026, PO-per-employee ratio of 0.41](images/04_03_0010.png)

## Exercise 4.4 - Talent and procurement

```
Who are the top performers in the Procurement-related departments in SuccessFactors, and what purchase requisitions have those departments raised in S/4HANA?
```

Joule identifies **17 procurement-related departments** with **72 active employees** across 15 of them. The largest is Procurement (US) with 15 employees (department 50300001, cost centre US10_M5), with notable staff including Rosa Villa (Procurement Manager), Denzel Coleman (Sourcing & Procurement Head), and Melissa Holmes (Purchasing Manager).

For purchase requisitions in S/4HANA, Joule finds **401 PRs** in company 1710, all under Purchasing Organisation 1710 with release status "Not Necessary". Group 005 (Transportation Services) accounts for 346 of them (86%), with the most recent dated 12 October 2026.

Performance ratings are not available for employees outside your direct reporting chain. This is a role-based permission boundary, not a data gap. Joule notes that linking procurement HR departments to their S/4HANA PRs requires a cost centre bridge (e.g. US10_M5 for Procurement US) rather than a direct department-to-purchasing-group mapping.

![Joule response showing 17 procurement departments with 72 employees and 401 purchase requisitions by purchasing group](images/04_04_0010.png)

## Exercise 4.5 - Org and finance alignment

```
Are there any active employees in SuccessFactors whose cost centre (US10_RDGEN) maps to a cost centre that exists in S/4HANA? List them side by side.
```

Joule confirms that cost centre **US10_RDGEN** exists and is active in both systems. In S/4HANA it is labelled "R&D-General", belongs to Controlling Area A000 / Company Code 1710, profit centre US10_PC10, category L (General/Overhead), valid since 1950. In SuccessFactors the HR master label isn't returned but the code and company (1710) match.

The side-by-side employee list shows **86 active employees** on cost centre US10_RDGEN across 10 departments, ranging from VP Operations and VP R&D to Engineering Interns, Project Managers, and Field Service Technicians.

![Joule response showing cost centre US10_RDGEN confirmed in both systems and employee list with 86 active staff](images/04_05_0010.png)

## Pro tip

Cross-system questions work best when you give Joule a shared anchor that exists in both systems: a company code, cost centre, or org unit. That's what it uses to join the data from two backends into one answer.

## Your turn

Write your own cross-system query. Think of something from your own work that would normally require two different logins or two separate reports.

```
(your prompt here)
```

## Summary

You've connected data across SAP S/4HANA and SuccessFactors using company code 1710 as the bridge. Joule handled the API calls. You just asked the question. Continue to [Exercise 5 - Generate a Document from Live Data](../ex5/README.md).
