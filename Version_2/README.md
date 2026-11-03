# Version 2 — Workflow Catalog

[Project overview](../README.md) · [Quick start](../docs/QUICK_START.md) · [Version 1 reference](../Version_1/README.md)

Start here when choosing a workflow. This folder contains nine Markdown specifications, each with its own scope, inputs, process, and review requirements. Supply the selected file to a capable AI assistant with the relevant source data and tools; browsing this folder does not execute it.

## Choose the right workflow

| Task | Workflow | Prepare before starting | Key review |
| --- | --- | --- | --- |
| Convert journals, invoices, trial balances, or master data for an accounting-system import | [Accounting import alignment](Accounting_Import_Format_Alignment_Skill.md) | Source export, exact target specification, approved code crosswalks | Source-to-output reconciliation and target-schema validation |
| Prepare a U.S. income-tax provision and corporate tax workpapers | [U.S. GAAP and tax](US_GAAP_tax_Skill.md) | Approved records, entity/tax classification, reporting and tax dates, supporting schedules | Financial-reporting and tax professional review |
| Prepare IFRS income-tax reporting and Hong Kong profits-tax workpapers | [IFRS and Hong Kong tax](HK_IFRS_tax_Skill.md) | Confirmed reporting basis, trial balance, tax schedules, year of assessment | Financial-reporting and Hong Kong tax professional review |
| Build a revenue-led budget, forecast, and scenarios | [FP&A](FPandA_Skills.md) | Sales detail, cost drivers, resource capacity, opening balances, targets | Sales, department, Controller, and Finance review |
| Reformat finance data for an ERP, report, or presentation table | [Format alignment](Format_alignment_Skill.md) | Source files, target schema, mapping and reference data | Reconciliation, duplicate controls, rejected-record treatment |
| Refresh an existing presentation using new figures | [PowerPoint update](PowerPoint_Template_Data_Update_SKILL.md) | Editable template deck, approved data, as-of date and update scope | Numerical consistency, editability, visual inspection |
| Prepare the finance section of a board pack | [Board reporting](Strategic_reporting_board_Skill.md) | Approved plan, actuals, latest outlook, initiative updates, board calendar | Decision clarity, consistent figures, CFO and pack-control review |
| Combine entities or departments into a group dataset | [Group consolidation](Consolidation_group_finance_Skill.md) | Submissions, scope, mapping, currency policy, supporting schedules | Completeness, reconciliation, and mode-specific adjustments |
| Compare a company with its industry peers | [Competitor analysis](Competitor-analysis-SKILL.md) | Industry/anchor company, purpose, geography, as-of date | Comparable definitions, primary evidence, transparent judgments |

## Resolve common overlaps

**Accounting import alignment or format alignment?** Choose accounting import alignment for a specific accounting-system object such as a journal or AP invoice. Choose format alignment for broader finance transformations, including reporting and presentation datasets. For an overlapping import task, select one lead workflow and one authoritative mapping.

**Data combination or consolidation?** The consolidation workflow distinguishes simple data combination, management consolidation, and accounting consolidation. Select the mode explicitly. Stacking entity files alone does not complete accounting consolidation.

**FP&A or board reporting?** FP&A builds the model and explains the forecast. Board reporting turns reviewed results, strategic progress, and risks into decisions and oversight material. Reference the approved model version.

**Board reporting or PowerPoint update?** Board reporting defines the content and decisions. The PowerPoint workflow refreshes an existing presentation and checks consistency with the approved content.

## File names and module references

Some playbooks retain proposed paths and module identifiers from the original project plan. Use the actual links above when opening files in this repository.

| Reference inside a playbook | Repository interpretation |
| --- | --- |
| Module 01 / `01_accounting.md` | Planned general accounting-treatment module; not currently supplied. The accounting import workflow has a narrower purpose. |
| Module 02 / `02_tax.md` | Split into the U.S. and Hong Kong tax workflows linked above. |
| `2.1_US_GAAP_tax.md` / `2.2_HK_IFRS_tax.md` | Internal identifiers for the corresponding tax workflow files. |
| Module 03 / `03_fpa.md` | `FPandA_Skills.md` |
| Module 04 / `04_format_alignment.md` | `Format_alignment_Skill.md` |
| Module 05 / `05_ppt_update.md` | `PowerPoint_Template_Data_Update_SKILL.md` |
| Module 06 / `06_reporting.md` | `Strategic_reporting_board_Skill.md` |
| Group consolidation / competitor analysis | Separate workflows; select by business purpose rather than assuming a shared module number. |

References to other skills, software, or local folders describe execution dependencies. Those dependencies are not bundled merely because they appear in a Markdown file.

## Version and validation policy

- Record each file's internal version and the repository commit SHA when logging a run.
- `Version_2` identifies this collection; it does not mean every playbook has internal version `2.0`.
- A documented test, an arithmetic check, a completed tool execution, and a client acceptance decision are different evidence. Record exactly what was performed.
- The [roadmap](../docs/ROADMAP.md) separates available specifications from work still needed for an integrated pilot.
