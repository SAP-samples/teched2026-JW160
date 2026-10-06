# Exercise 8 - Web-augmented intelligence: build a live dashboard

**Duration:** ~25 min | **Level:** Advanced

Joule can go beyond your SAP landscape. In this exercise you'll ask it to pull real-world market data from the web and combine it with live SAP data to build an intelligence dashboard -- the kind of view that would normally take a team hours to put together.

A working example of the dashboard this exercise produces is in `Joule_Dashboard_Exercise8_Example.html` (shared by your instructor). Use it as a reference for what the final output can look like.

## Exercise 8.1 - Get industry benchmarks from the web

Ask Joule to search for current procurement benchmarks:

```
What are the current 2026 benchmarks for procurement savings rate and PO accuracy for manufacturing companies?
```

Joule searches the web and returns figures from sources like dragonsourcing.com, gep.com, and jaggaer.com. Typical benchmarks include:
- PO Accuracy: >= 98%
- On-Time Delivery: >= 95%
- Contract Compliance: >= 90-95%
- Procurement Savings Rate: 5-15%

## Exercise 8.2 - Compare to your own SAP data

Now layer in your live data:

```
Now compare our company's procurement activity from S/4HANA to those benchmarks.
```

Joule retrieves your actual procurement figures and overlays them against the industry targets, flagging where you're ahead or behind.

## Exercise 8.3 - Add HR context

Bring in SuccessFactors and a market salary range:

```
Add our Engineering Manager headcount from SuccessFactors and the industry benchmark salary range for Engineering Managers ($145K-$245K base, median ~$156K).
```

## Exercise 8.4 - Generate the HTML dashboard

Ask Joule to pull everything together into a visual file:

```
Create an HTML dashboard file showing: (1) my procurement KPIs vs industry benchmarks, (2) my team headcount, and (3) market salary context. Make it look professional.
```

Joule generates a self-contained HTML file with three panels, KPI indicators, and colour-coded RAG (Red/Amber/Green) status against each benchmark. Open it directly in your browser.

**Dashboard panels:**
| Panel | Content | Data source |
|---|---|---|
| Procurement KPIs | PO accuracy, OTD, contract compliance, savings rate vs benchmarks | S/4HANA + Web |
| Team Overview | Engineering headcount, company 1710 context, PO-per-employee ratio | SuccessFactors + S/4HANA |
| Market Intelligence | Engineering Manager salary band, procurement benchmark sources | Web Search |

## Exercise 8.5 - Export to PDF

Convert the dashboard for a quarterly review pack:

```
Export that dashboard to a PDF for our quarterly review.
```

## Summary

You've built a live intelligence dashboard that combines SAP system data with real-world market benchmarks, entirely through conversation. Continue to [Exercise 9 - Knowledge Graph: Explore Hidden Data Relationships](../ex9/README.md).
