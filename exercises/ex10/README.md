# Exercise 10 - Upload, activate and test a new skill

**Duration:** ~30 min | **Level:** Expert

Skills are pre-built capability packs that extend what Joule can do. They connect Joule to additional systems, APIs, and domain knowledge beyond its built-in set. In this final exercise you'll upload a skill, activate it, and test it at the depth that fits your background.

## Background: what is a skill?

A skill is a configuration package that tells Joule which APIs to call, what data entities are available, how to interpret questions in a specific domain, and how to format results. Think of it as a plug-in: once activated, Joule gains new expertise without any redeployment.

Skill packages are typically provided by:
- Your SAP system administrator or Centre of Excellence
- The SAP Joule Skill Catalogue (accessible via your user profile -> Explore Skills)
- A custom skill built by your internal IT team

## Choose your track

This exercise runs at three levels. Work through the track that fits your background.

---

### Track A -- Business User (~20 min)

*For: finance managers, HR leads, operations -- no coding background*

Your instructor has provided a pre-built **KPI Health Score** skill as a YAML file. This skill pulls live data from S/4HANA and SuccessFactors, evaluates it against configurable thresholds, and returns a colour-coded RAG (Red/Amber/Green) health score.

**Step 1 -- Upload the skill:**
1. Click your user profile icon in the bottom-left corner of Joule.
2. Select **Explore Skills** from the menu.
3. Click **Upload Skill** (or **Import Skill** depending on your version).
4. Select the `kpi-health-score.yaml` file provided by your instructor.
5. Review the description and permissions, then click **Install / Activate**.

**Step 2 -- Verify the skill is active:**
```
What skills do you currently have available?
```

**Step 3 -- Change a threshold:**

Open `kpi-health-score.yaml` in a text editor. Find the `po_accuracy` block and change the amber threshold from `0.98` to `0.96`. Save the file and re-upload it via **Explore Skills**.

**Step 4 -- Test your change:**
```
What is our procurement health score for company 1710?
```

The PO Accuracy row in the result should now reflect your updated threshold.

---

### Track B -- Power User / Analyst (~25 min)

*For: business analysts, consultants, power users -- comfortable with config files*

Start from the YAML template provided by your instructor and add a new KPI.

**Step 1 -- Open the YAML template** and find the commented-out section at the bottom:
```yaml
# Track B: add your own KPI here
# - id: my_kpi
#   label: My Custom KPI
#   domain: Cross-System
#   ...
```

**Step 2 -- Define a new KPI:** Add an "Employees per Active PO" metric. It requires data from both SuccessFactors (headcount) and S/4HANA (PO count). Ask your instructor for the OData entity names if you need them.

**Step 3 -- Upload and test** your extended skill. Then run a comparison:
```
Run a KPI check and show me the before and after for the new metric.
```

---

### Track C -- Developer (~30 min)

*For: BTP developers, SAP BTP architects -- full technical background*

Build the KPI engine as a microservice and connect it to Joule via the A2A (Agent-to-Agent) protocol.

**Step 1 -- Scaffold the agent:**
Use the `joule-a2a-agent` starter project. Implement the KPI engine as a TypeScript or Python microservice with its own tools for querying S/4HANA and SuccessFactors.

**Step 2 -- Deploy to BTP:**
Deploy to BTP Cloud Foundry. You'll need a service instance bound to both the S/4HANA and SuccessFactors APIs.

**Step 3 -- Register with Joule:**
Register the agent via the A2A protocol and publish an Agent Card.

> **Note:** Your Joule instance must be on schema version >= 3.28.0 for A2A support. Run `joule status` to confirm before starting.

**Step 4 -- Test end-to-end:**
```
Run a KPI health check.
```

Joule should route the prompt to your external A2A agent. Confirm in your agent's logs that the call arrived.

---

## All tracks converge

At the end of the session, all three tracks demo using the same prompt:
```
Run a KPI health check for company 1710.
```

Track A's threshold change and Track C's A2A agent both respond, showing the same Joule extensibility story at three different levels of depth.

## Design your own workflow

Before you leave, take five minutes to think about a recurring task in your own role that involves data from multiple systems. Try to sketch it as 3-5 steps Joule could handle:

1. *(your step 1)*
2. *(your step 2)*
3. *(your step 3)*

Share it with the group.

## Summary

You've installed a Joule skill, customised it for your role, and tested it with live SAP data. That's all 10 exercises done.

---

*If you have questions about the skill design patterns covered in this exercise, the full assessment document (`Joule_Skill_Workshop_Assessment.docx`) is available from your instructor.*
