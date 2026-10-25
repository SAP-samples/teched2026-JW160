# Exercise 6 - Upload a file and ask Joule to analyse it

**Duration:** ~20 min | **Level:** Intermediate

> [!NOTE]
> Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> [!NOTE]
> **Instructor note:** This exercise uses four sample files included in this repository: `preferred_vendors.csv`, `supplier_contract.pdf` (a supplier contract), `headcount_jan2026.csv`, and `headcount_oct2026.csv`. All four files are in the `exercises/ex6/` folder.

> [!IMPORTANT]
> Make sure **Agentic Thinking** is enabled before you start. File upload only appears in the `+` menu when Agentic Thinking is active.

Joule isn't limited to SAP system data. You can upload your own files and ask it to interpret, summarise, cross-reference, or compare them against live SAP data.

**Supported formats:** Excel (.xlsx / .xls / .csv), PDF (.pdf), Word (.docx), and plain text. You can upload more than one file in the same conversation.

## How to upload a file

Open a new conversation and enable Agentic Thinking via the `+` button. Then click `+` again: you'll see **Upload a File or Image** at the top of the menu. Click it to open the file picker, then select your file.

![Empty Joule conversation with + and @ buttons in the input area](images/06_01_0010.png)

After enabling Agentic Thinking, the chip appears in the input bar:

![Input bar with Agentic Thinking chip active](images/06_upload_button.png)

Click `+` again to reveal the upload option:

![+ menu open showing Upload a File or Image, Agentic Thinking, and Space options](images/06_01_0030.png)

After selecting a file, it appears as a card above the text box; you can then type your question and send:

![File card showing preferred_vendors.csv attached in the input area with Agentic Thinking enabled](images/06_01_0050.png)

With the file attached, type your question and send:

![File card attached with the vendor list prompt typed in and ready to send](images/06_01_0060.png)

You can also drag and drop a file directly onto the chat input area.

The `@` button (bottom-left of the input) opens a list of specialised assistants. You can activate one to focus Joule on that domain.

![@ menu showing Billing Assistant, Sourcing Assistant, and SAP LeanIX Joule Capabilities options](images/06_assistants_menu.png)

## Exercise 6.1 - Upload a vendor list

Upload `preferred_vendors.csv` via `+` → **Upload a File or Image**, then ask:

```
I've uploaded our vendor list. Summarise it: how many vendors are there, which countries are represented, and what is the total annual spend?
```

Joule reads the file and returns a breakdown of vendor count by country and a spend total. Follow up with a contract expiry check:

```
Which vendors have contracts expiring in the next 6 months? List their names, contract end dates, and annual spend.
```

Then cross-reference the uploaded list against live S/4HANA data:

```
Which vendors from my uploaded list also exist as suppliers in S/4HANA?
```

Joule searches the S/4HANA supplier master for each vendor in the uploaded file. If the commercial names in the CSV don't match the legal entity names stored in S/4HANA — or the vendors aren't formally onboarded in the ERP — Joule flags the mismatch and suggests alternative approaches: search by SAP Vendor Number, search by country, or onboard the missing vendors directly.

## Exercise 6.2 - Upload a PDF contract

Upload `supplier_contract.pdf`, then extract key terms:

```
I've uploaded a supplier contract PDF. What are the key payment terms and delivery SLAs?
```

Joule reads the PDF and returns a structured breakdown of the payment terms and delivery SLAs found in the document — including standard payment windows, early payment discounts, delivery lead times, and any special requirements.

![Joule response showing payment terms and delivery SLAs extracted from the uploaded contract](images/06_02_0010.png)

Follow up with a specific question:

```
Does the contract mention a penalty clause? What is it?
```

Joule identifies the penalty clause section and explains the delay penalty structure, cancellation rights, and any early warning obligations defined in the contract.

![Joule response showing the penalty clause section with delay rates and cancellation terms](images/06_02_0020.png)

## Exercise 6.3 - Compare two files

Upload the two headcount CSV exports in the same conversation. The app accepts one file per message, so upload `headcount_jan2026.csv` first with a short note, then attach `headcount_oct2026.csv` in a follow-up message and ask:

```
Here are two headcount exports from January and October. What changed? Who joined and who left?
```

Joule reads both files from the conversation context and produces a full diff: a summary table with total headcount change, joiners, leavers, and promotions, followed by detailed lists for each category with names, departments, and roles.

![Joule response showing headcount comparison summary table and joiners list](images/06_03_0020.png)

## What Joule does with an uploaded file

When you attach a file, Joule reads its content and adds it to the current conversation context. You can then ask questions about it, combine it with live SAP data, or use it as input for a generated document, all in the same conversation thread.

## Summary

You've used Joule to analyse a spreadsheet, extract terms from a PDF contract, and compare two data exports, combining uploaded files with live S/4HANA supplier data in a single step. Continue to [Exercise 7 - Chaining Multiple Capabilities](../ex7/README.md).
