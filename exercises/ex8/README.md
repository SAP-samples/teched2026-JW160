# Exercise 8 - Web-augmented intelligence: build a live dashboard

**Duration:** ~25 min | **Level:** Advanced

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

Joule can reach beyond your SAP landscape. In this exercise you ask it to pull industry benchmark data from the web and combine it with live SAP data to build an intelligence dashboard, the kind of view that would normally take a team hours to assemble.

A working example of the dashboard this exercise produces is in `Joule_Dashboard_Exercise8_Example.html` (shared by your instructor). Use it as a reference for what the final output can look like.

## Exercise 8.1 - Get industry benchmarks from the web

Ask Joule to search for current procurement benchmarks:

```
What are the current 2026 benchmarks for procurement savings rate and PO accuracy for manufacturing companies?
```

Joule draws on established procurement research from APQC, The Hackett Group, and Ardent Partners and returns tiered benchmark tables. For manufacturing companies:

**Procurement Savings Rate (% of total managed spend):**
| Performance Tier | Savings Rate |
|---|---|
| World-Class / Best-in-Class | 8% to 12% |
| Industry Average | 4% to 7% |
| Below Average | < 3% |

**PO Accuracy Rate:**
| Performance Tier | PO Accuracy |
|---|---|
| World-Class / Best-in-Class | 97% to 99%+ |
| Industry Average | 88% to 94% |
| Below Average | < 85% |

Additional benchmarks: Spend Under Management (best-in-class >80%, avg 50% to 65%), On-Contract Compliance (>85% vs 60% to 75%), Cost per PO (<$50 vs $75 to $150), Cycle time requisition to PO (<1 day vs 3 to 5 days).

![Joule response showing 2026 procurement benchmarks for manufacturing: Procurement Savings Rate and PO Accuracy tables](images/08_01_0010.png)

## Exercise 8.2 - Compare to your own SAP data

Now layer in your live data:

```
Now compare our company's procurement activity from S/4HANA to those benchmarks.
```

Joule attempts to retrieve spend analytics and PO accuracy figures from S/4HANA. In this demo environment two data categories are unavailable: PO counts and statuses require a service that isn't activated (`MM_PUR_PO_MAINT_V2_SRV`), and spend analytics require an authorization role the connector user doesn't have (`SAP_MM_PUR_ANA_*`). Joule explains the gap clearly, lists the exact steps to unblock it, and shows the comparison table with "Pending access" placeholders so you can see exactly what the populated view would look like.

> **Note:** This is a demo environment limitation. In a production system with the relevant services activated, Joule populates the "Your Company" column with live figures and flags immediately where you're above or below each benchmark.

![Joule response showing data access unavailable for S/4HANA spend analytics, with a comparison table showing Pending placeholders](images/08_02_0010.png)

## Exercise 8.3 - Add HR context

Bring in SuccessFactors data and a market salary range:

```
Add our Engineering Manager headcount from SuccessFactors and the industry benchmark salary range for Engineering Managers ($145K-$245K base, median ~$156K).
```

Joule queries SuccessFactors and returns **23 active Engineering Managers** distributed across 23 unique departments (Engineering, R&D, and Technology units across multiple company codes and cost centres). It combines this with the salary benchmark you provided:

| Benchmark | Base Salary |
|---|---|
| Range Floor | $145,000 |
| Median | ~$156,000 |
| Range Ceiling | $245,000 |
| Typical Total Comp (base + bonus + equity) | $180K to $320K+ |

![Joule response showing 23 Engineering Managers from SuccessFactors and the salary benchmark table](images/08_03_0010.png)

## Exercise 8.4 - Generate the HTML dashboard

Ask Joule to pull everything together into a visual file:

```
Create an HTML dashboard file showing: (1) my procurement KPIs vs industry benchmarks, (2) my team headcount, and (3) market salary context. Make it look professional.
```

Joule generates a self-contained `.html` file. Open it directly in any browser, no server required.

**Dashboard sections:**

| Section | Content |
|---|---|
| At a Glance | 4 KPI headline cards: headcount, PO accuracy, savings rate, median salary |
| Procurement Benchmarks | Full table: 6 KPIs vs. industry average & best-in-class + horizontal bar chart |
| Engineering Manager Headcount | Live count of 23 from SuccessFactors with mini-stats |
| Market Salary Context | Visual range bar + $145K to $245K breakdown with total comp context |
| Department Breakdown | All 23 managers by dept code + interactive donut chart |
| Next Steps | 3 action cards: unblock S/4HANA data, pull comp data, set procurement targets |

The procurement "Your Company" column is marked **Pending** with a note on the S/4HANA services that need to be unlocked to populate it with live figures.

![Joule response with HTML dashboard download link and table of dashboard sections](images/08_04_0010.png)

## Exercise 8.5 - Export to PDF

Convert the dashboard for a quarterly review pack:

```
Export that dashboard to a PDF for our quarterly review.
```

Joule produces a 2-page print-ready PDF:

- **Page 1:** Header, At-a-Glance KPI cards, procurement benchmarks table with data note, Engineering Manager headcount panel, market salary range bar
- **Page 2:** Department breakdown (all 23 managers), recommended next steps, confidential footer with sources

The PDF uses the SAP Horizon colour scheme, a gradient salary range bar, alternating-row benchmark table, and a three-column action plan. It is tagged **CONFIDENTIAL · Q4 2026** in the footer.

![Joule response confirming the Q4 2026 PDF export with download link and two-page content description](images/08_05_0010.png)

## Summary

You built a live intelligence dashboard by combining SAP system data with real-world market benchmarks, entirely through conversation. Continue to [Exercise 9 - Knowledge Graph: Explore Hidden Data Relationships](../ex9/README.md).
