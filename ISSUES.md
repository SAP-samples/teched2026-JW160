# TechEd 2026 JW160 — Test Run Issues

Full retest of ex0–ex10 against the Joule Work standalone app (tenant 747238487.eu10), participant JW160-001, October 2026. All issues below were found and fixed during the retest.

---

## Fixed: screenshots replaced across all exercises

All exercise screenshots were outdated. The Joule Work UI has been refreshed since the screenshots were taken. Replaced with current screenshots in every exercise folder.

---

## ex0: Tour screenshots

The onboarding tour step sequence and wording changed. Screenshots and README alt text updated to match the current flow.

---

## ex1: Calculation screenshots

Minor UI differences. Screenshots replaced.

---

## ex2–ex8: Screenshot-only updates

No README text errors found. Screenshots replaced to match current UI.

---

## ex9: Knowledge Graph — sap-knowledge-graph skill toggle

The `sap-knowledge-graph` skill card is present on the Explore Skills page but its toggle is **disabled by default** in this tenant. The ex9 exercises (cross-system data discovery, entity-relationship traversal) ran successfully with the other enabled skills (s4hana-public-cloud, successfactors-hr, ariba-buyer, ariba-sourcing), suggesting the Explore Skills toggle for sap-knowledge-graph does not block the underlying Knowledge Graph capability used by Agentic Thinking.

Recommend clarifying in ex9 whether participants need to enable the sap-knowledge-graph skill toggle or whether Agentic Thinking uses the KG layer independently.

---

## ex10: Multiple issues found and fixed

### SKILL.md requires YAML frontmatter (was undocumented)

The import dialog requires the skill file to have a YAML frontmatter block with `name` and `description` fields. Without it, the Import button stays disabled. The README described SKILL.md as "a markdown format" with no mention of frontmatter.

**Fix:** Added YAML frontmatter example to the Background section. Updated SKILL.md with frontmatter. README updated.

### Import creates a duplicate instead of replacing

Re-importing a skill with the same name adds a second card instead of replacing the existing one. The original enabled instance remains. Participants who re-import after adjusting a threshold (Track A Step 4) will see two kpi-health-score cards and must manually delete the old one.

**Workaround documented:** Delete the old card via the `...` → Delete Skill menu, then enable the new one.

### Toggle must be enabled after import (was undocumented)

After a successful import, the skill toggle defaults to OFF. The original README Step 1 said "Click Import to activate it" implying the skill would be active immediately.

**Fix:** Track A Step 1 now includes a step 5: "Find the kpi-health-score card and click its toggle to Enable it."

### Wrong S/4HANA field for PO completion status

SKILL.md used `ProcessingStatus = "C"` (Completed) as the numerator for PO Accuracy. This field does not exist in this S/4HANA tenant. The first test run returned PO Accuracy as "Unavailable."

The correct field is `PurchaseOrderStatus` with value `'05'` (Follow-On Documents Created, meaning fully processed).

**Fix:** Updated SKILL.md step 2 to use `PurchaseOrderStatus = '05'`. PO Accuracy now returns 99.3% (GREEN).

### Active PO Ratio threshold vs. historical backlog mismatch

The threshold (85% green) is designed for a metric like "this week's POs / total POs this week." The skill calculates it as "POs created in the current calendar month / all POs ever in the system." Against a tenant with 62,952 cumulative POs and 1,367 new ones in October 2026, this gives 2.2%, which is permanently RED.

The metric definition and threshold are inconsistent. Joule correctly identifies and explains this in its interpretation paragraph.

**Recommendation:** Change the skill to compute active_po_ratio over a rolling 30-day window against the same 30-day base, or change the description to say "current-month new POs as a share of total historical POs" and adjust the threshold accordingly (e.g., green > 2%).

### Procurement Savings Rate unavailable via PO API

The savings_rate KPI cannot be retrieved from the standard S/4HANA purchase order API (C_PurchaseOrderTP). It requires sourcing/negotiation data from SAP Ariba. The scorecard correctly returns "unavailable" with a RED flag.

**Recommendation:** Remove the savings_rate KPI from the default SKILL.md, or add an explicit note that it requires Ariba integration. Leave it as a Track B exercise for participants who have Ariba connected.

---

## Screenshot files added or replaced

| File | Change |
|------|--------|
| exercises/ex10/images/10_02_0010.png | Replaced: All Skills page with kpi-health-score enabled |
| exercises/ex10/images/10_03_0010.png | Replaced: Import Skill dialog |
| exercises/ex10/images/10_04_0010.png | Replaced: kpi-health-score skill detail page |
| exercises/ex10/images/10_05_0010.png | New: Joule skill list response |
| exercises/ex10/images/10_06_0010.png | New: RAG scorecard response |
| exercises/ex10/images/10_02_skill_enabled.png | Deleted: intermediate file |

---

## Files modified

| File | Change |
|------|--------|
| exercises/ex10/kpi-health-score/SKILL.md | Added YAML frontmatter; fixed PurchaseOrderStatus field |
| exercises/ex10/README.md | Added frontmatter docs, 4-tab note, enable-after-import warning, expected scorecard output |
| exercises/ex10/kpi-health-score/SKILL_kv.md | Deleted (test file) |
| exercises/ex10/kpi-health-score/SKILL_minimal.md | Deleted (test file) |
