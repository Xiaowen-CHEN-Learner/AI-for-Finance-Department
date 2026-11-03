# Strategic Reporting — Employee Work to Corporate Strategy

| Metadata | Value |
|---|---|
| Project | AI for Finance Department |
| Skill ID | 06_reporting |
| Version | v0.1 — reusable MVP workflow |
| Suggested repository path | `skills/06_reporting.md` |
| Process owner | Finance Transformation Lead / FP&A Manager |
| Prepared on | 2026-11-02 |
| Last human review | Not yet reviewed |
| Reviewer roles | Department Manager; Finance Manager; Executive Sponsor for strategic decisions |
| Reporting period / source as-of date | Required for each run; no default to today's date |
| Output version | Required for each run, starting at v0.1 |
| Jurisdiction / accounting framework | Record the entity and basis of financial inputs when relevant; this module does not determine accounting or tax treatment |
| Workflow status | Draft for internal MVP review on 2026-11-08 |
| Basis | Attached `AI_for_Finance_Department_One_Week_MVP_Plan(4).md`, especially Module 06 and the shared workflow requirements |

## Purpose and supported scope

Turn a company's vision, priorities, department plans, and employee updates into an evidence-based weekly or monthly management report. Explain **what people did, what changed, how that supports strategy, what remains uncertain, and what management should do next**.

Use this reporting chain:

**Activity → deliverable → observed outcome → KPI movement → strategic contribution → risks → next action.**

An incomplete chain is a valid finding. Explicitly identify missing evidence or an unconfirmed strategic link instead of inventing business impact.

### Supported work

- Translate approved corporate priorities into a strategy-to-KPI map.
- Consolidate department and employee activity updates into an alignment register.
- Compare actual results with approved targets and comparable prior periods.
- Explain financial and operational implications using documented evidence.
- Identify blockers, duplicated work, unsupported claims, and activities whose strategic link needs clarification.
- Prepare management commentary, an action register, a decision log, and a reviewer handoff.
- Supply approved reporting content to Module 05 for presentation updates.

### MVP boundaries

This Markdown file defines a workflow; it does not itself connect to systems, calculate a live dashboard, change a forecast, update a PPTX, or distribute a report. Use available calculation and file tools when running it, and state any execution limitation.

Use reporting for operational decisions and team coordination. Do not infer individual competence or rank employees from task counts, hours, or incomplete work logs. Describe documented contributions and dependencies. Personnel decisions require the organization's separate review process.

Keep client details in a configuration pack. Reuse the core workflow across clients. The worked example below uses fictional data and must be replaced with the project's agreed sample company for the integrated demonstration.

## Inputs and required documents

### Required inputs

| Input | Minimum content | Missing-input behavior |
|---|---|---|
| Corporate vision and priorities | Approved wording, strategy version, effective dates, sponsor | Draft proposed interpretations only; do not claim confirmed strategic alignment |
| Reporting scope | Entity, departments, audience, period, cutoff, cadence, currency, units, timezone | Request the missing field before finalizing affected comparisons |
| Department plans | Initiatives, expected deliverables, owners, milestones, dependencies | Show activity-level reporting; flag the missing plan |
| Employee / team updates | Activity ID, owner, dates, work performed, deliverable, status, blockers, evidence references | Retain incomplete records with explicit unknowns |
| KPI dictionary | Definition, formula, scope, direction, baseline, target, target date, owner, source, status thresholds | Do not invent targets or calculate a status using an undefined metric |
| Actual results | Values, periods, approved source version, source location, completeness status | Report missing or partial data; never replace it with a forecast |
| Evidence | Deliverable files, project records, reconciliations, operational records, finance schedules | Label unsupported updates as self-reported; do not present impact as verified |
| Review roles | Department reviewer, Finance reviewer, final approver | Prepare a draft with approval pending |

Optional inputs: the prior report, open actions, risk register, resource constraints, approved budgets, and the latest approved Module 03 forecast. Use an approved phased target for the report period when the strategic target is for a later date; otherwise show progress toward that future target without assigning a current target status.

### Client / run configuration

Complete this block for each engagement. `null` means unknown, not zero. Do not require a client to complete every optional field before producing a useful draft.

```yaml
client_id: null
company_name: null
entities: []
departments: []
audience: management
cadence: monthly                 # weekly or monthly
reporting_period_start: null     # YYYY-MM-DD
reporting_period_end: null
source_cutoff_at: null           # ISO 8601 timestamp, including timezone offset
timezone: null
fiscal_calendar: null
reporting_currency: null
display_units: null              # currency units / thousands / millions
financial_basis: null            # e.g., approved management accounts
strategy_version: null
approved_kpi_dictionary_version: null
actuals_version: null
fpa_model_version: null          # only if forecasts are used
prior_report_version: null
output_version: v0.1
confidentiality: internal
department_reviewer: null
finance_reviewer: null
executive_approver: null
decision_due_date: null
approved_status_rules: {}        # per KPI, in that KPI's own units
stale_data_rules: {}             # maximum age / required refresh by source
materiality_rules: {}            # client-approved reporting thresholds
shared_controls_version: null
shared_data_contract_version: null
shared_review_rules_version: null
```

Load `shared/controls.md`, `shared/data_contract.md`, and `shared/review_rules.md` if supplied. If unavailable, apply the controls in this file and disclose the missing shared dependencies; do not claim to have checked files that were not provided. Raise conflicts between shared controls and client configuration to the Finance Manager before issuing an affected final conclusion.

## Output files and schemas

The minimum deliverable is one review-ready Markdown report containing the registers below. Separate CSV files are optional exports when supported and useful. Filenames below are output specifications, not files already created by this workflow document.

### Output package

| File | Required content |
|---|---|
| `strategic_report_<period_end>_<version>.md` | Executive summary, objective scorecard, activity alignment, risks, actions, decision requests, evidence limitations, approvals |
| `alignment_register_<period_end>_<version>.csv` | Every in-scope activity, including work with unconfirmed alignment |
| `kpi_scorecard_<period_end>_<version>.csv` | Definitions, comparable actuals, targets, calculations, status and provenance |
| `action_decision_log_<period_end>_<version>.csv` | Risks, blockers, next actions, decisions, accountable owners and dates |
| `evidence_register_<period_end>_<version>.csv` | Source IDs, locations, versions, periods, verification status and linked claims |
| `review_log_<period_end>_<version>.md` | Checks performed, exceptions, changes from prior version and human sign-offs |

Use UTF-8 for CSV exports, ISO dates, stable text IDs, and numeric values without currency symbols or thousands separators. Preserve leading zeros in IDs. Store percentages in percentage units (`38.5` for 38.5%) and label the unit `%`; store changes in those values as percentage points (`pp`). Preserve unrounded values for calculations and round only displayed results. Quote CSV fields containing commas or newlines.

### Core schemas

| Register | Required fields |
|---|---|
| Strategy map | `objective_id`, `approved_objective`, `strategy_version`, `objective_owner`, `department`, `initiative_id`, `kpi_ids`, `baseline_period`, `target_period`, `source_ids` |
| Activity alignment | `activity_id`, `period_start`, `period_end`, `department`, `activity_owner`, `activity`, `deliverable`, `activity_status`, `objective_id`, `alignment_status`, `expected_mechanism`, `observed_outcome`, `kpi_ids`, `contribution_basis`, `evidence_ids`, `blocker`, `next_action_id` |
| KPI scorecard | `kpi_id`, `definition`, `formula`, `scope`, `direction`, `unit`, `baseline_value`, `baseline_period`, `prior_value`, `prior_period`, `actual_value`, `actual_period`, `target_value`, `target_period`, `actual_minus_prior`, `actual_minus_target`, `status`, `evidence_status`, `source_ids`, `source_version`, `source_as_of`, `kpi_owner` |
| Actions / decisions | `record_id`, `record_type`, `linked_objective_ids`, `linked_activity_ids`, `issue_or_request`, `business_implication`, `proposed_action_or_options`, `owner`, `approver`, `due_date`, `status`, `dependency`, `closure_evidence_ids` |
| Evidence | `evidence_id`, `source_name`, `source_location`, `source_version`, `covered_period`, `source_as_of`, `source_owner`, `verification_status`, `limitations`, `linked_record_ids` |
| Review log | `check_id`, `check_description`, `result`, `exception_id`, `reviewer_role`, `reviewer_name`, `reviewed_at`, `decision`, `output_version` |

Allow a null `objective_id` or `kpi_ids` where a link is unknown, accompanied by an exception and next action. Missing required context is an explicit null plus an explanation, not a fabricated value. If a task contributes to multiple goals, use mapping rows with the same activity ID; retain one canonical activity record and do not count its hours, spend, or benefits more than once.

### Management report template

```markdown
# Strategic Alignment Report — [Company] — [Period]

Reporting scope: [entities / departments]
Reporting period: [start–end] | Source cutoff: [timestamp]
Strategy / actuals / forecast versions: [versions or N/A]
Report version: [version] | Status: Draft — pending review
Prepared by: [name/role] | Reviewers: [names/roles]
Currency / units / financial basis: [values]

## Executive summary
- Result: [most material measured result, with evidence ID]
- Strategic implication: [supported interpretation and uncertainty]
- Priority risk: [risk, owner and impact]
- Decision requested: [choice, decision owner and due date]

## Strategy and KPI scorecard
[Objective | KPI | Prior | Actual | Target | Change | Gap | Status | Source]

## Employee and department contribution
[Owner | Activity / deliverable | Observed outcome | Goal / KPI link | Evidence | Limitation]

## Work requiring alignment clarification
[Activity | Why linkage is unconfirmed | Clarification owner | Next action]

## Risks, blockers and next-period actions
[Issue | Business implication | Action | Owner | Due | Dependency]

## Decisions required
[Decision | Options / tradeoffs | Recommendation | Approver | Due]

## Evidence, assumptions and limitations
[Sources, missing data, untested assumptions, forecasts, attribution limits]

## Review and approval
[Checks completed | Open exceptions | Department review | Finance review | Final approval]
```

## Workflow / decision steps

### Step 1 — Establish scope and source versions

1. Read the supplied configuration, strategy, KPI definitions, activity logs and evidence.
2. Confirm the reporting period, organizational scope, cutoff, units and audience.
3. Assign stable source IDs and record file/sheet/cell, page, ticket, or other locators sufficiently precise for review.
4. Identify draft versus approved sources. Freeze the selected input versions for the run.
5. Log missing or stale inputs. Continue unaffected sections; hold affected conclusions.

### Step 2 — Convert vision into a strategy map

For each approved priority, record its objective ID, intended outcome, accountable owner, timeframe, KPI, baseline and target. Explain how the department's work is expected to influence the KPI. Keep proposed interpretations separately marked for sponsor review.

Example mechanism: **standardize month-end reconciliations → reduce rework → complete reconciliations earlier → shorten the close → give management timely information**. This is a proposed causal pathway until outcome evidence supports it.

Do not retrofit every activity to an objective. Classify alignment as:

- **Direct:** an explicit, evidenced link to an approved goal and KPI.
- **Enabling:** work that supports an initiative, control or prerequisite, with an explained mechanism.
- **Unconfirmed:** a plausible or absent link that needs owner clarification.

Required control or maintenance work can be enabling even when it produces no revenue. Absence of a KPI link is not proof that work is unnecessary.

### Step 3 — Normalize activity updates

Separate each update into activity, deliverable, completion evidence, observed outcome, possible strategic contribution, blockers and next action. Use activity statuses `not_started`, `in_progress`, `completed`, `blocked`, or `cancelled`.

“Prepared a pricing analysis” is a completed deliverable. “Improved gross margin” is an outcome claim requiring actual results. “Could improve gross margin” is an expectation or forecast, not an observed result.

Keep self-reported completion visible as such until validated. Deduplicate records by activity ID and source evidence. Preserve legitimate recurring work in different periods.

### Step 4 — Calculate KPI movement and target gaps

Use an approved definition and comparable populations, periods, currencies and units. Show actuals, budgets, targets and forecasts in separate fields.

```text
Absolute movement = current actual − comparable prior actual
Target gap = current actual − target for the same reporting period
Relative movement (%) = (current actual / prior actual − 1) × 100
```

Calculate relative movement only when the prior value is positive and the ratio is meaningful. Otherwise show the absolute movement and explain why the relative percentage is not meaningful. For rates expressed in percentage units, show absolute movement and target gap in percentage points.

For direction `higher_is_better`, a positive target gap is favorable. For `lower_is_better`, a negative target gap is favorable. For `target_range`, use the approved lower/upper bounds; improvement means moving toward the range, not automatically increasing or decreasing.

Calculate aggregate ratios from their underlying totals, such as total gross profit divided by total revenue. Do not average department percentages without the appropriate denominator weights. Do not combine currencies without an approved conversion method, rate source and period.

### Step 5 — Assign performance and evidence status separately

Performance status uses client-approved rules for the reporting period:

| Status | Rule |
|---|---|
| Green | Actual meets or exceeds a direction-specific target, or lies within the approved target range |
| Amber | Actual misses the target but falls within its approved amber tolerance |
| Red | Actual misses the target beyond that tolerance |
| Unknown | Missing definition, actual, comparable target, threshold, or sufficiently current evidence prevents classification |

Apply tolerance in the KPI's native units, such as days, count, currency or percentage points. Do not invent a universal 5% rule. Never assign Green from a forecast or a completed-task count when the KPI measures a business outcome.

Evidence status is independent: `validated`, `self_reported`, `missing`, `stale`, or `conflicting`. “Validated” means reconciled to the selected source under this workflow, not independently audited or causally proven.

For an objective with several required KPIs, use the approved rollup rule. If none is supplied, show KPI-level statuses without an overall color. Any missing required KPI must remain visible; do not average colors or let an activity-completion rate override outcome evidence.

### Step 6 — Assess contribution without overstating causality

For each material claim, answer:

1. What happened, and what evidence supports it?
2. What KPI moved over a comparable period?
3. What mechanism connects the work to the result?
4. What other factors could explain the movement?
5. What can be concluded now, and what remains unmeasured?

Use `observed_association`, `plausible_contribution`, `forecast_only`, `not_measured`, or `attribution_supported` for contribution basis. Use `attribution_supported` only when evidence supports an incremental effect, such as a well-defined comparison or experiment, and state limitations. A budget variance bridge explains arithmetic; it does not by itself establish employee causality.

Keep these benefits distinct:

- **Realized financial benefit:** an evidenced reduction in expenditure or increase in relevant earnings/cash, with period and baseline stated.
- **Released capacity:** time made available for other work; do not call this cash savings without evidence of an actual spending reduction.
- **Estimated / forecast benefit:** assumptions or modeled future impact, clearly labeled and linked to the model version.

Do not sum overlapping benefits from several teams. Identify a shared benefit once, with contributing teams and any approved allocation method.

### Step 7 — Build management commentary and decision requests

Lead with the most material result or risk. For each key finding, write **result → strategic meaning → evidence / limitation → recommended action**. Keep the executive summary to approximately 150–250 words unless the audience requests another format.

Each action needs one accountable owner, a due date, a linked issue and a closure criterion. If a date or owner is only proposed, label it proposed. Each decision needs an approver, available options, tradeoffs and a decision deadline. Clearly separate recommendations from approved decisions.

### Step 8 — Reconcile, review and hand off

Run the controls below, resolve material exceptions, and record remaining limitations. Include previous open actions until they are closed with evidence, cancelled with a reason, or explicitly carried forward.

| Integration | Handoff rule |
|---|---|
| Module 01 — Accounting | Use approved actuals and evidence references; do not create or post correcting entries from this report |
| Module 02 — Tax | Link relevant milestones and review status; do not turn a draft tax estimate into a final liability or strategic fact |
| Module 03 — FP&A | Reuse approved objective/KPI IDs and forecast version; label scenario data separately from actuals |
| Module 04 — Format alignment | Use accepted data plus the exception report; disclose excluded records and their effect on coverage |
| Module 05 — PPT update | Provide approved summary, KPI tables, units, dates, source IDs and report version; require slide figures to match the report |

Only mark a report approved when actual human approval is recorded. Prepare a report or handoff file within the requested scope; do not send it to employees, management, or external parties without authorization.

### Copy-and-use execution prompt

```text
Apply 06_reporting.md to the attached client configuration and source files.
Act as an FP&A and strategic reporting analyst preparing a management draft.

1. Identify the reporting period, source cutoff, strategy/KPI versions and gaps.
2. Build the strategy map and normalize all in-scope employee/team activities.
3. Link activities to deliverables, outcomes, KPIs and approved goals.
4. Keep activity completion, KPI performance, evidence quality and contribution
   claims separate. Mark unconfirmed alignment and missing impact evidence.
5. Calculate comparable KPI movements and target gaps; show formulas and sources.
6. Apply approved status rules only. Separate actuals, targets and forecasts.
7. Prepare the Markdown management report and embedded registers. Export CSVs
   only if requested or useful and tools support them.
8. Include decisions, blockers, owners, due dates, exceptions and reviewer status.
9. Run the validation controls and report what passed, failed or was not run.
10. Finish with a short handoff stating the main decision and outstanding reviews.

Do not invent numbers, targets, owners, evidence, impact, approvals or tool actions.
Do not treat capacity savings as cash savings or correlation as proven causality.
Use the supplied output naming convention and preserve traceability.
```

## Assumptions and source hierarchy

Use the best source for each type of claim, rather than one blanket hierarchy:

| Claim | Preferred source | Lower-confidence fallback |
|---|---|---|
| Strategic priority / target | Approved strategy and KPI dictionary effective for the period | Management draft, clearly marked proposed |
| Financial actual | Approved finance ledger or management report with reconciliation | Draft finance export, marked provisional |
| Operational result | Authoritative operational records with documented definitions | Manager-certified schedule or self-reported update |
| Completed deliverable | Accepted file, ticket, milestone or acceptance record | Employee statement, labeled self-reported |
| Forecast / expected benefit | Approved FP&A model and assumption register | Explicit draft estimate with assumptions |

If sources disagree, log the conflicting values and versions and request the relevant owner's resolution. Do not silently select the more favorable result. A newer timestamp alone does not establish approval or comparability.

Maintain an assumption register with assumption ID, statement, rationale, affected outputs, owner, confirmation status and expiry/review date. Do not present assumptions as source facts. External benchmarks are optional; if used, verify the source, date, definition and comparability and cite the original source. No external research is necessary for the synthetic example below.

## Validation and reconciliation controls

- **Coverage:** Every unique in-scope activity appears in the register, including unconfirmed and cancelled work. Reconcile received records = unique included records + excluded/out-of-scope records + duplicate records; keep an exclusion log. Check multi-goal mapping rows separately.
- **Strategic traceability:** Every confirmed goal link uses an approved objective ID. Unconfirmed links carry a reason and an action owner.
- **Evidence:** Every material numeric or outcome claim has a source ID and precise locator. Check the source period, cutoff, version, status and limitations.
- **Metric integrity:** Check formula, units, signs, denominator, currency, period, scope, rounding and KPI direction. Report division-by-zero and noncomparable data explicitly.
- **Financial reconciliation:** Tie totals and ratios to the same approved actuals version used by Module 03 and the presentation. Document any reconciliation difference before release.
- **Status logic:** Recalculate statuses from the approved rules. Task completion, actual performance, evidence quality and forecast expectations remain distinct.
- **Attribution and benefits:** Review unsupported causal wording, overlapping benefits and cash-versus-capacity claims. Shared outcomes are not credited in full to each employee.
- **Actions:** Every material issue has an accountable role/person, a confirmed or proposed due date and a closure criterion. Prior-period open actions are retained or explicitly resolved.
- **Privacy:** Include only work information needed by the audience. Use role labels or anonymized identifiers for demos and omit unnecessary personal or customer details.
- **Version consistency:** The report, exports and slide handoff share reporting dates, selected input versions and output version. Log changed conclusions when a source is revised.
- **Review status:** No human reviewer, sign-off, acceptance test or system action is marked complete without evidence that it occurred.

For each control, record `pass`, `fail`, or `not_run`, with the reason. A draft may contain visible exceptions; a final management conclusion cannot silently depend on a failed material control.

## Exception handling and escalation

| Exception | Reporting treatment | Reviewer / next step |
|---|---|---|
| Vision is too broad or no approved priorities exist | Draft a proposed map; mark alignment unconfirmed | Executive Sponsor confirms objectives |
| Task has no credible strategic link | Keep it in the unconfirmed-work section; do not label it waste | Department Manager clarifies rationale or proposes reprioritization |
| Completed task has no measured outcome | Report completion only; outcome remains not measured | Activity/KPI owner defines follow-up measurement |
| Actual, target, formula or threshold is missing | Show the available data; affected performance status is Unknown | KPI owner supplies approved definition/data |
| Target is annual but actual is monthly | Use an approved monthly milestone if available; otherwise no monthly target status | FP&A confirms phasing |
| Evidence is stale, conflicting or after cutoff | Flag the limitation; separate subsequent information from period results | Source owner and Finance Manager resolve |
| Source totals do not reconcile | Hold the affected number and conclusion; continue unaffected sections | Finance Manager resolves reconciliation |
| Duplicate / shared contribution | Preserve traceability; count work and benefits once | Department owners confirm attribution |
| Claimed savings only reflect fewer work hours | Reclassify as released capacity unless spending reduction is evidenced | Finance Manager validates benefit category |
| Required tool or source is unavailable | Identify the operation not performed; provide a manual handoff | Process owner supplies access or completes the check |
| New source arrives after review | Create a revised draft and change log; reassess affected approvals | Finance reviewer reapproves affected content |

Escalate only the blocked decision or unsupported conclusion. Do not fabricate missing data to make the package appear complete.

## Human review and approval gate

| Role | Review responsibility | Evidence of completion |
|---|---|---|
| Employee / activity owner | Factual accuracy of their updates and source references | Confirmed update or correction record |
| Department Manager | Deliverable acceptance, alignment, blockers, accountable actions | Review comments and sign-off for department scope |
| KPI owner / Finance Manager | Metric definitions, reconciliations, targets, status, financial claims and benefit categories | Completed control log and recorded approval |
| Executive Sponsor / delegated approver | Strategic interpretation, resource choices and material decisions | Decision log and final approval where required |

Report lifecycle: **Draft → In review → Changes requested / Approved**. Use **Superseded** for replaced approved versions. Keep unresolved limitations visible in approved reports if the designated approver explicitly accepts them; do not imply missing evidence has been validated.

The AI prepares and checks the package. Human reviewers approve facts and management decisions. For the MVP demonstration, simulated approvals must be labeled simulated and cannot authorize real distribution or system changes.

## Worked example (input → output)

### A. Fictional inputs

**Company:** Harbor Operations Co. — synthetic placeholder for the common demo company.  
**Vision:** Grow profitably while giving management timely, reliable information.  
**Reporting period:** September 1–30, 2026; comparison August 1–31, 2026.  
**Source cutoff:** October 9, 2026, 17:00 America/New_York.  
**Currency / units:** USD, whole currency units; rates shown as percentages.  
**Output:** v0.1, Draft — pending human review.

This is a retrospective September example; the October 9 cutoff allows the month-end close to be completed before reporting. All source IDs, records, owners and values in this example are fictional. They illustrate expected behavior; they are not actual attached datasets or approvals.

| Evidence ID | Illustrative source / locator | Version and coverage | Limitation |
|---|---|---|---|
| E01 | Strategy register, objectives O1–O3 and KPI rules K1–K3 | Strategy v1.0; September targets | Fictional approved inputs for the scenario only |
| E02 | Management accounts, P&L revenue / COGS rows | Actuals v1.0; August and September | Synthetic management figures |
| E03 | Close calendar, period completion dates | Calendar v1.0; August and September | Business-day convention held constant |
| E04 | Reconciliation tracker, September cohort of 15 items | Tracker v1.0; September 30 snapshot and August backlog | Unresolved items are all overdue in this example |
| E05 | Accepted deliverables A01–A03 and update A04 | Activity log v1.0; September | Cannot establish individual causal impact |
| E06 | Time estimate, 12 hours/week released; USD 50/hour assumed | Estimate v0.1; September | Self-reported estimate; no expense reduction evidence |

| Objective | KPI / direction | August actual | September target | Approved synthetic status rule |
|---|---|---:|---:|---|
| O1 — Improve profitable growth | K1 Gross margin; higher is better | 37.0% | 40.0% | Green ≥40%; Amber ≥38% and <40%; Red <38% |
| O2 — Provide timely management information | K2 Close duration in business days; lower is better | 8 | 6 | Green ≤6; Amber >6 and ≤7; Red >7 |
| O3 — Strengthen financial information reliability | K3 Overdue reconciliations at month-end; lower is better | 5 | 2 | Green ≤2; Amber =3; Red ≥4 |

Financial inputs from E02:

| Metric | August | September |
|---|---:|---:|
| Revenue | 900,000 | 1,000,000 |
| Cost of goods sold | 567,000 | 615,000 |
| Gross profit | 333,000 | 385,000 |

Operational inputs: the September close took 6 business days (E03). Of a defined cohort of 15 reconciliations scheduled for resolution, 12 were completed and 3 remained unresolved and overdue at month-end (E04). No additional overdue items existed in the synthetic snapshot. This cohort completion measure is separate from the total backlog KPI.

### B. Expected activity alignment register

| ID / owner | Activity and status | Deliverable / observed outcome | Goal / KPI link | Contribution basis and limitation |
|---|---|---|---|---|
| A01 — Reporting Analyst | Standardized close checklist; completed | Accepted checklist (E05); close duration fell from 8 to 6 days (E03) | O2 / K2; enabling | Plausible contribution; staffing, workload and other process changes have not been isolated |
| A02 — FP&A Analyst | Prepared pricing and product-mix analysis; completed | Analysis accepted (E05); implementation has not started | O1 / K1; enabling | Forecast-only pathway; September margin improvement cannot be attributed to an unimplemented proposal |
| A03 — Accounting Team Lead | Resolved reconciliations; in progress | 12 of 15 completed; 3 overdue remain (E04) | O3 / K3; direct | Observed work completion and lower backlog; unresolved balances still require review |
| A04 — Finance Analyst | Redesigned dashboard colors; self-reported completed | Updated design reported (E05); no user testing or decision-use evidence | Unconfirmed | Outcome not measured; ask the manager whether readability/accessibility or another approved need justified the work |

### C. Expected KPI scorecard

| KPI | August actual | September actual | September target | Movement | Actual − target | Status | Source |
|---|---:|---:|---:|---:|---:|---|---|
| Gross margin | 37.0% | 38.5% | 40.0% | +1.5 pp | −1.5 pp | Amber | E01, E02 |
| Close duration | 8 days | 6 days | 6 days | −2 days | 0 days | Green | E01, E03 |
| Overdue reconciliations | 5 | 3 | 2 | −2 | +1 | Amber | E01, E04 |

Expected calculations:

```text
August gross profit = 900,000 − 567,000 = USD 333,000
September gross profit = 1,000,000 − 615,000 = USD 385,000
August gross margin = 333,000 / 900,000 × 100 = 37.0%
September gross margin = 385,000 / 1,000,000 × 100 = 38.5%
Gross margin movement = 38.5% − 37.0% = +1.5 percentage points
September margin target gap = 38.5% − 40.0% = −1.5 percentage points
Gross profit increase = 385,000 − 333,000 = USD 52,000

Arithmetic bridge (sequential method, not proof of causality):
Revenue effect at prior margin = (1,000,000 − 900,000) × 37% = USD 37,000
Margin effect at current revenue = 1,000,000 × (38.5% − 37%) = USD 15,000
Bridge total = 37,000 + 15,000 = USD 52,000

Close duration reduction = 8 − 6 = 2 business days
Relative close duration reduction = 2 / 8 × 100 = 25%
September reconciliation cohort completion = 12 / 15 × 100 = 80%
Estimated weekly capacity value = 12 hours × USD 50/hour = USD 600/week
```

The USD 600/week is an illustrative value of released capacity based on E06, not realized cash savings. No annualization or reduction in payroll expense is claimed. Do not combine it with the gross profit improvement as a total realized financial benefit.

### D. Expected management commentary

> September performance improved across all three monitored KPIs, although profitable growth and reconciliation reliability remained below target. Gross margin increased from 37.0% to 38.5%, and gross profit increased by USD 52,000; the margin remains 1.5 percentage points below the 40.0% target (E01–E02). The arithmetic bridge associates USD 37,000 of the gross profit increase with higher revenue at the prior margin and USD 15,000 with the margin change at current revenue. It does not identify the employees or actions that caused those changes.
>
> Close duration improved from eight to six business days and met its target (E01, E03). The standardized checklist plausibly supported the result, but the contribution of other factors has not been isolated. The reconciliation team completed 12 of 15 scheduled items; three overdue items remain against a target of no more than two (E04).
>
> Management should prioritize resolving those three items and deciding whether to authorize a measured pricing pilot. The pricing analysis is complete, but implementation and financial benefit have not yet been demonstrated. The dashboard redesign requires clarification of its intended business outcome. Human review and approval remain pending.

### E. Expected actions and decisions

All dates below are proposed demonstration dates, not actual commitments.

| ID / type | Action or decision | Accountable owner / approver | Proposed due | Closure criterion |
|---|---|---|---|---|
| N01 — Action | Resolve or document a remediation plan for the three overdue reconciliations | Accounting Team Lead / Controller | 2026-10-16 | Tracker and balance evidence show resolution or an approved plan for every item |
| D01 — Decision | Authorize a limited pricing pilot, revise it, or defer it; weigh margin potential against volume risk | Commercial Lead / CFO | 2026-10-16 | Decision recorded with pilot scope, measurement approach and guardrails if approved |
| N02 — Action | Confirm the dashboard redesign's strategic or usability requirement | Finance Analyst / Department Manager | 2026-10-15 | Objective or enabling requirement documented, or reprioritization agreed |
| N03 — Action | Validate the claimed released hours and how capacity is used | Reporting Analyst / Finance Manager | 2026-10-16 | Before/after work samples and redeployment evidence; benefit category confirmed |

Example checks: 4 received activity records = 4 unique included + 0 excluded + 0 duplicates; 3 activities have confirmed direct/enabling alignment and 1 remains unconfirmed. The 12/15 cohort completion rate does not override K3's Amber backlog status. Numerical expected results can be checked independently; human approvals and real source verification have not occurred.

### F. Negative example

**Input:** “The new dashboard saved USD 20,000,” with no baseline, source, period or calculation.

**Expected treatment:** Retain the dashboard activity; label the savings claim unsupported, exclude USD 20,000 from realized-benefit totals, request evidence from the activity owner, and record Finance review pending. Do not silently replace the number with an estimate or label the employee's work unsuccessful.

## Acceptance tests

These are test specifications for the November 8 MVP review. They are not a claim that a live reporting system or client dataset has passed testing. Record actual result, pass/fail/not-run, run date, evidence and reviewer when executing them.

| Test | Input / condition | Expected result |
|---|---|---|
| AT01 — Worked example calculations | Synthetic E02–E04 values above | Gross margin 38.5%; movement +1.5 pp; gap −1.5 pp; gross profit bridge USD 52,000; close reduction 25%; cohort completion 80% |
| AT02 — Direction and status | K1 38.5%; K2 6 days; K3 3 overdue, with example rules | Amber / Green / Amber respectively; each tied to E01 rules |
| AT03 — Unsupported impact | Dashboard savings claim of USD 20,000 without evidence | Claim flagged; no realized savings recognized; evidence request logged |
| AT04 — Missing KPI definition / target | Activity complete but approved KPI definition or target absent | Completion shown; affected performance status Unknown |
| AT05 — Unconfirmed alignment | Activity has no approved strategic or enabling link | Record retained with clarification action; no invented goal or claim of waste |
| AT06 — Duplicate and shared benefit | Same activity appears in two updates and maps to two goals | Duplicate logged; one canonical activity and one benefit counted; both links preserved |
| AT07 — Incomparable data | Monthly actual versus annual target without phasing, or mixed currencies without rates | No unsupported comparison or combined total; exception escalated |
| AT08 — Forecast versus actual | Completed analysis predicts improvement, but implementation has not started | Forecast-only contribution; predicted outcome excluded from actual KPI results |
| AT09 — Capacity versus cash | 12 estimated hours/week × USD 50/hour | USD 600/week estimated capacity value; no cash savings claim |
| AT10 — Stale / conflicting source | Source exceeds freshness rule or approved reports conflict | Affected metric flagged; no automatic Green; owner resolution requested |
| AT11 — Boundary and zero cases | Values exactly at example thresholds; prior value zero | K1 38% Amber, 40% Green; K2 7 Amber; K3 2 Green, 4 Red; relative movement from zero marked not meaningful |
| AT12 — Human approval | Report calculations pass, but no reviewer has signed | Status remains Draft / In review; no invented sign-off or distribution |
| AT13 — Cross-module reconciliation | Report and PPT/FP&A contain different actuals versions | Mismatch flagged and affected release held until reconciled |
| AT14 — Coverage and continuity | Mix of duplicate, excluded and unconfirmed work; prior open actions | Counts reconcile; exclusions explained; unconfirmed work retained; open actions carried forward or resolved with evidence |

**MVP completion criteria:** At least the worked example and one negative case have recorded results; material calculations and sources reconcile; every strategic impact claim is supported or explicitly qualified; all activities and exceptions are accounted for; the report has dates, versions and explicit reviewer status. Production and client readiness require the configured pilot and human acceptance described in the project plan.

## Version history

| Version | Date | Changes | Review status |
|---|---|---|---|
| v0.1 | 2026-11-02 | Initial reusable strategic reporting workflow aligned to Module 06; input/output contracts, reporting prompt, KPI rules, evidence and approval controls, synthetic example and acceptance tests | Draft for internal review; no client deployment or human sign-off claimed |

For later client versions, record configuration changes separately from core workflow changes. Preserve prior approved reports and explain material restatements instead of silently overwriting earlier conclusions.
