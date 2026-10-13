# Exercise 5 - Generate a document from live data

**Duration:** ~20 min | **Level:** Intermediate

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

Joule creates files, not just answers. In this exercise you'll generate a Word document, a PDF, and an HTML dashboard from live SAP data, then refine the content through follow-up prompts.

## Exercise 5.1 - Word document

Ask Joule to create a procurement summary:

```
Create a Word document summarising my last 10 purchase orders with a formatted table and a short introduction.
```

Joule retrieves the 10 most recent purchase orders from S/4HANA and produces a downloadable `.docx` file. The document is A4 landscape, blue colour scheme, with alternating row shading, a header and footer with page numbers, and a footnote. The 10 POs are Standard POs (type NB), all in USD under Purchasing Organisation 1710, all with status "In Process":

- **13 Oct 2026:** POs 4500102976 to 4500102982 (suppliers USSU-VSF81 ×4, USSU-VSF82 ×2, USSU-VSF83 ×1)
- **12 Oct 2026:** POs 4500102840 to 4500102842 (supplier USSU-VSF85 ×3)

![Joule response with Word document download link and feature list for the PO summary](images/05_01_0010.png)

## Exercise 5.2 - PDF report

Convert the same content to PDF:

```
Now generate the same report as a PDF instead of Word.
```

Joule produces a `.pdf` with the same PO data in a branded layout: dark blue header bar labelled "SAP S/4HANA Public Cloud — Confidential", alternating light-blue and white table rows, and a dark blue footer. PDFs keep the layout fixed, which makes them useful for archiving, emailing, or sending for sign-off.

![Joule response with PDF download link and description of the branded dark-blue layout](images/05_02_0010.png)

## Exercise 5.3 - HTML dashboard

Create a browser-ready dashboard:

```
Can you create an HTML dashboard showing my purchase order activity and team headcount side by side?
```

Joule generates a self-contained `.html` file with:

- **KPI strip at the top:** 10 Purchase Orders · 3 Suppliers · 41 Headcount · 100% In Process
- **Left panel:** PO donut chart by supplier + bar chart by date + full PO table
- **Right panel:** 4 stat tiles + horizontal bar chart (41 Specialists) + scrollable team list (Shared Services, Executive Office, US-Philadelphia)

The file can be opened in any browser, published to an intranet, or embedded in a presentation.

![Joule response with HTML dashboard download link and KPI strip preview](images/05_03_0010.png)

## Exercise 5.4 - Iterate on the output

Refine the document through follow-up prompts without starting over.

### Add an executive summary

```
Add an executive summary at the top.
```

Joule adds an executive summary banner between the header and the KPI strip. It is split into two columns (**Procurement Activity** and **Team Overview**), each with highlighted key figures pulled from the live data.

![Joule response confirming executive summary added to the HTML dashboard](images/05_04_0010.png)

### Translate it

```
Translate the executive summary into German.
```

Joule translates only the executive summary section, leaving the charts, table, and team list in English (they are source-system field values). The translated sections are labelled **📦 Beschaffungsaktivität** and **👥 Teamübersicht**:

> *In den vergangenen 2 Tagen (12.–13. Oktober 2026) wurden insgesamt 10 Standard-Bestellungen (NB) unter Einkaufsorganisation 1710 angelegt, alle in USD...*
>
> *Das Team umfasst derzeit 41 aktive direkt unterstellte Mitarbeiter, alle mit der Bezeichnung Spezialist innerhalb der Abteilung Shared Services...*

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
