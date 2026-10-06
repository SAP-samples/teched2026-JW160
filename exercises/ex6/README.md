# Exercise 6 - Upload a file and ask Joule to analyse it

**Duration:** ~20 min | **Level:** Intermediate

Joule isn't limited to SAP system data. You can upload your own files and ask it to interpret, summarise, cross-reference, or compare them against live SAP data.

**Supported formats:** Excel (.xlsx / .xls / .csv), PDF (.pdf), Word (.docx), and plain text. You can upload more than one file and ask Joule to compare them.

## Exercise 6.1 - Upload a vendor list

Your instructor has provided a sample vendor spreadsheet (`preferred_vendors.xlsx`). Click the attachment icon in the Joule chat window (or drag and drop the file) to upload it.

1. Once uploaded, ask Joule to summarise it:
    ```
    I've uploaded our vendor list. Summarise it and tell me how many vendors are in each country.
    ```

2. Cross-reference with live S/4HANA data:
    ```
    Which vendors from my uploaded list also exist as suppliers in S/4HANA?
    ```
    Joule compares the uploaded file against the live supplier master and returns the matches, including any IDs that don't exist in the system.

## Exercise 6.2 - Upload a PDF contract

Upload a supplier contract PDF provided by your instructor.

1. Extract key terms:
    ```
    I've uploaded a supplier contract PDF. What are the key payment terms and delivery SLAs?
    ```

2. Check for a penalty clause:
    ```
    Does the contract mention a penalty clause? What is it?
    ```

Joule reads the PDF and pulls out the relevant sections in plain language.

## Exercise 6.3 - Compare two files

Upload two headcount exports -- one from January and one from October (provided by your instructor).

```
Here are two headcount exports from January and October. What changed? Who joined and who left?
```

Joule diffs the two files and reports joiners, leavers, and the net headcount change between the two periods.

## What Joule does with an uploaded file

When you upload a file, Joule reads its content and adds it to the current conversation context. You can then ask questions about it, combine it with live SAP data, or use it as input for a generated document, all in the same conversation thread.

## Summary

You've used Joule to analyse a spreadsheet, extract terms from a PDF contract, and compare two data exports -- combining uploaded files with live S/4HANA supplier data in a single step. Continue to [Exercise 7 - Chaining Multiple Capabilities](../ex7/README.md).
