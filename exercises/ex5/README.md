# Exercise 5 - Generate a document from live data

**Duration:** ~20 min | **Level:** Intermediate

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

Joule creates files, not just answers. In this exercise you'll generate a Word document, a PDF, and an HTML dashboard from live SAP data, then refine the content through follow-up prompts.

## Exercise 5.1 - Word document

Ask Joule to create a procurement summary:

```
Create a Word document summarising my last 10 purchase orders with a formatted table and a short introduction.
```

Joule retrieves the 10 most recent purchase orders from S/4HANA and produces a downloadable `.docx` file. The document is A4 landscape with alternating row shading, a footer with page number and generation date, and a footnote. The 10 POs are Standard POs (type NB), all under Purchasing Organisation 1710 and supplier USSU-VSF85, with a mix of statuses:

- **23 Oct 2026:** POs 4500104148 to 4500104157 — nine "Ordered / Open" (USD 50–150 each) and one "Partially Delivered" (4500104157, USD 1,500)

![Joule response with Word document download link and feature list for the PO summary](images/05_01_0010.png)

## Exercise 5.2 - PDF report

Convert the same content to PDF:

```
Now generate the same report as a PDF instead of Word.
```

Joule produces a `.pdf` with the same PO data in a branded layout: dark blue header bar with report title and generation date, alternating row shading with status values colour-coded (green for Ordered/Open, amber for Partially Delivered), and a mid-blue footer with "Confidential" label. PDFs keep the layout fixed, which makes them useful for archiving, emailing, or sending for sign-off.

![Joule response with PDF download link and description of the branded dark-blue layout](images/05_02_0010.png)

## Exercise 5.3 - HTML dashboard

Create a browser-ready dashboard:

```
Can you create an HTML dashboard showing my purchase order activity and team headcount side by side?
```

Joule generates a self-contained `.html` file with:

- **KPI metrics at the top:** Total POs on record (104,157), status breakdown of the latest 10, total active headcount (4,053)
- **Left panel:** Bar chart by net amount per PO (colour-coded green for open, amber for partial) + full PO table with number, date, supplier, value, and status badge
- **Right panel:** Doughnut chart by division, horizontal bar chart by top locations, and department table ranked by size

The file can be opened in any browser, published to an intranet, or embedded in a presentation.

> **Note:** The headcount panel shows all active employees across SuccessFactors (4,053 total), not just direct reports. The division/location charts are based on a sample of 200 employee records; the 4,053 total is the precise live count.

![Joule response with HTML dashboard download link and KPI strip preview](images/05_03_0010.png)

## Exercise 5.4 - Iterate on the output

Refine the document through follow-up prompts without starting over.

### Add an executive summary

```
Add an executive summary at the top.
```

Joule adds an executive summary section to the Word document. It is placed at the top before the original report and contains:

- An "Executive Summary" heading with a coloured rule
- A KPI tile bar with four dark-blue/green/amber tiles: 104,157 Total POs on Record · USD 2,550 Value (latest 10) · 9/10 Ordered & Open · 1/10 Partially Delivered
- Four bullet findings covering procurement volume, order values, delivery status, and recommended actions
- A divider rule separating the summary from the original PO table

![Joule response confirming executive summary added to the HTML dashboard](images/05_04_0010.png)

### Translate it

```
Translate the executive summary into German.
```

Joule translates the executive summary section into German, leaving the original PO table in English (field values from SAP). The translated labels include:

| English | German |
|---|---|
| Executive Summary | Zusammenfassung |
| Total POs on Record | Bestellungen gesamt |
| Value — Latest 10 POs | Wert – Letzte 10 Bestellungen |
| Ordered & Open | Bestellt & Offen |
| Partially Delivered | Teilgeliefert |
| ▸ Procurement Volume | ▸ Beschaffungsvolumen |
| ▸ Order Values | ▸ Bestellwerte |
| ▸ Delivery Status | ▸ Lieferstatus |
| ▸ Recommended Actions | ▸ Empfohlene Maßnahmen |

![Joule response showing the German executive summary preview with Beschaffungsaktivität and Teamübersicht sections](images/05_04_0020.png)

## Document types Joule can produce

| Format | Best for |
|---|---|
| Word (.docx) | Reports, memos, summaries, HR and procurement briefs |
| PDF (.pdf) | Archiving, emailing, signing: fixed layout |
| HTML (.html) | Browser viewing, intranet publishing, PowerPoint import |
| CSV (.csv) | Raw data export for Excel or further analysis |
| Inline table/chart | Quick answers shown directly in the chat window |

## Pro tip

After downloading a file, you can upload it back into the Joule conversation and ask for further edits, for example: *"Please add page numbers to this document."*

## Summary

You've generated Word, PDF, and HTML outputs from live SAP data and refined them through follow-up prompts. Continue to [Exercise 6 - Upload a File and Ask Joule to Analyse It](../ex6/README.md).
