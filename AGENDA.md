# JW160 - Working Smarter with Joule
## SAP TechEd 2026 — Session Agenda

**Format:** Hands-on lab | **Total time:** ~3 hours 15 minutes  
**No SAP background required.** All exercises run through natural-language conversation with Joule.

---

## What this session covers

You'll use **Joule**, SAP's AI assistant, to retrieve live data, generate business documents, analyse uploaded files, combine data across systems, and extend Joule's capabilities with a custom skill — all through conversation, no transaction codes.

**Systems used:** SAP S/4HANA Public Cloud · SAP SuccessFactors

---

## Exercises at a glance

| # | Topic | Level | Time |
|---|---|---|---|
| 0 | Getting Started | — | 5 min |
| 1 | Say Hello to Joule | Beginner | 8 min |
| 2 | Query Live S/4HANA Data | Easy | 18 min |
| 3 | Explore HR Data in SuccessFactors | Easy | 18 min |
| 4 | Cross-System Queries | Intermediate | 25 min |
| 5 | Generate a Document from Live Data | Intermediate | 20 min |
| 6 | Upload a File and Analyse It | Intermediate | 20 min |
| 7 | Chaining Multiple Capabilities | Advanced | 10 min |
| 8 | Web-Augmented Intelligence | Advanced | 25 min |
| 9 | Knowledge Graph | Advanced | 20 min |
| 10 | Upload, Activate and Test a Skill | Expert | 30 min |

---

## Exercise descriptions

### 0 — Getting Started (5 min)
Open Joule and confirm it's connected to both SAP systems. Covers: Fiori Launchpad access, the Joule chat panel, and a first test query to verify the S/4HANA and SuccessFactors connections.

---

### 1 — Say Hello to Joule · Beginner · 8 min
A first conversation to understand how Joule communicates. No SAP data yet.
- Ask Joule to introduce itself and explain its capabilities
- Test its limitations and data-freshness behaviour
- Run a simple calculation to confirm it handles follow-up questions

---

### 2 — Query Live S/4HANA Data · Easy · 18 min
Pull data from a real SAP S/4HANA Public Cloud system across several business areas.
- **2.1** Purchase orders — list, filter by value, drill into line items
- **2.2** Cost centres — check balances, list by controlling area
- **2.3** Finance, sales, and materials — open invoices, top sales orders, inventory
- **2.4** Supplier deep-dive — full supplier master including address and VAT

---

### 3 — Explore HR Data in SuccessFactors · Easy · 18 min
Retrieve HR data through conversation without opening the SuccessFactors interface.
- **3.1** Your profile — job title, cost centre, reporting line
- **3.2** Headcount — by division and company
- **3.3** Performance and goals — active reviews, team goals
- **3.4** Time and absence — team leave balances
- **3.5** Recruiting — open job requisitions

---

### 4 — Cross-System Queries · Intermediate · 25 min
Combine live data from S/4HANA and SuccessFactors in a single answer. The bridge between both systems is company code **1710**.
- **4.1** Cost centre bridge — link HR identity to procurement activity
- **4.2** Manager to procurement responsibility — resolve a cost centre across systems
- **4.3** Headcount vs. spend ratio — cross-system arithmetic
- **4.4** Talent and procurement — top performers mapped to purchase requisitions
- **4.5** Org and finance alignment — validate cost centres across both systems

---

### 5 — Generate a Document from Live Data · Intermediate · 20 min
Joule creates downloadable files from live SAP data and refines them through follow-up prompts.
- **5.1** Word document — procurement summary with formatted table
- **5.2** PDF report — same content, fixed layout for archiving or signing
- **5.3** HTML dashboard — PO activity and team headcount side by side
- **5.4** Iterate on the output — add an executive summary, translate to German

---

### 6 — Upload a File and Analyse It · Intermediate · 20 min
Upload your own files and cross-reference them against live SAP data.
- **6.1** Vendor list spreadsheet — summarise and cross-reference against S/4HANA supplier master
- **6.2** PDF contract — extract payment terms, delivery SLAs, and penalty clauses
- **6.3** Compare two files — diff two headcount exports to find joiners and leavers

---

### 7 — Chaining Multiple Capabilities · Advanced · 10 min
Run a full quarterly procurement review in a single conversation: live ERP data, live HR data, an uploaded vendor list, and a generated Word report — five steps, roughly two minutes each.

---

### 8 — Web-Augmented Intelligence · Advanced · 25 min
Combine real-world market data from the web with live SAP data to build an intelligence dashboard.
- **8.1** Pull industry procurement benchmarks from the web (PO accuracy, OTD, savings rate)
- **8.2** Overlay your company's live S/4HANA figures against those benchmarks
- **8.3** Add SuccessFactors headcount and market salary context
- **8.4** Generate an HTML dashboard with RAG status indicators
- **8.5** Export the dashboard to PDF for a quarterly review pack

---

### 9 — Knowledge Graph · Advanced · 20 min
Use the SAP Knowledge Graph to discover data relationships you didn't know existed, without specifying APIs or system names.
- **9.1** Discover available data entities across all connected systems
- **9.2** Trace a relationship path: Employee → Cost Centre → Purchase Order
- **9.3** Cross-LOB discovery — surface everything linked to a supplier across all systems
- **9.4** Surface anomalies — find employees whose cost centre doesn't exist in S/4HANA
- **9.5** Navigate without knowing technical names

---

### 10 — Upload, Activate and Test a Skill · Expert · 30 min
Install and customise a Joule skill — a plug-in that extends Joule's capabilities with new APIs and domain knowledge.

Three tracks based on background:

| Track | Audience | What you do |
|---|---|---|
| **A — Business User** | Finance/HR/Ops managers | Upload the pre-built KPI Health Score skill, change a threshold, verify the result |
| **B — Power User** | Business analysts, consultants | Extend the YAML template with a new cross-system KPI metric |
| **C — Developer** | BTP developers/architects | Build the KPI engine as a microservice and connect it to Joule via the A2A protocol |

All three tracks converge on the same closing prompt: `Run a KPI health check for company 1710.`

---

## By the end of this session you will have

- Retrieved live procurement and HR data through conversation
- Combined data from S/4HANA and SuccessFactors in a single answer
- Generated Word, PDF, and HTML outputs from live SAP data
- Used web search to compare your company's KPIs against industry benchmarks
- Explored data relationships through the SAP Knowledge Graph
- Installed and tested a custom Joule skill
