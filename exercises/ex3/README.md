# Exercise 3 - Explore HR data in SuccessFactors

**Duration:** ~18 min | **Level:** Easy

> **Note:** Screenshots were taken on a shared demo environment. The exact values, names, and counts in your session will differ — that is expected.

> **Prerequisite:** Make sure **Agentic Thinking** is enabled before you start. See [Exercise 0: Enable Agentic Thinking](../ex0/README.md#enable-agentic-thinking) if you haven't done this yet.

SAP SuccessFactors covers employee records, org structure, headcount, performance, goals, leave, and recruiting. In this exercise you'll ask Joule to retrieve all of it through conversation, without opening the SuccessFactors interface.

## Exercise 3.1 - Your profile

Start with yourself.

1. Find out your job title and cost centre:
    ```
    What is my current job title and cost centre?
    ```
    Joule identifies your user account automatically and returns your profile from SuccessFactors. The screenshot shows the instructor account (JW160-000) with job title **Specialist** and cost centre **US10_M1**; your result will show your own user ID, job title, and assigned cost centre.

    ![Joule response showing user profile: Specialist in cost centre US10_M1, Shared Services, Company 1710](images/03_01_0010.png)

2. Check your reporting line:
    ```
    Who is my manager and who reports to me?
    ```
    Joule shows your manager and confirms there are no direct reports in this demo environment; the reporting chain isn't fully populated. The manager in the screenshot (JW160 000) belongs to the instructor account; your account will show your own assigned manager.

    ![Joule response showing manager JW160 000 and no direct reports](images/03_01_0020.png)

## Exercise 3.2 - Headcount

1. Count employees in a division:
    ```
    How many employees do we have in the Manufacturing division?
    ```
    Joule searches the org structure and returns **922 active employees** in the Manufacturing (MANU) division.

    ![Joule response showing 922 employees in the Manufacturing division](images/03_02_0010.png)

2. Get a headcount breakdown by division:
    ```
    Who are the employees in company 1710?
    ```
    Company 1710 has **2,430 active employees**. Because that's too many to list individually, Joule returns the first 10 and offers to filter further by division, department, or job title.

    ![Joule response showing company 1710 with 2,430 total employees and first 10 listed](images/03_02_0020.png)

## Exercise 3.3 - Performance and goals

1. Check active performance reviews:
    ```
    Show me the active performance reviews in my organisation.
    ```
    Joule returns **0 active performance reviews**. This is expected in a demo environment; annual review cycles are typically launched in November or December, and no cycle has been started yet for 2026.

    ![Joule response showing 0 active performance reviews](images/03_03_0010.png)

2. Look at team goals:
    ```
    What goals have been set for the Engineering department this year?
    ```
    Joule finds **92 employees** across 11 Engineering departments globally (US, DE, UK, FR, AU, BR, CN, ES, AT, Türkiye, IL). Both 2026 goal plan templates return a permissions restriction — as a Specialist without a manager role, your account can only view your own goals, not those of peers or employees in other departments.

    ![Joule response showing Engineering department with 92 employees and access restricted for goals](images/03_03_0020.png)

## Exercise 3.4 - Time and absence

Ask about your team's remaining leave:

```
How many days of leave does the team have remaining this year?
```

Joule retrieves leave balances for all direct reports of your manager. The team has **82 members**, each with **20 vacation days** remaining this year — **1,640 days** total across the team.

> **Note:** The leave data reflects the Vacation (TAT_VAC_REC) account. Other leave types such as sick leave and time in lieu are tracked separately in the system.

![Joule response showing team leave: 82 employees, 20 days each, 1,640 days total remaining](images/03_04_0010.png)

## Exercise 3.5 - Recruiting

Check for open job requisitions:

```
Are there any open job requisitions in my department?
```

Joule attempts to query the Recruiting module and returns that **no open job requisitions** are currently visible for the Shared Services department (5000018). This is because as a Specialist, you are not assigned a recruiting operator role (Recruiter, Hiring Manager, Sourcer, or Coordinator) on any active requisition — access to requisition data is restricted to users directly involved in the hiring process.

> **Note:** If you had a recruiting role, Joule would list open requisitions for your department with job title, status, and recruiter. You can still view them directly in **SAP SuccessFactors → Recruiting → Job Requisitions** if you have the appropriate access.

![Joule response showing no open job requisitions visible for Shared Services department due to recruiting role access restriction](images/03_05_0010.png)

## A note on permissions

When Joule says it can't show certain data (like goals for people outside your target population, or recruiting requisitions where you have no assigned role), that's the system working correctly. Joule respects Role-Based Permissions. In a production deployment, your permissions would be configured to match your role.

## Key takeaways

| What you observed | What it means |
|---|---|
| Profile and org data returned immediately | SuccessFactors HR data is live, with no data copy or cache |
| Goal results were access-restricted | Role-Based Permissions prevent viewing other employees' goals without a manager or HR role |
| Leave balance shown across 82 team members | Joule can aggregate team data across large headcounts in a single query |
| Job requisitions not visible | Recruiting data access requires a recruiter or hiring manager role on the requisition |

## Summary

You've used Joule to pull employee profiles, org headcount, performance reviews, leave balances, and recruiting data from SuccessFactors through conversation. Continue to [Exercise 4 - Cross-System Queries](../ex4/README.md).
