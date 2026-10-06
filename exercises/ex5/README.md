# Exercise 5 - Generate a document from live data

**Duration:** ~20 min | **Level:** Intermediate

Joule doesn't just answer questions -- it creates files too. In this exercise you'll generate a Word document, a PDF, and an HTML dashboard from live SAP data, then refine the content through follow-up prompts.

## Exercise 5.1 - Word document

Ask Joule to create a procurement summary:

```
Create a Word document summarising my last 10 purchase orders with a formatted table and a short introduction.
```

Joule produces a downloadable `.docx` file with headings, a formatted PO table, and an introduction, all sourced from live S/4HANA data.

## Exercise 5.2 - PDF report

Convert the same content to PDF:

```
Now generate the same report as a PDF instead of Word.
```

PDFs are useful when the layout needs to stay fixed -- for archiving, emailing, or sending for signature.

## Exercise 5.3 - HTML dashboard

Create a browser-ready dashboard:

```
Can you create an HTML dashboard showing my purchase order activity and team headcount side by side?
```

The HTML file can be opened in any browser, published to an intranet, or embedded in a presentation.

## Exercise 5.4 - Iterate on the output

Refine the document through follow-up prompts without starting over:

1. Add an executive summary:
    ```
    Add an executive summary at the top.
    ```

2. Translate it:
    ```
    Translate the executive summary into German.
    ```

Each follow-up updates the existing document rather than generating a new one.

## Document types Joule can produce

| Format | Best for |
|---|---|
| Word (.docx) | Reports, memos, summaries, HR and procurement briefs |
| PDF (.pdf) | Archiving, emailing, signing -- fixed layout |
| HTML (.html) | Browser viewing, intranet publishing, PowerPoint import |
| CSV (.csv) | Raw data export for Excel or further analysis |
| Inline table/chart | Quick answers shown directly in the chat window |

## Pro tip

After downloading a file, you can upload it back into the Joule conversation and ask for further edits -- for example: *"Please add page numbers to this document."*

## Summary

You've generated Word, PDF, and HTML outputs from live SAP data and refined them through follow-up prompts. Continue to [Exercise 6 - Upload a File and Ask Joule to Analyse It](../ex6/README.md).
