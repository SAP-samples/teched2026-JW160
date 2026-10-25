# Exercise 2 - Query live S/4HANA data

**Duration:** ~18 min | **Level:** Easy

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

In this exercise you'll ask Joule to pull data from a real SAP S/4HANA Public Cloud system across several business areas: purchasing, finance, sales, materials, and suppliers. Watch how Joule picks the right Fiori app or OData service for each question without you having to name one.

> **Before you start:** Open **Explore Skills** and confirm that only **S/4HANA Public Cloud** is enabled. If you also see an **S/4HANA Private Cloud** skill, disable it — no private cloud system is connected in this workshop tenant and leaving it enabled can cause routing errors or unexpected failures.

## Exercise 2.1 - Purchase orders

1. Retrieve your most recent purchase orders:
    ```
    Show me my last 5 purchase orders.
    ```
    Joule returns a table of your most recent purchase orders sourced live from S/4HANA.

    ![Joule response showing last 5 purchase orders in a table](images/02_01_0010.png)

2. Filter by value within a scope:
    ```
    Are there any purchase orders over $50,000 created in company code 1710 this month?
    ```
    Joule filters to the current month in the specified company code and returns a summary of matching purchase orders.

    > **Note:** Asking across all company codes and all time periods can return a very large dataset and take several minutes. Scoping to a company code and date range keeps the response fast.

3. Drill into a specific PO:
    ```
    Drill into PO 4500101060 and show me its line items.
    ```
    Joule shows the PO header and a line-item table, all without switching apps.

    ![Joule response showing a PO header and its line items](images/02_01_0030.png)

## Exercise 2.2 - Cost centres

1. Look up a specific cost centre:
    ```
    Tell me about cost center 10101501. What company and controlling area does it belong to?
    ```
    Joule retrieves the master data for this cost centre including its company code, controlling area, and other key attributes.

    _Screenshot to be updated._

2. Get an overview of the cost centre landscape:
    ```
    How many cost centres are in controlling area A000, and how are they split across company codes?
    ```
    Joule returns the total count and a breakdown by company code — useful for understanding the scale of the cost centre hierarchy without listing every record.

    > **Note:** Asking Joule to *list* all cost centres in a large controlling area can return hundreds of records and take several minutes. Asking for a count or summary instead returns the same insight in seconds.

## Exercise 2.3 - Finance, sales, and materials

Try each of these in turn:

1. Open vendor invoices:
    ```
    Show me all open vendor invoices from last month.
    ```
    Joule searches across company codes and returns a summary of open invoices — top suppliers by outstanding amount, and the largest individual invoices.

    _Screenshot to be updated._

2. Top sales orders:
    ```
    Show me the top 5 sales orders by value.
    ```
    Joule ranks the top sales orders by value and returns a summary table.

    _Screenshot to be updated._

3. Inventory check:
    ```
    What materials do we have in inventory at plant 1710?
    ```
    Joule identifies the materials available at the specified plant.

    _Screenshot to be updated._

Each question pulls from a different Fiori app and OData service. Joule routes them automatically.

## Exercise 2.4 - Supplier deep-dive

Look up a specific supplier's master record:

```
Tell me more about supplier 10300001. What's their address and VAT number?
```

Joule returns the full supplier profile from the Business Partner service: name, address, and tax details.

_Screenshot to be updated._

## Key takeaways

| What you observed | What it means |
|---|---|
| Results appeared without a transaction code | Joule maps your question to the right OData API automatically |
| You could drill into a PO with a follow-up question | Conversation context carries across turns |
| Different topics (POs, invoices, materials) all worked | Joule routes each question to the correct backend service |

## Summary

You've retrieved live data from SAP S/4HANA across five business areas, all through natural language. Continue to [Exercise 3 - Explore HR Data in SuccessFactors](../ex3/README.md).
