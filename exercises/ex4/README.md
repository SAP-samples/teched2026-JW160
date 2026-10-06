# Exercise 4 - Cross-system queries

**Duration:** ~25 min | **Level:** Intermediate

Joule can combine data from both SAP S/4HANA and SuccessFactors in a single answer. This exercise runs five scenarios that cross the boundary between ERP and HR.

The natural bridge between the two systems in this environment is **company code 1710** -- it exists as an FI entity in S/4HANA and as an EC company entity in SuccessFactors.

## Exercise 4.1 - Cost centre bridge

Link your HR identity to procurement activity:

```
I am Engineering Manager in company 1710 with cost centre US10_RDGEN. Show me the purchase orders raised in company code 1710 from S/4HANA and tell me how many team members I have from SuccessFactors.
```

Joule makes two API calls, one to each system, and combines the results into a single answer.

## Exercise 4.2 - Manager to procurement responsibility

Resolve a cost centre across both systems:

```
Who in SuccessFactors is assigned to the Purchasing & Store cost centre (10101201 in S/4HANA)? And how many POs ran through that cost centre?
```

## Exercise 4.3 - Headcount vs. spend ratio

Ask Joule to do cross-system arithmetic:

```
For company code 1710, compare the number of active employees (from SuccessFactors) to the number of purchase orders this month (from S/4HANA). What is the PO-per-employee ratio?
```

Joule retrieves each number from a different backend and calculates the ratio.

## Exercise 4.4 - Talent and procurement

```
Who are the top performers in the Procurement-related departments in SuccessFactors, and what purchase requisitions have those departments raised in S/4HANA?
```

## Exercise 4.5 - Org and finance alignment

```
Are there any active employees in SuccessFactors whose cost centre (US10_RDGEN) maps to a cost centre that exists in S/4HANA? List them side by side.
```

Joule may make sequential calls -- first to SuccessFactors for employee and cost-centre data, then to S/4HANA to validate -- before giving you a combined answer.

## Pro tip

Cross-system questions work best when you give Joule an anchor that exists in both systems: a company code, cost centre, or org unit. That's what it uses to join the data.

## Your turn

Write your own cross-system query below. Think about a question from your own work that would normally require two different logins or two separate reports.

```
(your prompt here)
```

## Summary

You've connected data across SAP S/4HANA and SuccessFactors using company code 1710 as the bridge. Joule handled the API calls -- you just asked the question. Continue to [Exercise 5 - Generate a Document from Live Data](../ex5/README.md).
