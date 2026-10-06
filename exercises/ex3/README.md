# Exercise 3 - Explore HR data in SuccessFactors

**Duration:** ~18 min | **Level:** Easy

SAP SuccessFactors covers employee records, org structure, headcount, performance, goals, leave, and recruiting. In this exercise you'll ask Joule to retrieve all of it through conversation, without opening the SuccessFactors interface.

## Exercise 3.1 - Your profile

Start with yourself.

1. Find out your job title and cost centre:
    ```
    What is my current job title and cost centre?
    ```
    Joule identifies the session user automatically and returns your profile from SuccessFactors.

2. Check your reporting line:
    ```
    Who is my manager and who reports to me?
    ```

## Exercise 3.2 - Headcount

1. Count employees in a division:
    ```
    How many employees do we have in the Manufacturing division?
    ```

2. List employees in a specific company:
    ```
    Who are the employees in company 1710?
    ```

## Exercise 3.3 - Performance and goals

1. Check active performance reviews:
    ```
    Show me the active performance reviews in my organisation.
    ```

2. Look at team goals:
    ```
    What goals have been set for the Engineering department this year?
    ```

## Exercise 3.4 - Time and absence

Ask about your team's remaining leave:

```
How many days of leave does the team have remaining this year?
```

Joule aggregates leave balances across your team from the Time Off module.

## Exercise 3.5 - Recruiting

Check for open job requisitions:

```
Are there any open job requisitions in my department?
```

## A note on permissions

If Joule says it can't show certain data, that's expected. Your role in SuccessFactors determines what you can see, and Joule respects those boundaries. Try a different question or check with your instructor if you're unsure what access you have.

## Reflection

- Which queries returned results straight away?
- Did Joule clarify or rephrase any of your questions before answering?
- How does this compare to navigating SuccessFactors manually?

## Summary

You've used Joule to pull employee profiles, headcount, performance, time-off, and recruiting data from SuccessFactors through conversation. Continue to [Exercise 4 - Cross-System Queries](../ex4/README.md).
