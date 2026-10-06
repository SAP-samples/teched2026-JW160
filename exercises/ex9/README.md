# Exercise 9 - Knowledge Graph: explore hidden data relationships

**Duration:** ~20 min | **Level:** Advanced

The SAP Knowledge Graph is a semantic layer that connects data entities across your SAP landscape. Joule uses it to discover relationships you didn't know existed and to answer questions that span multiple systems without you having to name which API to call.

Use this exercise when you don't know where the data lives. Describe what you want and Joule works out the path.

## Exercise 9.1 - Discover what's available

Start by asking what entities exist across all connected systems:

```
What data entities are available to me across all connected SAP systems?
```

The Knowledge Graph returns a list of entity types -- Employee, PurchaseOrder, CostCenter, Supplier, SalesOrder, PerformanceForm, and more.

## Exercise 9.2 - Navigate a relationship path

Ask Joule to trace a path from your employee record to purchase orders:

```
Starting from my employee record in SuccessFactors, what is the path to the purchase orders that are linked to my cost centre in S/4HANA?
```

The Knowledge Graph maps a 3-hop traversal: **Employee -> CostCenter -> PurchaseOrder**.

## Exercise 9.3 - Cross-LOB discovery (no system specified)

Ask about a supplier without telling Joule which system to check:

```
Show me everything linked to supplier TS-Tech across all my SAP systems.
```

The Knowledge Graph traverses from Supplier to Purchase Orders (S/4HANA) to Contracts, and potentially into Ariba sourcing events, without you specifying which systems to query.

## Exercise 9.4 - Surface anomalies

Ask Joule to find inconsistencies between the two systems:

```
Are there any employees in SuccessFactors whose cost centre doesn't exist in S/4HANA cost centre master data?
```

The Knowledge Graph performs a set-difference across both systems and returns any orphaned cost centres.

## Exercise 9.5 - Navigate without knowing the technical names

This one requires no SAP knowledge at all:

```
I don't know the technical name of what I need. I want to see who approves purchase orders and whether they are active employees. How would you find that?
```

Joule uses the Knowledge Graph to discover the relevant entities and relationships -- you never need to know the field or API names.

## When to use the Knowledge Graph

The Knowledge Graph is most useful when:
- You're not sure which system holds the data you need
- You want to discover relationships between entities you wouldn't normally connect
- You're looking for inconsistencies or gaps across systems
- You're exploring an unfamiliar part of your SAP landscape

## Summary

You've used the SAP Knowledge Graph to discover data relationships, trace paths across systems, and surface anomalies, without specifying any APIs or system names. Continue to [Exercise 10 - Upload, Activate and Test a New Skill](../ex10/README.md).
