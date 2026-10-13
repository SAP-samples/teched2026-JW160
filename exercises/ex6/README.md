# Exercise 6 - Upload a file and ask Joule to analyse it

**Duration:** ~20 min | **Level:** Intermediate

> **Instructor note:** This exercise requires the sample files distributed at the start of the session. Make sure you have `preferred_vendors.xlsx`, a supplier contract PDF, and the two headcount CSVs before you start.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. File upload only appears in the `+` menu when Agentic Thinking is active.

Joule isn't limited to SAP system data. You can upload your own files and ask it to interpret, summarise, cross-reference, or compare them against live SAP data.

**Supported formats:** Excel (.xlsx / .xls / .csv), PDF (.pdf), Word (.docx), and plain text. You can upload more than one file in the same conversation.

## How to upload a file

Open a new conversation and enable Agentic Thinking via the `+` button. Then click `+` again: you'll see **Upload a File or Image** at the top of the menu. Click it to open the file picker, then select your file.

![Empty Joule conversation with + and @ buttons in the input area](images/06_01_0010.png)

Click `+` with Agentic Thinking active to reveal the upload option:

![+ menu open showing Upload a File or Image, Agentic Thinking, and Space options](images/06_01_0030.png)

After selecting a file, it appears as a card above the text box; you can then type your question and send:

![File card showing preferred_vendors.csv attached in the input area with Agentic Thinking enabled](images/06_01_0050.png)

You can also drag and drop a file directly onto the chat input area.

The `@` button (bottom-left of the input) opens a list of specialised assistants (@Billing Assistant, @Sourcing Assistant, @Supplier Management Assistant, and others). You can activate one to focus Joule on that domain.

## Exercise 6.1 - Upload a vendor list

Upload `preferred_vendors.xlsx` via `+` → **Upload a File or Image**, then ask:

```
I've uploaded our vendor list. Summarise it and tell me how many vendors are in each country.
```

Joule reads the spreadsheet and returns a country-by-country breakdown of vendor counts. Follow up with a cross-reference against live S/4HANA data:

```
Which vendors from my uploaded list also exist as suppliers in S/4HANA?
```

Joule compares the uploaded file against the live supplier master and returns matches, including any IDs that don't exist in the system.

## Exercise 6.2 - Upload a PDF contract

Upload the supplier contract PDF, then extract key terms:

```
I've uploaded a supplier contract PDF. What are the key payment terms and delivery SLAs?
```

Follow up with a specific question:

```
Does the contract mention a penalty clause? What is it?
```

Joule reads the PDF and pulls out the relevant sections in plain language, without needing to scroll through pages of legalese.

## Exercise 6.3 - Compare two files

Upload both headcount CSV exports (January and October) in the same conversation, then ask:

```
Here are two headcount exports from January and October. What changed? Who joined and who left?
```

Joule diffs the two files and reports joiners, leavers, and the net headcount change.

## What Joule does with an uploaded file

When you attach a file, Joule reads its content and adds it to the current conversation context. You can then ask questions about it, combine it with live SAP data, or use it as input for a generated document, all in the same conversation thread.

## Summary

You've used Joule to analyse a spreadsheet, extract terms from a PDF contract, and compare two data exports, combining uploaded files with live S/4HANA supplier data in a single step. Continue to [Exercise 7 - Chaining Multiple Capabilities](../ex7/README.md).
