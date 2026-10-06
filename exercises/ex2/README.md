# Exercise 2 - Query live S/4HANA data

**Duration:** ~18 min | **Level:** Easy

In this exercise you'll ask Joule to pull data from a real SAP S/4HANA Public Cloud system across several business areas: purchasing, finance, sales, materials, and suppliers. Watch how Joule picks the right Fiori app or OData service for each question without you having to name one.

## Exercise 2.1 - Purchase orders

1. Retrieve your most recent purchase orders:
    ```
    Show me my last 5 purchase orders.
    ```
    Joule returns a table with PO number, supplier, amount, status, and date, all sourced live from S/4HANA.

2. Filter by value:
    ```
    Are there any open purchase orders over $50,000?
    ```

3. Drill into a specific PO:
    ```
    Drill into PO 4500101060 -- show me its line items.
    ```
    Joule moves from the PO header to its individual line items without you switching apps.

## Exercise 2.2 - Cost centres

1. Check a specific cost centre balance:
    ```
    What is the current balance of cost center 10101501?
    ```
    This is the R&D cost centre for company 1710.

2. List all cost centres:
    ```
    Show me all cost centres in controlling area A000.
    ```

## Exercise 2.3 - Finance, sales, and materials

Try each of these in turn:

1. Open vendor invoices:
    ```
    Show me all open vendor invoices from last month.
    ```

2. Top sales orders:
    ```
    Show me the top 5 sales orders by value.
    ```

3. Inventory check:
    ```
    What materials do we have in inventory at plant 1710?
    ```

Each question pulls from a different Fiori app and OData service. Joule routes them automatically.

## Exercise 2.4 - Supplier deep-dive

Look up a specific supplier's master record:

```
Tell me more about supplier 10300001 -- what's their address and VAT number?
```

Joule returns the full supplier profile including name, address, and VAT registration from the Business Partner service.

## Key takeaways

| What you observed | What it means |
|---|---|
| Results appeared without a transaction code | Joule maps your question to the right OData API automatically |
| You could drill into a PO with a follow-up question | Conversation context carries across turns |
| Different topics (POs, invoices, materials) all worked | Joule routes each question to the correct backend service |

## Summary

You've retrieved live data from SAP S/4HANA across five business areas, all through natural language. Continue to [Exercise 3 - Explore HR Data in SuccessFactors](../ex3/README.md).
