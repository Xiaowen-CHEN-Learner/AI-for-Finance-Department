# Strategic Reporting — Finance Department Report to the Board

| Metadata | Value |
|---|---|
| Project | AI for Finance Department |
| Skill ID | 06_reporting |
| Version | v0.2 — reusable MVP workflow, board-meeting edition |
| Suggested repository path | `skills/06_reporting.md` |
| Process owner | CFO / Finance Transformation Lead (preparation delegated to FP&A Manager) |
| Prepared on | 2026-11-02 |
| Last human review | Not yet reviewed |
| Reviewer roles | FP&A Manager (preparer check); Controller; CFO (content sign-off); Board Secretary / Company Secretary (pack control); Audit or Finance Committee Chair (pre-read, where the charter requires it) |
| Primary audience | Board of Directors, or its Audit / Finance Committee |
| Secondary audience | Executive leadership team (management edition of the same registers) |
| Reporting period / source as-of date | Required for each run; no default to today's date |
| Board meeting date / pre-read deadline | Required for each run; the pack is frozen at the pre-read deadline |
| Output version | Required for each run, starting at v0.1 |
| Jurisdiction / accounting framework | Record the entity, basis of preparation and whether figures are audited, reviewed or management-only; this module does not determine accounting or tax treatment |
| Workflow status | Draft for internal MVP review on 2026-11-08 |
| Basis | `AI_for_Finance_Department_One_Week_MVP_Plan(4).md`, Module 06 and shared workflow requirements; v0.1 of this file |

## Purpose and supported scope

Produce the finance section of a board pack: an evidence-based report that tells directors **how the company performed against the plan the board approved, whether strategic priorities are on track, what the material risks are, and which decisions the board is being asked to make**.

The board does not manage the finance department. It oversees the company. The report therefore reports at the level of **strategy, initiative, financial result, risk and decision**, and keeps employee-level activity in the management edition and appendices. The underlying evidence chain is unchanged:

**Activity → deliverable → observed outcome → KPI movement → strategic contribution → risk → decision.**

For the board, the chain is read from the right: start with the decision or the material result, and trace back to evidence only as far as a director needs to be confident in it. An incomplete chain is a valid finding; disclose missing evidence or an unconfirmed strategic link instead of inventing business impact.

### Supported work

- Translate board-approved strategy, budget and KPI targets into a strategy-to-KPI map.
- Consolidate department and team updates into initiative-level progress with evidence.
- Compare actual results with budget, prior period, prior year and the latest approved outlook.
- Explain financial and operational implications in board-level language, with limitations stated.
- Classify every board item as **For decision**, **For discussion** or **For noting**.
- Track the status of prior board resolutions and action items until closed.
- Prepare the cover memo, finance report, draft resolutions, appendices and the Board Secretary handoff.
- Supply approved content to Module 05 for the board slide deck.

### MVP boundaries

This Markdown file defines a workflow; it does not itself connect to systems, calculate a live dashboard, change a forecast, update a PPTX or circulate a pack. Use available calculation and file tools when running it, and state any execution limitation.

Board material is used for oversight and decisions. Do not present individual employee performance, task counts or hours to the board. Describe initiatives, owners by role, outcomes and dependencies. Personnel matters follow the organization's separate governance and HR process.

Keep client details in a configuration pack. Reuse the core workflow across clients. The worked example below uses fictional data and must be replaced with the project's agreed sample company for the integrated demonstration.

## Board reporting principles

These principles govern every output of this module. They are checked in the controls section.

| Principle | What it means in practice |
|---|---|
| Decision-first | The cover memo states, in order, what the board must decide, what it should discuss and what it should note. Nothing the board is asked to decide appears only in an appendix. |
| Plan-anchored | Every result is compared with what the board approved: the budget, the strategic target and the last outlook presented to the board. "Better than last month" is not a board message on its own. |
| Materiality | Use board-approved materiality thresholds. Below threshold, report in a table without commentary. Above threshold, write commentary and name an accountable executive. |
| One version of the numbers | Figures in the cover memo, report, appendices, slides and any FP&A outlook agree to the same approved actuals version. A difference is a control failure, not a rounding note. |
| Forward view with basis | Forecasts, outlooks and expected benefits are labeled, linked to the approved model version, and never mixed into actual results. |
| Risk owned | Each material risk has an executive owner, a stated impact, the control or mitigation in place, and a trend (improving / stable / deteriorating). |
| Nothing assumed approved | The pack is a draft until the CFO signs off and the Board Secretary accepts it; board resolutions exist only once minuted. |
| Read in 20 minutes | Cover memo one page; finance report roughly six to twelve pages; everything else in appendices. Directors read the pack before the meeting, not during it. |
| Board-appropriate confidentiality | Mark the pack board-confidential. Where the company is listed or regulated, treat unpublished results as price-sensitive and apply the disclosure policy to circulation. |

## Inputs and required documents

### Required inputs

| Input | Minimum content | Missing-input behavior |
|---|---|---|
| Board-approved strategy and priorities | Approved wording, strategy version, effective dates, sponsoring executive, board approval date | Draft proposed interpretations only; mark alignment unconfirmed |
| Board-approved budget / annual plan | Revenue, margin, operating expense, capital, cash and headcount plan by month or quarter, approval reference | Compare with prior period and target only; state that no budget comparison is possible |
| Reporting scope | Entity or group, segments, audience, period, cutoff, cadence, currency, units, timezone, basis of preparation | Request the missing field before finalizing affected comparisons |
| Financial actuals | P&L, balance sheet highlights, cash flow, approved source version, reconciliation status, audit/review status | Report missing or partial data; never substitute a forecast |
| KPI dictionary | Definition, formula, scope, direction, baseline, target, target date, owner, source, status thresholds, board rollup rule | Do not invent targets or calculate a status using an undefined metric |
| Strategic initiative plans | Initiative ID, objective link, executive sponsor, milestones, budget, expected benefit, status | Report activity-level progress; flag the missing plan |
| Department / team updates | Activity ID, owner (role), dates, deliverable, status, blockers, evidence references | Retain incomplete records with explicit unknowns; roll up to initiative level for the board |
| Evidence | Management accounts, reconciliations, operational records, accepted deliverables, finance schedules | Label unsupported updates as self-reported; do not present impact as verified |
| Prior board materials | Previous finance report, minutes, resolutions, open action items, prior outlook presented | Note that continuity could not be checked; carry nothing forward as "closed" |
| Risk register and risk appetite statement | Material financial and strategic risks, owners, ratings, appetite thresholds | Report risks identified in this run only, labeled "not reconciled to the corporate risk register" |
| Board calendar and governance roles | Meeting date, pre-read deadline, committee, Board Secretary, CFO, delegation-of-authority limits | Hold the pack as an unscheduled draft |

Optional inputs: latest approved Module 03 forecast or full-year outlook, covenant and liquidity schedules, external audit status and management letter points, Module 02 tax provision status, external benchmarks (verified and cited), and the last investor or lender report where consistency matters.

Use an approved phased (monthly or quarterly) target for the reporting period when the strategic target is for a later date; otherwise show progress toward that future target without assigning a current target status.

### Client / run configuration

Complete this block for each engagement. `null` means unknown, not zero. Do not require a client to complete every optional field before producing a useful draft.

```yaml
client_id: null
company_name: null
entities: []
segments_or_departments: []
audience: board                     # board | audit_committee | finance_committee | management
listed_or_regulated: null           # true/false; drives disclosure and circulation controls
cadence: quarterly                  # monthly | quarterly, aligned to the board calendar
reporting_period_start: null        # YYYY-MM-DD
reporting_period_end: null
year_to_date_start: null
source_cutoff_at: null              # ISO 8601 timestamp, including timezone offset
board_meeting_date: null
pre_read_deadline: null             # pack frozen at this time
timezone: null
fiscal_calendar: null
reporting_currency: null
display_units: null                 # currency units / thousands / millions
financial_basis: null               # e.g., unaudited management accounts under IFRS/US GAAP
strategy_version: null
budget_version: null                # board-approved plan reference
approved_kpi_dictionary_version: null
actuals_version: null
fpa_model_version: null             # only if forecasts or outlook are used
prior_board_report_version: null
prior_minutes_reference: null
risk_register_version: null
output_version: v0.1
confidentiality: board-confidential
preparer: null
controller_reviewer: null
cfo_approver: null
board_secretary: null
committee_chair_prereview: null     # if the charter requires it
delegation_of_authority_reference: null
approved_status_rules: {}           # per KPI, in that KPI's own units
objective_rollup_rules: {}          # how KPI statuses roll up to an objective, if approved
board_materiality_rules: {}         # e.g., commentary required above X currency or Y pp vs budget
stale_data_rules: {}                # maximum age / required refresh by source
shared_controls_version: null
shared_data_contract_version: null
shared_review_rules_version: null
```

Load `shared/controls.md`, `shared/data_contract.md` and `shared/review_rules.md` if supplied. If unavailable, apply the controls in this file and disclose the missing shared dependencies; do not claim to have checked files that were not provided. Raise conflicts between shared controls and client configuration to the CFO before issuing an affected final conclusion.

## Output files and schemas

The minimum deliverable is one review-ready Markdown board pack containing the cover memo, finance report and appendices. Separate CSV exports are optional. Filenames below are output specifications, not files already created by this workflow document.

### Output package

| File | Required content |
|---|---|
| `board_finance_pack_<meeting_date>_<version>.md` | Cover memo; executive summary; financial performance; strategy and KPI scorecard; strategic initiatives; risks and controls; decisions required with draft resolutions; prior board actions; evidence, assumptions and limitations; approvals |
| `appendix_initiative_register_<period_end>_<version>.csv` | Every in-scope initiative and the activities rolled into it, including work with unconfirmed alignment (owners by role only) |
| `appendix_kpi_scorecard_<period_end>_<version>.csv` | Definitions, comparable actuals, budget, targets, calculations, status and provenance |
| `appendix_financial_summary_<period_end>_<version>.csv` | Period, YTD and full-year view: actual, budget, prior year, variance, outlook, source version |
| `board_action_decision_log_<meeting_date>_<version>.csv` | Decisions requested, prior resolutions, open actions, owners, due dates, status, closure evidence |
| `evidence_register_<period_end>_<version>.csv` | Source IDs, locators, versions, periods, verification status and linked claims |
| `review_log_<meeting_date>_<version>.md` | Checks performed, exceptions, changes from prior version, sign-offs and Board Secretary acceptance |
| `management_edition_<period_end>_<version>.md` | Optional: the department-level report (v0.1 template) from which the board pack was aggregated |

Use UTF-8 for CSV exports, ISO dates, stable text IDs, and numeric values without currency symbols or thousands separators. Preserve leading zeros in IDs. Store percentages in percentage units (`38.5` for 38.5%) and label the unit `%`; store changes in those values as percentage points (`pp`). Preserve unrounded values for calculations and round only displayed results. Quote CSV fields containing commas or newlines. Display negative variances consistently (parentheses or minus sign, never both in one pack) and state the convention once in the cover memo.

### Core schemas

| Register | Required fields |
|---|---|
| Strategy map | `objective_id`, `approved_objective`, `strategy_version`, `board_approval_ref`, `executive_sponsor`, `initiative_ids`, `kpi_ids`, `baseline_period`, `target_period`, `source_ids` |
| Initiative register | `initiative_id`, `objective_id`, `executive_sponsor`, `initiative`, `milestone_due`, `milestone_status`, `budget_value`, `spend_to_date`, `expected_benefit`, `benefit_basis`, `alignment_status`, `rolled_up_activity_ids`, `evidence_ids`, `blocker`, `board_item_type` |
| Activity alignment (appendix / management edition) | `activity_id`, `period_start`, `period_end`, `department`, `owner_role`, `activity`, `deliverable`, `activity_status`, `initiative_id`, `objective_id`, `alignment_status`, `expected_mechanism`, `observed_outcome`, `kpi_ids`, `contribution_basis`, `evidence_ids`, `blocker`, `next_action_id` |
| Financial summary | `line_id`, `line_item`, `period_actual`, `period_budget`, `period_prior_year`, `ytd_actual`, `ytd_budget`, `ytd_prior_year`, `fy_budget`, `fy_outlook`, `outlook_version`, `variance_vs_budget`, `variance_vs_budget_pct`, `materiality_flag`, `commentary_required`, `source_ids`, `source_version` |
| KPI scorecard | `kpi_id`, `definition`, `formula`, `scope`, `direction`, `unit`, `baseline_value`, `baseline_period`, `prior_value`, `prior_period`, `actual_value`, `actual_period`, `budget_value`, `target_value`, `target_period`, `actual_minus_prior`, `actual_minus_target`, `status`, `trend`, `evidence_status`, `source_ids`, `source_version`, `source_as_of`, `kpi_owner` |
| Board actions / decisions | `record_id`, `record_type` (`decision_requested`, `prior_resolution`, `action`, `risk`), `board_item_type` (`for_decision`, `for_discussion`, `for_noting`), `linked_objective_ids`, `linked_initiative_ids`, `issue_or_request`, `business_implication`, `options_and_tradeoffs`, `management_recommendation`, `draft_resolution`, `authority_level` (board / committee / management under DoA), `owner`, `approver`, `due_date`, `status`, `minutes_reference`, `closure_evidence_ids` |
| Risk | `risk_id`, `risk`, `category`, `executive_owner`, `impact`, `likelihood`, `rating`, `appetite_status` (within / near / outside), `trend`, `control_or_mitigation`, `linked_objective_ids`, `source_ids` |
| Evidence | `evidence_id`, `source_name`, `source_location`, `source_version`, `covered_period`, `source_as_of`, `source_owner`, `verification_status`, `limitations`, `linked_record_ids` |
| Review log | `check_id`, `check_description`, `result`, `exception_id`, `reviewer_role`, `reviewer_name`, `reviewed_at`, `decision`, `output_version` |

Allow a null `objective_id` or `kpi_ids` where a link is unknown, accompanied by an exception and next action. Missing required context is an explicit null plus an explanation, not a fabricated value. If an activity contributes to multiple initiatives, use mapping rows with the same activity ID; retain one canonical record and do not count its spend or benefits more than once.

### Board pack template

```markdown
# Finance Report to the Board — [Company] — [Board meeting date]

Classification: Board-confidential | Pack version: [version] | Status: Draft — pending CFO sign-off
Reporting period: [start–end] | Year to date: [start–end] | Source cutoff: [timestamp]
Basis of preparation: [e.g., unaudited management accounts, IFRS] | Currency / units: [values]
Versions: strategy [v], budget [v], actuals [v], outlook [v or N/A], KPI dictionary [v]
Prepared by: [role] | Reviewed by: [Controller] | Approved by: [CFO] | Pack control: [Board Secretary]
Sign convention: [negative variances shown in parentheses / with minus sign]

## 1. Cover memo (one page)
Purpose of this paper: [one sentence]

For decision
- D01: [decision], recommendation: [option], approver: [board / committee], by: [date]

For discussion
- [topic and the question the board is asked to consider]

For noting
- [result or event, one line each]

Headline: [most material result versus budget, with evidence ID]
Priority risk: [risk, executive owner, trend]

## 2. Executive summary (≤ 250 words)
Performance vs plan → strategic implication → principal risk → what management is doing → what the board is asked to do.

## 3. Financial performance
[Line item | Period actual | Budget | Variance | PY | YTD actual | YTD budget | YTD variance | FY budget | FY outlook]
Commentary for every variance above materiality: cause, whether it is timing or permanent, action, owner.
Cash, liquidity and covenant headroom: [values, source, headroom vs limits]

## 4. Strategy and KPI scorecard
[Objective | KPI | Prior | Actual | Budget/Target | Change | Gap | Status | Trend | Source]

## 5. Strategic initiatives
[Initiative | Objective | Executive sponsor | Milestone status | Budget vs spend | Expected benefit (basis) | Issue / ask]

## 6. Risks and controls
[Risk | Owner | Rating | Appetite status | Trend | Mitigation | Board attention required?]

## 7. Decisions required
For each: context → options and tradeoffs → management recommendation → authority level → draft resolution wording → deadline.

## 8. Prior board resolutions and actions
[Reference | Resolution / action | Owner | Due | Status | Evidence of closure]

## 9. Evidence, assumptions and limitations
[Sources and versions; missing data; untested assumptions; forecast basis; attribution limits; items after cutoff]

## 10. Review and approval
[Checks completed | Open exceptions | Controller review | CFO sign-off | Committee chair pre-read | Board Secretary acceptance]

## Appendices
A. Initiative and activity register (roles only)   B. KPI definitions and status rules
C. Financial detail and reconciliations            D. Management edition (if circulated)
```

## Workflow / decision steps

### Step 1 — Establish scope, versions and the board calendar

1. Read the configuration, strategy, budget, KPI dictionary, actuals, initiative plans, updates, prior board materials and evidence.
2. Confirm the reporting period, YTD window, scope, cutoff, units, basis of preparation and audience (board or committee).
3. Confirm the board meeting date and pre-read deadline. Work backward: CFO sign-off before the pre-read deadline; Controller review before that; preparer check before that. Record the dates in the review log.
4. Assign stable source IDs and locators (file/sheet/cell, page, ticket) precise enough for a reviewer to retrace.
5. Freeze the selected input versions for the run. Identify draft versus approved sources.
6. Log missing or stale inputs. Continue unaffected sections; hold affected conclusions.

### Step 2 — Convert strategy and budget into a strategy map

For each board-approved priority, record the objective ID, intended outcome, executive sponsor, timeframe, KPI, baseline, target and the budget lines that fund it. Explain how initiatives are expected to influence the KPI. Keep proposed interpretations separately marked for sponsor review.

Example mechanism: **standardize month-end reconciliations → reduce rework → complete reconciliations earlier → shorten the close → give the board timely information**. This is a proposed causal pathway until outcome evidence supports it.

Classify alignment as **Direct**, **Enabling** or **Unconfirmed**, as in v0.1. Required control or maintenance work can be enabling even when it produces no revenue. Absence of a KPI link is not proof that work is unnecessary.

### Step 3 — Normalize activity updates and roll them up to initiatives

Separate each update into activity, deliverable, completion evidence, observed outcome, possible strategic contribution, blockers and next action, with statuses `not_started`, `in_progress`, `completed`, `blocked` or `cancelled`. Keep self-reported completion visible until validated. Deduplicate by activity ID and evidence.

Then roll up for the board:

- Group activities under their initiative; report initiative milestone status, spend against budget and expected benefit.
- Replace employee names with roles. Name executives only as sponsors or owners of decisions and risks.
- Keep the activity-level register in the appendix or management edition. The board sees it only on request.
- Promote an activity to the board report on its own only if it is itself material: a blocked statutory deadline, a control failure, a material unsupported claim, or a request for authority above the delegation limits.

"Prepared a pricing analysis" is a completed deliverable. "Improved gross margin" is an outcome claim requiring actual results. "Could improve gross margin" is an expectation, not an observed result.

### Step 4 — Build the financial summary

Present the period, year to date and full year on one table: actual, budget, prior year, variance, and the latest approved outlook. Rules:

- Use the actuals version reconciled to the general ledger; state its audit/review status.
- Calculate variances in the direction directors expect: favorable variances positive for revenue and profit, unfavorable positive for cost only if the pack states that convention. Pick one convention and state it in the cover memo.
- Classify each material variance as **timing** (expected to reverse by year end, with the reversal period) or **permanent**, and say which.
- Show cash, liquidity and covenant headroom whenever the company has debt or a liquidity constraint; report headroom against the limit, not the ratio alone.
- Reconcile the full-year outlook to the version last presented to the board and bridge material changes.
- Do not restate prior-period figures silently. If a restatement is needed, show the previously reported value, the revised value, the reason and who approved it.

### Step 5 — Calculate KPI movement and target gaps

Use an approved definition and comparable populations, periods, currencies and units. Show actuals, budgets, targets and forecasts in separate fields.

```text
Absolute movement = current actual − comparable prior actual
Target gap = current actual − target for the same reporting period
Relative movement (%) = (current actual / prior actual − 1) × 100
```

Calculate relative movement only when the prior value is positive and the ratio is meaningful; otherwise show the absolute movement and explain. For rates expressed in percentage units, show movement and target gap in percentage points.

For direction `higher_is_better`, a positive target gap is favorable. For `lower_is_better`, a negative target gap is favorable. For `target_range`, use the approved bounds. Calculate aggregate ratios from underlying totals; do not average segment percentages without appropriate weights. Do not combine currencies without an approved conversion method, rate source and period.

### Step 6 — Assign performance, trend and evidence status separately

Performance status uses board-approved rules for the reporting period:

| Status | Rule |
|---|---|
| Green | Actual meets or exceeds a direction-specific target, or lies within the approved target range |
| Amber | Actual misses the target but falls within its approved amber tolerance |
| Red | Actual misses the target beyond that tolerance |
| Unknown | Missing definition, actual, comparable target, threshold or sufficiently current evidence prevents classification |

Trend is reported alongside status (improving / stable / deteriorating versus the prior comparable period), because a Red KPI that is improving and a Green KPI that is deteriorating call for different board attention.

Apply tolerance in the KPI's native units. Do not invent a universal 5% rule. Never assign Green from a forecast or a completed-task count when the KPI measures a business outcome.

Evidence status is independent: `validated`, `self_reported`, `missing`, `stale` or `conflicting`. "Validated" means reconciled to the selected source under this workflow, not independently audited or causally proven.

For an objective with several required KPIs, use the approved rollup rule. If none is supplied, show KPI-level statuses without an overall color. Any missing required KPI must remain visible; do not average colors or let an activity-completion rate override outcome evidence.

### Step 7 — Assess contribution without overstating causality

For each material claim, answer: what happened and what evidence supports it; what KPI moved over a comparable period; what mechanism connects the work to the result; what else could explain the movement; what can be concluded now and what remains unmeasured.

Use `observed_association`, `plausible_contribution`, `forecast_only`, `not_measured` or `attribution_supported` for contribution basis. Use `attribution_supported` only when evidence supports an incremental effect. A budget variance bridge explains arithmetic; it does not establish causality.

Keep these benefits distinct and never add them into one "total benefit" for the board:

- **Realized financial benefit:** an evidenced reduction in expenditure or increase in relevant earnings or cash, with period and baseline stated.
- **Released capacity:** time made available for other work; not cash savings unless an actual spending reduction is evidenced.
- **Estimated / forecast benefit:** modeled future impact, labeled and linked to the model version.

Do not sum overlapping benefits from several teams. Identify a shared benefit once, with contributing teams and any approved allocation method.

### Step 8 — Assess risks against appetite

Reconcile risks arising from this run to the corporate risk register. For each material risk, record the executive owner, impact, likelihood, rating, position against the board's risk appetite, trend, and the control or mitigation in place. Flag "Board attention required" when a risk is outside appetite, deteriorating, newly identified at material level, or tied to a decision requested in this pack. Do not rate risks the register has not rated unless the rating is labeled as management's proposal.

### Step 9 — Write the cover memo, commentary and draft resolutions

Write the cover memo last and place it first. Classify every item:

- **For decision:** the board or committee must resolve something within its authority. Provide options with tradeoffs, management's recommendation, the authority level under the delegation matrix, the deadline and draft resolution wording ("The Board resolves to…").
- **For discussion:** management seeks the board's view before a management decision or a future board decision.
- **For noting:** results and events that require no action.

If a request is within management's delegated authority, do not put it to the board as a decision; report it for noting with the authority reference.

Commentary follows **result → meaning for the plan → evidence / limitation → action and owner**. Lead with the most material item. Keep the executive summary to roughly 150–250 words. Write for a reader who did not attend the operational reviews: no internal acronyms without definition, no activity lists, no praise or blame of individuals.

Each action needs one accountable executive, a due date, a linked issue and a closure criterion; label proposed dates as proposed. Clearly separate recommendations from approved decisions.

### Step 10 — Follow up prior board resolutions and actions

Include every open resolution and action from prior minutes until closed with evidence, cancelled with a board-noted reason, or explicitly carried forward with a new date. A prior resolution's status is taken from minutes and evidence, never from an update that says "done".

### Step 11 — Reconcile, review and hand off

Run the controls below, resolve material exceptions and record remaining limitations. Then hand off:

| Integration | Handoff rule |
|---|---|
| Module 01 — Accounting | Use approved, reconciled actuals and evidence references; do not create or post correcting entries from this report |
| Module 02 — Tax | Link the provision and compliance milestones and review status; do not turn a draft tax estimate into a final liability or strategic fact |
| Module 03 — FP&A | Reuse approved objective/KPI IDs, budget version and outlook version; label scenario data separately from actuals; bridge the outlook to the last version shown to the board |
| Module 04 — Format alignment | Use accepted data plus the exception report; disclose excluded records and their effect on coverage |
| Module 05 — Board deck | Provide the signed-off cover memo, financial summary, KPI scorecard, decisions and draft resolutions, units, dates, source IDs and pack version; slide figures must match the pack and carry the same version number |
| Board Secretary | Deliver the frozen pack by the pre-read deadline with the version number, classification, distribution list and the list of open exceptions accepted by the CFO |

Only mark a pack approved when the CFO's sign-off and the Board Secretary's acceptance are recorded. Do not circulate it to directors, management or external parties without that authorization.

### Copy-and-use execution prompt

```text
Apply 06_reporting.md (board edition) to the attached client configuration and
source files. Act as an FP&A analyst preparing the finance section of a board
pack for the CFO's review.

1. Identify the reporting period, YTD window, source cutoff, board meeting date,
   pre-read deadline, strategy/budget/KPI/actuals versions and any gaps.
2. Build the strategy map; normalize all in-scope team activities; roll them up
   to initiatives with owners shown by role.
3. Build the financial summary: period, YTD and full year; actual vs budget vs
   prior year vs latest approved outlook; classify material variances as timing
   or permanent; show cash, liquidity and covenant headroom where relevant.
4. Calculate comparable KPI movements, target gaps, status and trend using the
   approved rules only; show formulas and sources.
5. Keep activity completion, KPI performance, evidence quality and contribution
   claims separate. Mark unconfirmed alignment and missing impact evidence.
6. Reconcile risks to the register and the risk appetite statement.
7. Classify every board item as for decision / discussion / noting. For each
   decision, give options, tradeoffs, recommendation, authority level, draft
   resolution wording and deadline. Do not escalate matters within management's
   delegated authority.
8. Carry forward every open prior board resolution and action with its status
   and evidence.
9. Draft the board pack in the template order, cover memo first. Export CSV
   appendices only if requested or useful and tools support them.
10. Run the validation controls and report what passed, failed or was not run.
11. Finish with a handoff note stating the main decision requested, open
    exceptions for the CFO to accept, and the sign-off steps still outstanding.

Do not invent numbers, budgets, targets, owners, evidence, impact, approvals,
resolutions or tool actions. Do not name individual employees or report their
performance. Do not treat capacity savings as cash savings or correlation as
proven causality. Use the supplied output naming convention and preserve
traceability.
```

## Assumptions and source hierarchy

Use the best source for each type of claim:

| Claim | Preferred source | Lower-confidence fallback |
|---|---|---|
| Strategic priority / target / budget | Board-approved strategy, budget and KPI dictionary effective for the period, with minutes reference | Management draft, clearly marked proposed |
| Financial actual | Reconciled general ledger or management accounts with stated audit/review status | Draft finance export, marked provisional |
| Outlook / forecast | Approved FP&A model and assumption register, version last shown to the board | Explicit draft estimate with assumptions |
| Operational result | Authoritative operational records with documented definitions | Manager-certified schedule or self-reported update |
| Completed deliverable | Accepted file, ticket, milestone or acceptance record | Employee statement, labeled self-reported |
| Risk rating | Corporate risk register approved by the risk owner / committee | Management proposal, labeled as such |
| Prior board decision | Approved minutes and resolutions | Management recollection, labeled unverified |

If sources disagree, log the conflicting values and versions and request the owner's resolution. Do not silently select the more favorable result. A newer timestamp alone does not establish approval or comparability.

Maintain an assumption register with assumption ID, statement, rationale, affected outputs, owner, confirmation status and expiry/review date. Do not present assumptions as source facts. External benchmarks are optional; if used, verify the source, date, definition and comparability and cite the original source.

## Validation and reconciliation controls

- **Coverage:** Every unique in-scope activity appears in the appendix register, including unconfirmed and cancelled work, and every in-scope initiative appears in the board report. Reconcile received records = unique included + excluded/out-of-scope + duplicates; keep an exclusion log.
- **Strategic traceability:** Every confirmed goal link uses an approved objective ID. Unconfirmed links carry a reason and an action owner.
- **Evidence:** Every material numeric or outcome claim has a source ID and precise locator with period, cutoff, version, status and limitations.
- **Metric integrity:** Check formula, units, signs, denominator, currency, period, scope, rounding and direction. Report division-by-zero and noncomparable data explicitly.
- **Financial reconciliation:** Period and YTD totals tie to the same approved actuals version used by Module 03 and the deck; the outlook reconciles to the version last shown to the board; restatements are disclosed. Document any difference before release.
- **One version of the numbers:** Cover memo, report, appendices and slides agree on every figure and carry the same pack version.
- **Status logic:** Statuses and trends are recalculated from approved rules. Task completion, actual performance, evidence quality and forecast expectations remain distinct.
- **Attribution and benefits:** No unsupported causal wording, overlapping benefits or cash-versus-capacity confusion; shared outcomes are not credited in full to each team; no combined "total benefit" that mixes benefit categories.
- **Board appropriateness:** No individual employee names or performance data in the board report; every item classified for decision / discussion / noting; every decision carries options, recommendation, authority level, draft resolution and deadline; nothing within delegated authority is put to the board as a decision.
- **Risk:** Every material risk has an executive owner, rating, appetite status, trend and mitigation, reconciled to the register or labeled as not reconciled.
- **Continuity:** Every open prior resolution and action is carried forward or closed with evidence; the pack references the prior minutes.
- **Actions:** Every material issue has an accountable executive, a confirmed or proposed due date and a closure criterion.
- **Privacy and confidentiality:** Only information the board needs; classification marked; disclosure policy applied for listed or regulated entities; no customer or personal details beyond what the audience requires.
- **Timeline:** Preparer check, Controller review and CFO sign-off are dated and fall before the pre-read deadline; items arriving after cutoff are separated from period results.
- **Review status:** No human reviewer, sign-off, acceptance test, resolution or system action is marked complete without evidence that it occurred.

For each control, record `pass`, `fail` or `not_run`, with the reason. A draft may contain visible exceptions; a pack cannot go to the Board Secretary with a failed material control unless the CFO has explicitly accepted the exception in the review log.

## Exception handling and escalation

| Exception | Reporting treatment | Reviewer / next step |
|---|---|---|
| Strategy or budget not formally board-approved | Draft a proposed map; label comparisons "versus management plan, not board-approved budget" | CFO confirms status with the Board Secretary |
| Activity has no credible strategic link | Keep it in the appendix as unconfirmed; do not label it waste; do not raise to the board unless material | Department Manager clarifies rationale |
| Completed work has no measured outcome | Report completion only; outcome not measured | Initiative sponsor defines follow-up measurement |
| Actual, target, formula or threshold missing | Show available data; affected status Unknown | KPI owner supplies approved definition/data |
| Target is annual but actual is monthly or quarterly | Use approved phasing if available; otherwise show progress without a period status | FP&A confirms phasing |
| Evidence is stale, conflicting or after cutoff | Flag the limitation; separate subsequent events from period results; disclose material post-cutoff events in the cover memo | Source owner and Controller resolve |
| Source totals do not reconcile | Hold the affected number and conclusion; continue unaffected sections | Controller resolves reconciliation |
| Outlook differs from the version last shown to the board | Bridge the change; label it a revised outlook pending CFO approval | CFO approves the revised outlook before circulation |
| Duplicate / shared contribution | Preserve traceability; count work and benefits once | Initiative sponsors confirm attribution |
| Claimed savings reflect fewer hours only | Reclassify as released capacity unless spending reduction is evidenced | Controller validates benefit category |
| Decision request is within management's delegated authority | Move to "for noting" with the DoA reference | CFO confirms authority level |
| Decision request exceeds the committee's authority | Route to the full board; note the committee's recommendation role | Board Secretary confirms routing |
| Prior resolution reported closed without evidence | Keep open; request closure evidence | Resolution owner supplies evidence |
| Required tool or source is unavailable | Identify the operation not performed; provide a manual handoff | Process owner supplies access or completes the check |
| New source arrives after CFO sign-off | Create a revised pack version and change log; re-obtain sign-off for affected content; the Board Secretary decides whether to recirculate or table at the meeting | CFO and Board Secretary |

Escalate only the blocked decision or unsupported conclusion. Do not fabricate missing data to make the pack appear complete.

## Human review and approval gate

| Role | Review responsibility | Evidence of completion |
|---|---|---|
| Initiative / activity owner | Factual accuracy of their updates and source references | Confirmed update or correction record |
| Department Manager | Deliverable acceptance, alignment, blockers, actions in the management edition | Review comments and sign-off for department scope |
| Controller / KPI owner | Metric definitions, reconciliations, financial figures, status, benefit categories, restatements | Completed control log and recorded review |
| FP&A Manager | Budget and outlook comparisons, variance classification, bridge to prior outlook | Recorded review |
| CFO | Content sign-off: strategic interpretation, materiality judgments, decisions requested, draft resolutions, accepted exceptions | Signed review log entry dated before the pre-read deadline |
| Audit / Finance Committee Chair | Pre-read where the charter requires it; comments before circulation | Recorded comments or "no comments" |
| Board Secretary / Company Secretary | Pack control: version, classification, distribution list, agenda placement, minutes references | Acceptance record and circulation log |
| Board of Directors / Committee | Decisions on items for decision | Minuted resolutions |

Pack lifecycle: **Draft → Controller review → CFO sign-off → Board Secretary accepted → Circulated → Minuted / Superseded**. Keep unresolved limitations visible in a signed-off pack if the CFO explicitly accepts them; do not imply missing evidence has been validated.

The AI prepares and checks the pack. Human reviewers approve facts, materiality judgments and recommendations. Only the board makes board decisions. For the MVP demonstration, simulated approvals must be labeled simulated and cannot authorize real circulation or system changes.

## Worked example (input → output)

### A. Fictional inputs

**Company:** Harbor Operations Co. — synthetic placeholder for the common demo company.
**Vision:** Grow profitably while giving the board and management timely, reliable information.
**Board meeting:** November 12, 2026 (Finance Committee); pre-read deadline November 5, 2026, 17:00 America/New_York.
**Reporting period:** September 1–30, 2026 (Q3 month three); comparison August 1–31, 2026. YTD omitted from this example to keep it checkable; a real run includes it.
**Source cutoff:** October 9, 2026, 17:00 America/New_York.
**Currency / units:** USD, whole currency units; rates shown as percentages.
**Basis:** unaudited management accounts.
**Output:** v0.1, Draft — pending Controller review and CFO sign-off.

All source IDs, records, owners and values are fictional and illustrate expected behavior only.

| Evidence ID | Illustrative source / locator | Version and coverage | Limitation |
|---|---|---|---|
| E01 | Strategy register, objectives O1–O3 and KPI rules K1–K3; board minutes 2026-01-22 | Strategy v1.0; September targets | Fictional approved inputs |
| E02 | Management accounts, P&L revenue / COGS rows | Actuals v1.0; August and September | Synthetic, unaudited |
| E03 | Close calendar, period completion dates | Calendar v1.0; August and September | Business-day convention held constant |
| E04 | Reconciliation tracker, September cohort of 15 items | Tracker v1.0; September 30 snapshot and August backlog | Unresolved items all overdue |
| E05 | Accepted deliverables A01–A03 and update A04 | Activity log v1.0; September | Cannot establish individual causal impact |
| E06 | Time estimate, 12 hours/week released; USD 50/hour assumed | Estimate v0.1; September | Self-reported; no expense reduction evidence |
| E07 | Board-approved FY2026 budget, September column | Budget v1.0 | Synthetic figures |
| E08 | Prior Finance Committee minutes 2026-08-13, resolution FC-2026-07 | Minutes v1.0 | Fictional |
| E09 | Delegation of authority matrix, pricing changes | DoA v2.0 | Fictional; pricing pilots above USD 100,000 annual revenue impact require committee approval |

| Objective | KPI / direction | August actual | September target | Approved synthetic status rule |
|---|---|---:|---:|---|
| O1 — Improve profitable growth | K1 Gross margin; higher is better | 37.0% | 40.0% | Green ≥40%; Amber ≥38% and <40%; Red <38% |
| O2 — Provide timely information | K2 Close duration in business days; lower is better | 8 | 6 | Green ≤6; Amber >6 and ≤7; Red >7 |
| O3 — Strengthen reliability | K3 Overdue reconciliations at month-end; lower is better | 5 | 2 | Green ≤2; Amber =3; Red ≥4 |

Financial inputs from E02 and E07:

| Metric | August actual | September actual | September budget |
|---|---:|---:|---:|
| Revenue | 900,000 | 1,000,000 | 980,000 |
| Cost of goods sold | 567,000 | 615,000 | 588,000 |
| Gross profit | 333,000 | 385,000 | 392,000 |
| Gross margin | 37.0% | 38.5% | 40.0% |

Board materiality rule (synthetic): commentary required for any P&L line variance above USD 5,000 or 1.0 pp against budget.

Operational inputs: the September close took 6 business days (E03). Of a cohort of 15 reconciliations scheduled for resolution, 12 were completed and 3 remained overdue at month-end (E04). Prior resolution FC-2026-07 (E08) asked management to bring the close to six business days by September and report back.

### B. Expected financial summary

| Line | Sep actual | Sep budget | Variance | Variance % | Aug actual | Commentary required |
|---|---:|---:|---:|---:|---:|---|
| Revenue | 1,000,000 | 980,000 | +20,000 | +2.0% | 900,000 | Yes (above USD 5,000) |
| COGS | 615,000 | 588,000 | −27,000 (unfavorable) | −4.6% | 567,000 | Yes |
| Gross profit | 385,000 | 392,000 | −7,000 (unfavorable) | −1.8% | 333,000 | Yes |
| Gross margin | 38.5% | 40.0% | −1.5 pp | n/a | 37.0% | Yes (above 1.0 pp) |

Sign convention used: favorable variances positive, unfavorable negative, for every line.

```text
Revenue variance = 1,000,000 − 980,000 = +20,000 (favorable), +2.0% of budget
COGS variance = 588,000 − 615,000 = −27,000 (unfavorable), −4.6% of budget
Gross profit variance = 385,000 − 392,000 = −7,000 (unfavorable), −1.8% of budget
Gross margin gap vs budget = 38.5% − 40.0% = −1.5 pp

Volume/mix split of the gross profit variance (arithmetic, not causality):
Revenue effect at budget margin = (1,000,000 − 980,000) × 40% = +8,000
Margin effect at actual revenue = 1,000,000 × (38.5% − 40.0%) = −15,000
Total = +8,000 − 15,000 = −7,000
```

Timing or permanent: not determinable from the synthetic inputs; a real run states which, with the expected reversal period.

### C. Expected KPI scorecard

| KPI | Aug actual | Sep actual | Sep target | Movement | Actual − target | Status | Trend | Source |
|---|---:|---:|---:|---:|---:|---|---|---|
| K1 Gross margin | 37.0% | 38.5% | 40.0% | +1.5 pp | −1.5 pp | Amber | Improving | E01, E02 |
| K2 Close duration | 8 days | 6 days | 6 days | −2 days | 0 days | Green | Improving | E01, E03 |
| K3 Overdue reconciliations | 5 | 3 | 2 | −2 | +1 | Amber | Improving | E01, E04 |

```text
August gross margin = 333,000 / 900,000 × 100 = 37.0%
September gross margin = 385,000 / 1,000,000 × 100 = 38.5%
Month-on-month gross profit increase = 385,000 − 333,000 = USD 52,000
  Revenue effect at prior margin = (1,000,000 − 900,000) × 37% = USD 37,000
  Margin effect at current revenue = 1,000,000 × (38.5% − 37%) = USD 15,000
Close duration reduction = 8 − 6 = 2 business days = 25%
Reconciliation cohort completion = 12 / 15 × 100 = 80% (not the K3 measure)
Estimated weekly capacity value = 12 hours × USD 50/hour = USD 600/week (released capacity, not cash)
```

### D. Expected initiative register (board level)

| Initiative | Objective | Sponsor | Milestone status | Expected benefit (basis) | Board item |
|---|---|---|---|---|---|
| I01 Close standardization (rolls up A01) | O2 / K2 | Controller | Checklist accepted and in use (E05); close at 6 days (E03) | Released capacity ~USD 600/week, self-reported (E06); contribution plausible, not isolated | For noting; closes FC-2026-07 subject to evidence |
| I02 Pricing and mix review (rolls up A02) | O1 / K1 | Commercial Lead | Analysis accepted (E05); implementation not started | Forecast-only; no actual margin effect attributable | For decision (D01) |
| I03 Reconciliation remediation (rolls up A03) | O3 / K3 | Controller | 12 of 15 cohort items complete; 3 overdue (E04) | Observed backlog reduction; balances under review | For discussion |
| Dashboard redesign (A04) | Unconfirmed | Finance Manager | Self-reported complete; no outcome evidence | Not measured | Appendix only; management action N02 |

A04 is not a board item: it is immaterial and its alignment is unconfirmed. It stays in the appendix with a management clarification action.

### E. Expected cover memo

> **Finance Report — Harbor Operations Co. — Finance Committee, 12 November 2026** (Draft v0.1, board-confidential)
>
> **Purpose.** Report September results against the approved budget and strategic KPIs, close out resolution FC-2026-07, and seek a decision on the pricing pilot.
>
> **For decision**
> - D01 — Pricing pilot. Management recommends authorizing a limited pricing pilot (scope, guardrails and measurement plan in section 7). Authority: Finance Committee under DoA v2.0 (E09). Decision requested at this meeting.
>
> **For discussion**
> - Reconciliation backlog: three overdue items against a target of two; remediation plan and timing (section 6).
>
> **For noting**
> - September revenue USD 1,000,000, 2.0% above budget; gross profit USD 385,000, USD 7,000 below budget; gross margin 38.5% versus 40.0% budget, up 1.5 pp on August (E02, E07).
> - Close completed in six business days, meeting target and the commitment in FC-2026-07 (E03, E08); closure of the resolution is recommended subject to the Committee's acceptance.
>
> **Headline.** Revenue beat budget but cost of sales grew faster; the margin shortfall of 1.5 pp drives an unfavorable gross profit variance of USD 7,000 (E02, E07). Whether this is timing or permanent is not yet determined.
>
> **Priority risk.** Margin target at risk for Q4 if mix and cost trends continue; owner: Commercial Lead; trend: improving month on month but outside budget.

### F. Expected decision paper (section 7 extract)

| Field | Content |
|---|---|
| Decision | D01 — Authorize a limited pricing pilot |
| Context | Gross margin 38.5% against a 40.0% budget; pricing and mix analysis accepted (E05); no implementation to date |
| Options | (a) Authorize a pilot on a defined product set with a margin floor and volume-loss stop rule; (b) Request a revised analysis including customer-retention sensitivity before deciding; (c) Defer to the next meeting |
| Tradeoffs | (a) earliest margin evidence, volume risk within guardrails; (b) better information, one quarter's delay; (c) no risk, no progress on O1 |
| Management recommendation | Option (a) |
| Authority | Finance Committee, DoA v2.0 (E09), because projected annual revenue impact exceeds USD 100,000 |
| Draft resolution | "The Finance Committee resolves to authorize management to run a pricing pilot on the product set described in Appendix C for a period not exceeding one quarter, subject to the margin floor and volume stop rule set out therein, and directs management to report the measured results to the Committee at its next scheduled meeting." |
| Decision deadline | 2026-11-12 (this meeting) |

### G. Expected actions and prior resolutions

All dates are proposed demonstration dates.

| ID / type | Item | Owner / approver | Due | Status / closure criterion |
|---|---|---|---|---|
| FC-2026-07 — Prior resolution | Bring the close to six business days by September and report back | Controller / Finance Committee | 2026-11-12 | Recommended for closure: September close 6 days (E03); Committee to confirm |
| N01 — Action | Resolve or document a remediation plan for the three overdue reconciliations | Controller / CFO | 2026-11-20 | Tracker and balance evidence show resolution or an approved plan for every item |
| N03 — Action | Validate the released-capacity estimate and how capacity is used | FP&A Manager / Controller | 2026-11-20 | Before/after work samples; benefit category confirmed |
| N02 — Management action (appendix) | Confirm the business need behind the dashboard redesign | Finance Manager / Department Manager | 2026-11-15 | Requirement documented or work reprioritized |

Coverage check: 4 received activity records = 4 unique included + 0 excluded + 0 duplicates; 3 roll up to board-level initiatives, 1 remains in the appendix as unconfirmed. The 12/15 cohort completion rate does not override K3's Amber status. Numerical results can be checked independently; human sign-offs and real source verification have not occurred.

### H. Negative examples

**Input 1:** "The new dashboard saved USD 20,000," with no baseline, source, period or calculation.
**Expected treatment:** Retain the activity in the appendix; label the claim unsupported; exclude USD 20,000 from any benefit figure; request evidence; record Controller review pending. Do not present it to the board.

**Input 2:** A department update asks the board to "approve the purchase of reconciliation software for USD 30,000," where the DoA gives the CFO authority to USD 50,000.
**Expected treatment:** Do not list it for decision. Report it for noting if material, with the DoA reference, or leave it in the management edition.

**Input 3:** The full-year outlook in the FP&A file is USD 120,000 lower than the outlook shown to the board in August, with no bridge.
**Expected treatment:** Hold the outlook figure; request the bridge and CFO approval; disclose in the cover memo that the outlook is under revision if the pack must be frozen first.

## Acceptance tests

Test specifications for the November 8 MVP review; not a claim that a live system or client dataset has passed. Record actual result, pass/fail/not-run, run date, evidence and reviewer when executing.

| Test | Input / condition | Expected result |
|---|---|---|
| AT01 — Worked example calculations | Synthetic E02–E04, E07 values | Gross margin 38.5%; +1.5 pp vs August; −1.5 pp vs budget; gross profit −7,000 vs budget (+8,000 volume, −15,000 margin); +52,000 vs August (37,000 / 15,000); close reduction 25%; cohort completion 80% |
| AT02 — Direction, status and trend | K1 38.5%; K2 6 days; K3 3 overdue | Amber / Green / Amber; all three "improving"; each tied to E01 rules |
| AT03 — Unsupported impact | USD 20,000 dashboard savings without evidence | Flagged; no benefit recognized; evidence request logged; not in the board report |
| AT04 — Missing KPI definition / target | Activity complete but definition or target absent | Completion shown; status Unknown |
| AT05 — Unconfirmed alignment | Activity has no approved link | Retained in appendix with clarification action; no invented goal, no claim of waste, not raised to the board unless material |
| AT06 — Duplicate and shared benefit | Same activity in two updates mapped to two goals | One canonical record, one benefit, both links preserved |
| AT07 — Incomparable data | Monthly actual vs annual target without phasing; mixed currencies | No unsupported comparison; exception escalated |
| AT08 — Forecast versus actual | Analysis predicts improvement; implementation not started | Forecast-only; excluded from actual KPI results |
| AT09 — Capacity versus cash | 12 hours/week × USD 50 | USD 600/week released capacity; no cash savings; never added to gross profit |
| AT10 — Stale / conflicting source | Source exceeds freshness rule or approved reports conflict | Flagged; no automatic Green; owner resolution requested |
| AT11 — Boundary and zero cases | Values at thresholds; prior value zero | K1 38% Amber, 40% Green; K2 7 Amber; K3 2 Green, 4 Red; relative movement from zero marked not meaningful |
| AT12 — Human approval | Calculations pass; no CFO sign-off or Board Secretary acceptance | Status remains Draft; no invented sign-off or circulation |
| AT13 — One version of the numbers | Pack and deck or FP&A outlook carry different actuals or outlook versions | Mismatch flagged; release held until reconciled or bridged |
| AT14 — Coverage and continuity | Duplicate, excluded and unconfirmed work; prior open actions | Counts reconcile; exclusions explained; open actions carried forward or closed with evidence |
| AT15 — Board appropriateness | Updates contain employee names, hours and task counts | Board report shows initiatives and roles only; names and performance data absent |
| AT16 — Decision classification | Items include a matter within CFO delegated authority and one above committee authority | Delegated matter moved to noting with DoA reference; above-authority matter routed to the board; every decision has options, recommendation, authority, draft resolution and deadline |
| AT17 — Prior resolution closure | Resolution FC-2026-07 and an update stating "done" without evidence | Closure recommended only where evidence (E03) exists; unevidenced resolution stays open |
| AT18 — Materiality and variance classification | Variances above and below the materiality rule | Commentary present only above threshold; each material variance labeled timing or permanent, or "not determinable" with a follow-up owner |
| AT19 — Outlook bridge | Outlook differs from the version last shown to the board | Bridge produced or outlook held; cover memo discloses revision status |
| AT20 — Pre-read timeline | Sign-off dates after the pre-read deadline | Timeline control fails; pack cannot be marked accepted |

**MVP completion criteria:** The worked example and at least two negative cases have recorded results; material calculations and sources reconcile; every strategic impact claim is supported or explicitly qualified; every board item is classified and every decision is complete; all activities and exceptions are accounted for; the pack carries dates, versions, classification and explicit reviewer status. Production and client readiness require the configured pilot and human acceptance described in the project plan.

## Version history

| Version | Date | Changes | Review status |
|---|---|---|---|
| v0.1 | 2026-11-02 | Initial reusable strategic reporting workflow aligned to Module 06; management-report audience | Draft; no sign-off |
| v0.2 | 2026-11-02 | Board-meeting edition: board reporting principles; board calendar, budget, risk-appetite, prior-minutes and DoA inputs; financial summary with budget, prior year, YTD, outlook and variance classification; initiative roll-up with roles only; for-decision / discussion / noting classification with draft resolutions; risk-appetite step; prior-resolution follow-up; CFO and Board Secretary approval chain; board-specific controls, exceptions and acceptance tests AT15–AT20; worked example rebuilt as a board pack | Draft for internal review; no client deployment or human sign-off claimed |

For later client versions, record configuration changes separately from core workflow changes. Preserve prior signed-off packs and explain material restatements instead of silently overwriting earlier conclusions.
