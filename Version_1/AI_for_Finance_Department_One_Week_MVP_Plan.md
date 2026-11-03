# AI for Finance Department — One-Week MVP Project Plan

**Project week:** Monday, November 2–Sunday, November 8, 2026  
**Review target:** Sunday, November 8, 2026  
**Objective:** Build and demonstrate six reusable, client-agnostic Markdown-based finance workflows. After the internal review, adapt the workflows to individual clients rather than hard-coding client details into the core system.

## 1. What will be ready by Sunday

An **MVP (minimum viable prototype)**, not an unattended production accounting or tax system:

1. Six tested `.md` workflows covering accounting, tax, FP&A, data-format alignment, PowerPoint updating, and strategic reporting.
2. Shared data contracts and controls covering provenance, assumptions, approvals, privacy, and error handling.
3. An anonymized or synthetic example company with sample financial data, an ERP-import schema, a PowerPoint template, and company objectives.
4. An end-to-end demonstration with logs of what was automated, what was checked, and what still needs professional review.
5. A 5–8-slide review presentation or equivalent demonstration package, plus a prioritized improvement backlog.

**Scope boundary:** The Markdown files define AI procedures, prompts, decision gates, and outputs. Actual file conversion, financial model creation, and PPTX edits may require Excel/Python or connected tools. Do not promise automated booking, tax filing, or ERP posting in the MVP.

## 2. Build timetable

| Date | Focus | Time budget | Minimum task set | End-of-day deliverable |
|---|---|---:|---|---|
| **Mon Nov 2** | Architecture and shared standards | **3 h** | Define users, supported inputs/outputs, sample company, reusable `.md` structure, data provenance, human approval rules, and acceptance criteria. | `README.md`, `shared/controls.md`, `shared/data_contract.md`, sample dataset inventory |
| **Tue Nov 3** | **01 — Accounting support** | **4 h** | Draft IFRS vs U.S. GAAP workflow; account mapping; proposed journal entries; debit/credit balancing; evidence references; standards differences; reviewer handoff. | `skills/01_accounting.md` + 3 worked entry cases |
| **Wed Nov 4** | **02 — Tax support** | **4 h** | Choose one demonstration jurisdiction, entity type, tax year, and form; map source documents to form fields; record assumptions, missing items, and CPA review questions. | `skills/02_tax.md` + draft working-paper checklist and one sample case |
| **Thu Nov 5** | **03 — FP&A** | **4 h** | Convert business vision into measurable objectives, KPIs, assumptions, model drivers, revenue/cost/cash-flow forecasts, and base/bull/bear scenarios. | `skills/03_fpa.md` + example driver-based model |
| **Fri Nov 6** | **04 — Format alignment** | **4 h** | Define CSV/XLSX/PDF/source-to-ERP mapping rules; normalize dates, account IDs, signs, currencies, mandatory fields and duplicates; create exception report. | `skills/04_format_alignment.md` + a sample ERP-ready import file and rejected-rows report |
| **Sat Nov 7** | **05 — PPT updates; 06 — Strategic reporting** | **6 h** | Apply updated figures to a provided PPTX template, preserve layouts, chart styles and as-of dates; build a reporting workflow linking employee activity to corporate priorities and KPIs. | `skills/05_ppt_update.md`, `skills/06_reporting.md`, updated sample deck, reporting sample |
| **Sun Nov 8** | Integration, quality assurance, review | **5 h** | Run end-to-end demo; test each workflow; compare figures across exports; document exceptions and unresolved risks; prepare review deck and next-step decisions. | `tests/acceptance_tests.md`, demo package, review notes, backlog, version `v0.1` |

**Total estimated focused work: 30 hours.** These are suggested work blocks; adjust around classes and other commitments without changing the Sunday review gate.

### Daily completion rule

Do not finish a day with just a prompt draft. Each `.md` workflow must include at least **one realistic worked example**, expected output format, validation steps, failure/escalation rules, and named reviewer role.

## 3. The six workflows and acceptance criteria

### 01 — Accounting support: IFRS and U.S. GAAP

**Inputs:** Transaction narrative, date, entity, currency, source evidence, chart of accounts, reporting framework, accounting period.  
**Outputs:** Proposed journals with explanations, standard-specific treatment, account mapping, and an approval-ready posting file or journal schedule.

**Checks:**
- Every entry balances (total debits = total credits).
- Distinguish IFRS and U.S. GAAP treatments where a difference is material; do not assume rules are interchangeable.
- Flag unsupported accounts, insufficient evidence, uncertain recognition/measurement, tax-vs-book differences, and periods that may be closed.
- Do not auto-post: an authorized accountant approves first.

**Demo cases:** Routine accrual, prepaid expense, and one treatment-sensitive case requiring separate IFRS/U.S. GAAP analysis.

### 02 — Tax preparation support for CPA review

**Inputs:** Country/state, tax year, entity type, form selection, trial balance, tax support schedules, supporting documents.  
**Outputs:** Source-to-form mapping, populated draft/working paper where appropriate, missing-document list, calculations, assumptions, and CPA review questions.

**Checks:**
- Require the user to identify the relevant jurisdiction, entity type, tax year, and form; the demo can use **one U.S. federal business return type** rather than claiming universal tax coverage.
- Tie calculations to source evidence, mark unknown fields explicitly, and keep tax adjustments separate from book results.
- Confirm the tax form version and instructions for the year before any real client engagement.
- **No final filing or legal/tax conclusion without qualified professional review.**

### 03 — FP&A: corporate vision to a financial model

**Inputs:** Company vision, strategic objectives, operating metrics, actual results, assumptions, time horizon, headcount/capacity data.  
**Outputs:** Strategy-to-KPI map; driver-based P&L, cash-flow and relevant balance-sheet forecasts; scenario and sensitivity tables; decision summary.

**Checks:**
- Each strategic objective maps to an owner, metric, baseline, target, timing, and model driver.
- Separate historical actuals, business assumptions, formulas, and forecasts.
- Check linked calculations and sensitivity logic; reconcile starting balances to actuals.

**Demo:** A 12-month plan showing revenue growth, gross margin, hiring, operating costs and cash runway under three scenarios.

### 04 — Format alignment for accounting/ERP systems

**Inputs:** Source exports (CSV/XLSX, and PDF when reliable extraction is possible), target schema, field definitions, lookup tables.  
**Outputs:** System-ready import file, mapping dictionary, error/exception report, source-to-target reconciliation.

**Checks:**
- Validate required columns, accepted data types, encoding, dates, number signs, currency, account codes, duplicates and allowed values.
- Preserve source IDs and document every transformation.
- Reconcile source row counts and amounts to accepted + rejected records; never quietly drop exceptions.
- Treat scanned PDFs and ambiguous extraction as manual-review cases rather than guessing.

### 05 — PowerPoint update from current data and template

**Inputs:** Existing editable `.pptx` template, new data/model, reporting date, source list, update instructions.  
**Outputs:** Updated `.pptx`, data refresh log, changed-slide inventory, source references and visual QA notes.

**Checks:**
- Preserve master/layouts, typography, brand colors and slide order unless change is requested.
- Verify that charts/tables agree with source figures and dates; do not simply update text labels while retaining old chart values.
- Check overflow, broken objects, mislabeled units and stale commentary.

### 06 — Reporting: employee work to corporate strategy

**Inputs:** Corporate vision, priorities, department plans, employee activities, deliverables, KPI definitions, actuals, evidence.  
**Outputs:** Weekly/monthly strategy-alignment report: activities → outcomes → KPI movement → strategic contribution → risks → next actions.

**Checks:**
- Distinguish completed activity from measured business outcomes.
- Show evidence, accountable owner, time period, progress status, and blockers.
- Explicitly flag work that cannot yet be linked to a strategic goal; never fabricate impact.

## 4. Shared `.md` workflow structure

Every skill should use the same headings, making later client customization cheaper:

```markdown
# Skill name
## Purpose and supported scope
## Inputs and required documents
## Output files and schemas
## Workflow / decision steps
## Assumptions and source hierarchy
## Validation and reconciliation controls
## Exception handling and escalation
## Human review and approval gate
## Worked example (input → output)
## Acceptance tests
## Version history
```

Recommended shared metadata in each file: **skill ID, version, owner, last review date, accounting/tax jurisdiction (where applicable), reporting period, source as-of date, reviewer, and output version.**

## 5. Suggested repository structure

```text
AI-for-Finance-Department/
├── README.md
├── skills/
│   ├── 01_accounting.md
│   ├── 02_tax.md
│   ├── 03_fpa.md
│   ├── 04_format_alignment.md
│   ├── 05_ppt_update.md
│   └── 06_reporting.md
├── shared/
│   ├── controls.md
│   ├── data_contract.md
│   └── review_rules.md
├── examples/
│   ├── sample_company_brief.md
│   ├── sanitized_source_data/
│   ├── target_system_schema/
│   └── ppt_template/
├── tests/
│   ├── acceptance_tests.md
│   └── exception_cases.md
└── demo_outputs/
    ├── journals/
    ├── tax_workpapers/
    ├── models/
    ├── imports/
    ├── presentations/
    └── management_reports/
```

## 6. Sunday integrated demonstration

Use the **same fictional company** across modules to prove consistency:

1. Load its company strategy, source transactions, trial balance, operating assumptions, and presentation template.
2. **Accounting:** propose entries under the selected standard, mark uncertain cases, obtain mock approval.
3. **Format alignment:** map approved records to a simulated ERP import schema; inspect rejected rows and reconciliation.
4. **Tax:** prepare a separate, explicitly draft tax working paper for CPA review using relevant source balances and adjustments.
5. **FP&A:** connect actual financial figures and business objectives to a driver-based forecast.
6. **PPT:** refresh a monthly management deck using current model outputs and the provided template.
7. **Reporting:** link department/employee actions to company goals, KPIs and next decisions.

**Pass criteria for v0.1:**
- Six `.md` files exist and each has at least one passed example and one negative/exception test.
- Proposed journals balance; unresolved standard choices are disclosed rather than silently guessed.
- ERP output has zero unreported dropped rows, and source/target totals reconcile with documented exceptions.
- FP&A calculations tie to source actuals and internally consistent scenario assumptions.
- Presentation figures match the same model/export version and pass visual inspection.
- Tax fields are evidence-linked and flagged for CPA approval; nothing is submitted.
- Every final output has a source, reporting date, version and explicit reviewer status.

## 7. Priority management when time is tight

**Priority 0 (must ship for review):** All six documented workflows, one example each, source tracking, human approval controls, one connected demo, and list of limitations.  
**Priority 1 (next iteration):** Robust automation scripts, additional accounting scenarios, multiple tax forms/jurisdictions, connector integrations, automatic model checks, PPT batch refresh, dashboarding.  
**Not in this one-week MVP:** Live ERP write-back, production tax submission, unsupervised statutory reporting, or a universal multi-country compliance engine.

## 8. What to collect after Sunday for each client

Keep the six core workflows unchanged where possible. Add a **client configuration pack** containing:

| Client information | Customization target |
|---|---|
| Country, entities, fiscal calendar and reporting framework | Accounting and tax logic |
| Chart of accounts, journal policy, approval thresholds | Accounting controls |
| Tax jurisdictions, entity classification, forms, advisors | Tax working papers |
| ERP name, import schema and source exports | Format alignment rules |
| Strategic objectives, KPI definitions, forecast drivers | FP&A and reporting |
| Brand PPTX and preferred management reporting format | Slide and report templates |
| User roles, permissions, retention/privacy requirements | Review gates and access policy |

**Client onboarding sequence:** discovery → collect sanitized representative files and reference templates → configure mapping and assumptions → run a controlled pilot → accountant/CPA/finance manager acceptance → deploy with logging and ongoing review. Do not use confidential client data in uncontrolled demos.

## 9. Sunday review agenda (45–60 minutes)

| Time | Review segment |
|---:|---|
| 5 min | Project purpose, six use cases, intended users |
| 15 min | Live demo: source data → accounting/formatting → forecast |
| 10 min | Tax review workflow and professional sign-off controls |
| 10 min | Refreshed management PPT and vision-alignment report |
| 10 min | Quality scorecard, exceptions, security, risks |
| 5–10 min | Agree next iteration and first client pilot |

**Decision requested at review:** Is v0.1 sufficiently accurate, traceable, and reusable to justify a **single-client pilot**, or which critical controls must be fixed first?
