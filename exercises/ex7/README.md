# Exercise 7 - Chaining multiple capabilities

**Duration:** ~10 min | **Level:** Advanced

This exercise chains everything together: live S/4HANA data, live SuccessFactors data, a file cross-reference, and a generated document, all in one conversation. It mirrors a real quarterly procurement review.

This one is faster than it looks. Five steps, roughly two minutes each.

## The workflow

Work through these five prompts in order, in the same Joule conversation. Don't start a new chat between steps -- Joule keeps the context so you don't have to repeat yourself.

**Step 1 -- Pull top suppliers from S/4HANA:**
```
Show me the top 10 suppliers by PO spend this quarter from S/4HANA.
```

**Step 2 -- Check contracts for those suppliers:**
```
For each of those suppliers, show me if we have an active contract.
```

**Step 3 -- Cross-reference with your preferred vendor list:**

Upload the `preferred_vendors.xlsx` file from Exercise 6 (or re-use the one already in the conversation), then ask:
```
I've uploaded our preferred vendor list. Which of the top 10 are on it?
```

**Step 4 -- Find the relationship manager in SuccessFactors:**
```
Who manages each supplier relationship? Check SuccessFactors.
```

**Step 5 -- Generate the review document:**
```
Create a Word document with all of this as a formatted review report.
```

Joule assembles data from both SAP systems, your uploaded file, and the current conversation into a single downloadable `.docx` file.

## What to notice

- Joule carries context from step to step -- you never need to re-specify the supplier list or company code.
- Each step adds a new data layer: ERP, contracts, vendor list, HR, document.
- The final Word document reflects everything in the conversation, not just the last prompt.

## Timing

Most participants finish this in 5-8 minutes. If you're moving quickly, that's the point -- chaining capabilities in Joule is faster than the equivalent manual process.

## Summary

You've run a full quarterly procurement review across two SAP systems, an uploaded file, and a generated report, entirely through conversation. Continue to [Exercise 8 - Web-Augmented Intelligence: Build a Live Dashboard](../ex8/README.md).
