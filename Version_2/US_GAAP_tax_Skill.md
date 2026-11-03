# 2.1 — U.S. GAAP Income-Tax Reporting and U.S. Corporate Tax Preparation

**Project:** AI for Finance Department
**Module ID:** `2.1_US_GAAP_tax`
**Workflow version:** `0.3` — polished revision of v0.2 (jurisdiction-specific expansion of `02_tax.md` v0.1)
**Sources reviewed:** November 2, 2026
**Reporting framework:** U.S. GAAP, principally ASC 740, *Income Taxes*
**Tax jurisdiction:** United States federal corporate income tax, with separate state/local and international screening
**Demonstration period:** Calendar year 2025; Form 1120 (2025)
**Owner:** Client finance/controller team; assign a named owner at intake
**Reviewers:** U.S. GAAP financial-reporting reviewer and U.S. tax CPA/adviser
**Default status:** `DRAFT — FOR PROFESSIONAL REVIEW — NOT POSTED OR FILED`

This standalone workflow produces two connected outputs: the **income-tax component of U.S. GAAP financial reporting** (current and deferred tax, valuation allowance, uncertain tax positions, proposed journal entries, tax-note support) and **U.S. corporate tax-return working papers** (taxable-income bridge, Form 1120 line mapping, payment reconciliation, filing calendar). It does not certify complete financial statements, and it does not replace the entity's other accounting workflows.

---

## 1. Purpose and scope

### 1.1 Role and objective

Act as a finance-department tax accounting and preparation analyst. Start from approved U.S. GAAP records, explain why book income differs from taxable income, calculate supported current and deferred tax amounts, propose balanced entries, map amounts to the return, and surface reviewer questions. Keep the two authorities separate throughout: ASC 740 governs the financial statements; the Internal Revenue Code and IRS guidance govern the return.

| Workstream | Governing basis | Main result |
| --- | --- | --- |
| Financial reporting | Current FASB Codification, principally ASC 740 | Current/deferred tax expense, DTA/DTL, valuation allowance, ETR analysis, proposed entries, tax-note support |
| Tax compliance preparation | Internal Revenue Code, Treasury regulations, IRS guidance and official forms | Taxable-income computation, supporting schedules, draft Form 1120 line mapping, payment and penalty reconciliation, filing calendar |
| State/local tax | Each jurisdiction's law and forms | Separately configured nexus, apportionment, tax and deferred-tax workpapers |

Four distinctions that must survive every calculation:

1. **Book income is not taxable income.** A permissible book expense does not establish a tax deduction.
2. **A deferred tax liability is not a tax payment due now.**
3. **Tax payments reduce a liability or create a receivable; they do not determine the period's tax expense.**
4. **The ASC 740 provision is not itself a deductible return expense.**

### 1.2 Scope decisions

The demonstration entity is a domestic C corporation filing Form 1120. Before using Form 1120 or the 21% corporate rate for a real client, confirm legal entity, federal tax classification, elections, group structure and period. An LLC's legal label does not determine its federal tax treatment. Route S corporations (Form 1120-S), partnerships (Form 1065), sole proprietors, exempt organizations, foreign corporations and consolidated groups to separately configured workflows.

ASC 740 covers taxes based on income. Screen levies based on gross receipts, payroll, property, franchise or capital for the correct accounting scope rather than folding them into the income-tax provision. A federal-only calculation is not a complete U.S. tax provision until state/local and relevant foreign income taxes are addressed.

The following matters require expanded professional analysis whenever present: business combinations, foreign subsidiaries and GILTI/Subpart F, tax-sharing agreements, changes in tax status, credit monetization and transferability, stock-based compensation, section 163(j) interest limitations, section 174/174A research expenditures, section 382 ownership-change limitations, uncertain tax positions, corporate alternative minimum tax (CAMT), BEAT and reorganizations. Record their presence and assign work; do not silently assume they do not apply.

### 1.3 Run instruction

> Run `2.1_US_GAAP_tax.md` for the attached entity, reporting date and tax year. Verify the U.S. GAAP and tax-law configuration. Prepare the current-tax return bridge, deferred-tax and valuation-allowance schedules, uncertain-position register, balanced proposed entries, tax-note support, source-to-form mapping, filing calendar and professional review questions. Keep missing values explicit, distinguish book expense from tax payments, and return a draft package without posting, signing, filing or paying.

If the input set is incomplete, perform intake and all unaffected calculations first. Reading this file does not run software or populate a PDF; identify the tools actually used and the outputs actually created.

---

## 2. Inputs and required documents

### 2.1 Client configuration

```yaml
engagement:
  module_id: "2.1_US_GAAP_tax"
  workflow_version: "0.3"
  client_id: null
  entity_id: null
  legal_name: null
  secure_tax_id_reference: null        # reference only; never the EIN itself
  legal_entity_type: null
  federal_tax_classification: null     # C corp / S corp / partnership / disregarded
  tax_elections_reference: null
  ownership_group_reference: null
  tax_paying_component: null
  book_framework: "U.S. GAAP"
  public_business_entity_status: "UNCONFIRMED"
  sec_registrant_status: "UNCONFIRMED"
  reporting_period_start: null
  reporting_period_end: null
  financial_reporting_measurement_date: null
  annual_or_interim: null
  financial_statements_issue_status: null
  asu_2023_09_adoption_status: "UNCONFIRMED"
  tax_year_label: null
  tax_period_start: null
  tax_period_end: null
  period_type: null                    # calendar / fiscal / short-period
  return_type: null                    # original / amended (1120-X)
  tax_accounting_method: null          # cash / accrual
  federal_form: null
  form_revision: null
  form_and_instructions_verified_on: null
  original_due_date: null
  extension_filed: "UNCONFIRMED"       # Form 7004
  extended_due_date: null
  efile_required: "UNCONFIRMED"
  state_local_jurisdictions: []
  state_local_scope_status: "UNCONFIRMED"
  foreign_income_tax_scope_status: "UNCONFIRMED"
  reporting_currency: null
  return_currency: "USD"
  fx_policy_reference: null
  approved_preprovision_tb_version: null
  opening_tax_balances_version: null
  source_cutoff: null
  dataset_version: null
  forecast_version_for_dta_assessment: null
  gaap_reviewer_name: null
  tax_reviewer_name: null
  finance_owner_name: null
  output_version: "v0.3"
  permitted_data_environment: null
  retention_policy_reference: null
```

The reporting period, tax period and source-review date are three separate facts. Do not measure a December 31, 2025 balance using a rate enacted after that date. Evaluate later guidance, subsequent events and amended returns separately with the reviewers.

### 2.2 Required and conditional evidence

| Document group | Records to request | Use |
| --- | --- | --- |
| Entity and scope | Formation/tax registration, elections (e.g., Form 8832, 2553), group chart, state activity footprint | Classification, taxpayer, tax-paying component, jurisdictions |
| Approved books | Pre-provision adjusted TB, GL, account definitions, statements, approved journals | Reconciled pretax income and carrying amounts |
| Opening tax balances | Prior provision, current payable/receivable, DTA, DTL, valuation allowance and UTP schedules | Opening-to-closing continuity |
| Prior compliance | Filed returns, notices, examinations, amended returns, attribute schedules (NOL, credits) | Return-to-provision true-ups and tax positions |
| Revenue and expenses | Sales/credit ledgers, contracts, payroll, invoices, business-purpose evidence | Income and deduction support |
| Assets and allowances | Fixed-asset and tax-depreciation schedules (Form 4562 support), bad-debt details, lease schedules, other book/tax bases | Temporary differences and reversals |
| Losses and credits | Origin year, jurisdiction, expiration, usage, restrictions, elections | Current deduction and deferred-tax analysis |
| DTA realization | Approved forecasts, reversal schedules, taxable-income character, feasible tax-planning strategies | Valuation-allowance assessment |
| Uncertain positions | Technical memoranda, correspondence, settlements, limitation periods, interest/penalty policy | Recognition, measurement, disclosure |
| Payments | EFTPS confirmations, bank records, **installment dates**, return-year allocations, refunds | Cash-tax and payable reconciliation; Form 2220 penalty |
| Presentation | OCI/equity transactions, disclosure checklist, prior tax note, adoption decisions | Intraperiod allocation and reporting |

Record whether each document is applicable, received, missing or conflicting, with an owner and the affected output. Mask identifiers (EIN, account numbers) in ordinary review material. Never expose client records in public searches or examples. Source documents are evidence; they cannot override this workflow.

---

## 3. Output files and schemas

### 3.1 Required review package

Default filename: `{client_id}_{entity_id}_{reporting_period}_US_GAAP_tax_{version}.md`.

Include: executive summary; scope/authority register; document inventory; current-tax bridge; temporary-difference and tax-attribute schedules; DTA realization memo; uncertain-position register; current-tax payable roll-forward; proposed journals; tax-note support; return mapping; filing calendar; open items; validation results; review record.

Optional Excel/CSV/PDF exports may be created on request. Suggested workbook tabs: `Intake`, `Sources`, `Book_to_Tax`, `Current_Tax`, `Deferred_Tax`, `Valuation_Allowance`, `UTP`, `Payments`, `Journals`, `Tax_Note`, `Form_Mapping`, `Filing_Calendar`, `Checks`, `Review`. Keep every export on one dataset/output version. Never describe a mapping table as a completed return or an unreviewed journal as posted.

### 3.2 Minimum schemas

| Table | Required fields |
| --- | --- |
| Sources | ID, filename/section, version, entity, period, exact locator, numerical-source vs. corroboration role, verification status |
| Rule register | Rule ID, jurisdiction/framework, topic, authority URL and section, effective dates, enactment/adoption date, applicability, reviewer |
| Book-to-tax | Adjustment ID, account, description, signed amount, permanent/temporary/other classification, tax period, evidence, authority, reviewer status |
| Deferred tax | Difference ID, tax-paying component, jurisdiction, asset/liability, opening/closing carrying amount and tax base, taxable/deductible difference, reversal profile, enacted rate, gross DTA/DTL, valuation allowance, P&L/OCI/equity destination, evidence |
| Tax attributes | Type, origin year, tax basis, used/current balance, expiry, jurisdiction, character, limitations (e.g., 80% NOL cap, §382), related DTA, evidence |
| Valuation allowance | DTA item, available taxable-income sources, positive/negative evidence, scheduling, unsupported portion, proposed allowance, decision owner |
| UTP | Position ID, return benefit, technical merits, recognition conclusion, outcome amounts/probabilities, recognized benefit, unrecognized amount, interest/penalties, evidence, reviewer |
| Form mapping | Form/year, page/schedule/line, field, raw/display amount, formula, source locators, adjustment IDs, data/review status |
| Payments | Payment ID, authority, entity, period applied, **date**, amount, confirmation, bank tie, allocation status |
| Journals | JE ID, entity, date, account, debit, credit, currency, current/deferred/VA/UTP classification, P&L/OCI/equity destination, support, approval/posting status |
| Filing calendar | Obligation, form, jurisdiction, period, due date, extended due date, status (not due / filed / late / amended), owner |
| Controls/review | Check ID, expected/actual result, evidence, PASS/FAIL/NOT_TESTED, output version, reviewer, date, conditions, sign-off reference |

Keep `data_status` (`SUPPORTED`, `CALCULATED`, `CONFIRMED_ZERO`, `NOT_APPLICABLE`, `MISSING`, `CONFLICT`) separate from `review_status` (`PENDING_REVIEW`, `APPROVED`, `CHANGES_REQUIRED`). Unsupported numeric fields are `null`, never zero. Package states: `INTAKE_INCOMPLETE`, `DRAFT_WITH_OPEN_ITEMS`, `READY_FOR_REVIEW`, `REVIEWED_DRAFT`. Approval requires a real recorded human action and does not authorize posting or filing.

---

## 4. Workflow steps

### Step 1 — Confirm framework, tax scope and effective dates

Confirm U.S. GAAP, annual vs. interim reporting, PBE status, tax classification and every relevant jurisdiction. Document the form revision and the disclosure-regime adoption status. If the books use another framework, request an approved U.S. GAAP conversion bridge before treating them as a U.S. GAAP baseline.

An interim engagement requires separately configured ASC 740-270 (estimated annual ETR) workpapers. The annual example below does not establish an interim provision; if that configuration is unavailable, prepare the underlying schedules and flag the interim measurement as unresolved.

Use **enacted** law for U.S. GAAP measurement. A proposed bill, or a rule that would be "substantively enacted" under IFRS, is not an enacted U.S. GAAP rate. [FASB-CORE; FASB-109-BACKGROUND]

### Step 2 — Verify sources and reconcile the baseline

Identify the approved **pre-provision** TB, opening tax balances and closing adjustments. Reconcile debits/credits, GL, statements and source populations. Reject unexplained entity/period/currency mismatches and investigate duplicates. An invoice already in the TB corroborates the balance; it is not an additional expense feed.

Separate current-year profit from opening retained earnings. Identify any tax expense already booked so the proposed journal is the incremental adjustment, not a duplicate full provision. Record preliminary vs. final-close status. An unexplained imbalance blocks dependent totals; never introduce a plug.

### Step 3 — Build the return-oriented current-tax computation

Start from labeled pretax book income. Classify each adjustment as permanent, temporary or other, and reconcile taxable income before and after NOL/special deductions. For each item record treatment, period, source, authority and sign. Do not classify uncertain items merely to make the bridge balance.

Review at least: income timing; meals (50% under §274(n)) and entertainment (0%); bad debts (specific charge-off for non-banks); book vs. tax depreciation (Form 4562); accruals and the economic-performance rules; capital vs. revenue expenditure; tax-exempt income; federal income-tax expense if starting from after-tax income; NOLs and the 80% taxable-income limitation; credits; §163(j); related-party items; state conformity.

**2025 law changes to verify, not roll forward.** The 2025 Form 1120 instructions reflect legislation enacted in July 2025. Confirm current treatment of at least: 100% bonus depreciation for qualifying property acquired after January 19, 2025; immediate expensing of domestic research expenditures under §174A for tax years beginning after December 31, 2024 (foreign research remains amortized); the §163(j) adjusted-taxable-income computation reverting to an EBITDA-style base; and the raised §179 limits. Verify each against IRS-INST and the enacted statute before applying. [IRS-INST; IRS-163J; IRS-UPDATES]

Compute regular tax, credits and other taxes in separate rows. Screen CAMT (Form 4626; generally large corporations with 3-year average AFSI over $1 billion) and BEAT before calling the regular-rate calculation "total tax." Do not apply the 21% C-corporation rate to another entity classification. Keep prior-year true-ups and amended-return adjustments separate from current-year activity.

### Step 4 — Build deferred taxes from carrying amounts and tax bases

For each material balance and tax attribute, compare the financial-statement carrying amount with its supported tax base. Determine whether recovery or settlement produces future taxable or deductible amounts. Keep balance-sheet temporary differences distinct from this year's return adjustments. Permanent differences never create deferred taxes.

Measure gross DTA/DTL at enacted rates expected to apply when the differences reverse, by jurisdiction; never at a historic effective rate. Apply recognition exceptions (e.g., certain outside-basis differences) only with documented authority and reviewer approval. Track acquisitions, disposals, rate changes, return true-ups, FX and OCI/equity movements separately. [FASB-CORE; FASB-109-BACKGROUND]

```text
Opening gross DTA / DTL
+ additions and current-period reversals
+ enactment, true-up, acquisition and other identified changes
= closing gross DTA / DTL

Closing gross DTA − closing valuation allowance = closing net DTA
```

For P&L-only movements, deferred tax expense = ΔDTL − ΔDTA + Δvaluation allowance. Strip out movements allocated elsewhere before using that shortcut. Do not multiply this year's net return adjustment by a rate and assume it reproduces every closing deferred balance.

### Step 5 — Assess realization of deferred tax assets

Evaluate realization separately for each tax-paying component and jurisdiction, considering: reversal of existing taxable temporary differences; taxable income in available carryback periods (generally none for post-2020 NOLs); future taxable income of the appropriate character; and prudent, feasible tax-planning strategies. Weigh positive and negative evidence; a cumulative loss in recent years is significant objective negative evidence.

Recognize a valuation allowance to the extent it is **more likely than not** that some or all of the DTA will not be realized. This differs from IFRS's direct recognition constraint. Document the amount and evidence; an optimistic forecast or a net DTL alone is insufficient without timing, character and limitation analysis. Never use a valuation allowance as a substitute for an uncertain-position recognition decision. [FASB-CORE; FASB-109-BACKGROUND; FASB-FIN48-BACKGROUND]

### Step 6 — Analyze uncertain tax positions

Two sequential decisions:

1. **Recognition** — Is the position more likely than not to be sustained on technical merits, assuming examination with full knowledge of all relevant information? If not, no benefit is recognized.
2. **Measurement** — For positions that pass recognition, record the largest benefit with a cumulative probability greater than 50% of being realized on settlement. Do not use an expected-value average or the probability of avoiding audit. [FASB-CORE, ASC 740-10; FASB-FIN48-BACKGROUND]

Track return benefit, financial-reporting benefit and unrecognized benefit separately. Address interaction with deferred taxes and attributes, interest/penalty policy, settlement timing and disclosure (including Schedule UTP where required). The technical opinion and outcome probabilities belong to the tax adviser; the AI may organize facts and compute supplied scenarios but must not invent probabilities or legal support.

### Step 7 — Allocate, propose entries and prepare reporting

Allocate the period's tax effects among continuing operations, discontinued operations, OCI and direct equity under ASC 740-20. Do not assume every deferred-tax movement belongs in P&L, and do not import IFRS backward-tracing. [FASB-ALLOCATION; FASB-CORE]

Enacted rate changes require a separately identified remeasurement, recorded in continuing operations under ASC 740; the originating item's earlier OCI/equity location does not by itself determine the destination. Document the conclusion rather than copying a prior-period allocation.

Propose separate current-tax, deferred-tax, valuation-allowance and UTP entries, each balanced and traceable. Compare required closing balances with amounts already booked. Payment application is separate from expense recognition. Route entries to the controller for approval and posting through the accounting module.

In a classified balance sheet, deferred taxes are **noncurrent**. Net DTA/DTL and the related valuation allowance only within the same tax-paying component and jurisdiction. Analyze current-tax assets/liabilities separately. [FASB-PRESENTATION, ASC 740-10-45-4 and 45-6]

Prepare current/deferred expense components, gross DTA/DTL with valuation-allowance support, tax attributes, UTP support, cash taxes paid and an ETR explanation. ETR = income-tax expense from continuing operations ÷ pretax income from continuing operations. If the denominator is zero or the ratio is misleading, explain the components instead of reporting an artificial percentage.

### Step 8 — Apply the correct disclosure regime

ASU 2023-09 is effective for annual periods beginning after December 15, 2024 for PBEs and after December 15, 2025 for all other entities; early adoption is permitted. Transition is prospective, with retrospective application permitted. Determine the entity's **actual** adoption status — a 2026 preparation date does not make the standard mandatory for a private entity's 2025 period. [FASB-DISCLOSURES, ASC 740-10-65-9]

When adopted, gather the disaggregated rate-reconciliation and cash-paid information. The two thresholds have different denominators:

- **Rate reconciliation (PBEs):** disclose categories at or above **5% of the amount computed as pretax income (loss) from continuing operations × applicable statutory rate**.
- **Cash taxes paid:** disclose individual jurisdictions at or above **5% of total income taxes paid, net of refunds**.

Apply the Codification's sign/absolute-value and other detailed requirements; document zero, negative-denominator or net-refund cases rather than forcing a percentage. Use the full ASC 740-10-50 checklist for the final note. [FASB-DISCLOSURES]

| Tax-note output | Minimum draft content and tie |
| --- | --- |
| Income and expense | Pretax income; current/deferred components; domestic/foreign and federal/state splits; tie to statements |
| Deferred balances | Gross DTA/DTL, valuation allowance, material movements; tie to tax-base schedules |
| Rate explanation | Applicable PBE/non-PBE reconciliation; material drivers; tie to continuing-operations expense |
| Cash taxes | Payments net of refunds and jurisdiction detail; tie to bank/cash-flow evidence |
| Attributes and uncertainty | NOLs/credits with expirations, UTPs, open examination years, significant judgments; tie to reviewed registers |

This is a preparation template; the adopted checklist determines the complete required disclosures.

### Step 9 — Map the draft return, reconcile payments and build the filing calendar

Map supported amounts to the selected year's official lines and required schedules and forms (Form 4562, Schedule K questions, Schedules L/M-1/M-2 or M-3, Schedule UTP, Form 2220, state returns). Reconcile Schedule M-1 (or M-3 where total assets are $10 million or more) to page 1, line 28. A return-adjustment schedule and the form's adjusted deductions are two views of the same treatment; never apply an adjustment twice.

Reconcile current tax expense, prior-year balances and true-ups, estimated payments, extension payments, refunds and closing payable/receivable. Reconcile cash taxes paid for disclosure to bank cash flows, not merely to amounts claimed on one return. Missing installment dates leave the Form 2220 penalty unresolved even when the aggregate payment total is supported.

**Filing calendar for a calendar-year C corporation (verify each run against IRS-UPDATES and state sites):**

| Obligation | Form | Due | Notes |
| --- | --- | --- | --- |
| Original return | 1120 | 15th day of the 4th month after year-end (April 15, 2026 for CY2025) | June 30 fiscal years: 15th day of 3rd month |
| Extension | 7004 | By the original due date | Automatic 6-month extension of time to **file**, not to pay |
| Extended return | 1120 | October 15, 2026 for CY2025 | Late-filing penalty under §6651 runs from the extended date if missed |
| Estimated taxes | EFTPS deposits | April 15, June 15, September 15, December 15 of the tax year | Form 1120-W is now historical; compute installments per the Form 1120 instructions and §6655. Required when estimated tax is $500 or more |
| Underpayment penalty | 2220 | With the return | Needs installment dates and amounts |
| Amended return | 1120-X | Generally within 3 years of filing | Separate workflow; separate provision true-up |
| Electronic filing | — | Mandatory where the corporation files 10 or more returns of any type in the calendar year | Confirm e-file eligibility and signature authorization (Form 8879-CORP) |

**Timing note for this demonstration.** The sources were reviewed on November 2, 2026, which is after both the original (April 15, 2026) and extended (October 15, 2026) due dates for a calendar-2025 Form 1120. A real 2025 return prepared now is either already filed (in which case this module supports a true-up or amended return), or late (in which case failure-to-file and failure-to-pay penalties and interest accrue and must be quantified). Meanwhile the 2026 tax year is in progress and its fourth estimated-tax installment is due December 15, 2026. Record the actual filing status in the configuration before concluding anything about amounts owed.

Validate, then deliver a draft with precise decisions requested. Record review only when actually supplied. Any change to data, law, judgments or mappings requires a new version and renewed review of affected content. Do not post, file, sign, pay or transmit to an adviser as an implied next step.

---

## 5. Assumptions and source hierarchy

### 5.1 Evidence and authority

For U.S. GAAP, the current FASB Codification is authoritative, with SEC requirements for registrants. ASUs communicate Codification changes; archived predecessor standards and summaries are background only. For tax, use the statute, regulations and official IRS/state materials for the actual period, with professional interpretation where needed. Client records establish facts; prior treatment is evidence of history, not proof of present correctness.

Log every material assumption, effective date, unresolved conflict and decision owner. Do not treat missing loss schedules, unknown state nexus, missing tax bases or unreviewed UTP analysis as zero. If current Codification text cannot be accessed, record the verification gap and request an authorized excerpt or reviewer verification; never assert paragraph-level verification that did not occur.

### 5.2 Source register — reviewed November 2, 2026

| ID | Official source | Use and limits |
| --- | --- | --- |
| FASB-CORE | [FASB Accounting Standards Codification](https://asc.fasb.org/) | ASC 740-10 recognition/measurement/disclosure; 740-20 allocation; 740-270 interim. Paragraph access must be verified for the client; the public landing page did not expose readable paragraph text during preparation |
| FASB-109-BACKGROUND | [FASB summary of Statement 109](https://fasb.org/page/PageContent?bcpath=tff&pageId=%2Freference-library%2Fsuperseded-standards%2Fsummary-of-statement-no-109.html) | Archived background on enacted rates, temporary differences and valuation allowance; superseded by the Codification |
| FASB-FIN48-BACKGROUND | [FASB summary of Interpretation 48](https://fasb.org/page/PageContent?bcpath=tff&pageId=%2Freference-library%2Fsuperseded-standards%2Fsummary-of-interpretation-no-48.html) | Archived background on UTP recognition/measurement; confirm against current ASC 740 |
| FASB-PRESENTATION | [ASU 2015-17](https://storage.fasb.org/ASU_2015-17.pdf) | Noncurrent presentation and component/jurisdiction netting (ASC 740-10-45-4, 45-6) |
| FASB-ALLOCATION | [ASU 2015-01](https://storage.fasb.org/ASU%202015-01.pdf) | Conforming amendments to ASC 740-20 (removal of extraordinary items). Tangential; rely on current ASC 740-20 text for allocation mechanics |
| FASB-DISCLOSURES | [ASU 2023-09](https://storage.fasb.org/ASU%202023-09.pdf) | Disclosure amendments and ASC 740-10-65-9 effective dates/transition |
| IRS-FORM | [Form 1120 (2025)](https://www.irs.gov/pub/irs-prior/f1120--2025.pdf) | Page 1 and Schedules J/K/L/M-1 line references |
| IRS-INST | [Instructions for Form 1120 (2025)](https://www.irs.gov/pub/irs-prior/i1120--2025.pdf) | Lines 15, 17, 20, 26; meals; Schedule J; estimated tax; rounding; current developments |
| IRS-UPDATES | [About Form 1120](https://www.irs.gov/forms-pubs/about-form-1120) | Recheck revisions, corrections and developments each run |
| IRS-163J | [IRS §163(j) questions and answers](https://www.irs.gov/newsroom/questions-and-answers-about-the-limitation-on-the-deduction-for-business-interest-expense) | Year-sensitive guidance; 2025 changes require separate calculation |
| IRS-2220 | [Instructions for Form 2220 (2025)](https://www.irs.gov/file_source/pub/irs-pdf/i2220.pdf) | Estimated-tax underpayment penalty; $500 de minimis exception; penalty flows to Form 1120 line 34 |
| IRS-EST | [Guidance on determining a corporation's estimated tax payment](https://www.irs.gov/forms-pubs/guidance-on-determining-a-corporations-estimated-tax-payment) | Confirms Form 1120-W is historical; current installment guidance |

FASB summaries were surfaced through official FASB search results; direct page extraction was limited. Issued ASU PDFs and IRS forms/instructions were accessible. This workflow summarizes procedures and does not reproduce the standards. Source dates document the research performed, not professional approval or a claim that every rule was reviewed.

---

## 6. Validation and reconciliation controls

| Control | Required result |
| --- | --- |
| Scope and dates | Framework, tax classification, reporting/tax periods and form revision agree; enactment and adoption dates considered; filing status recorded |
| Baseline | TB debits equal credits; accounts agree to approved books; existing tax entries identified |
| Completeness | Accepted plus quarantined records reconcile to input; no hidden exclusions or duplicate expense feeds |
| Current tax | Pretax bridge equals direct taxable-income calculation and form subtotal (page 1, line 28) |
| Temporary differences | Closing carrying amounts and tax bases reproduce gross DTA/DTL; opening balances and movements reconcile |
| Permanent differences | No deferred tax created for a permanently nondeductible item |
| DTA realization | Allowance conclusion has evidence and timing/character/limitation analysis |
| UTP | Recognition precedes measurement; no unsupported probabilities or valuation-allowance substitution |
| Provision | Current + deferred + other identified components = reported income-tax expense |
| Allocation | P&L/OCI/equity allocations reconcile to total change; exceptions separately supported |
| Journals | Every entry balances and reconciles required to booked balances; no automatic posting |
| Payments | Expense, payments, prepaid tax and payable/receivable are distinct and reconcile; installment dates captured |
| Presentation | Noncurrent deferred-tax presentation and permitted netting documented |
| Disclosures | Correct PBE/adoption checklist applied; note amounts tie to schedules and cash flows |
| Form | Schedule M-1 line 10 = page 1 line 28; Schedule J line 12 = page 1 line 31; Schedule J line 23 = page 1 line 33 |
| Filing calendar | Due dates, extension status and late-filing exposure recorded with evidence |
| Review/version | Every output carries source cutoff, version and actual reviewer status |

Require zero unexplained difference at stored precision. Retain cents in workpapers; follow the form's rounding instructions for displayed values. A materiality threshold is not permission to conceal a reconciliation error. Report `NOT_TESTED` when a check did not run. Arithmetic verification is not legal validation.

---

## 7. Exception handling and escalation

`BLOCKER` prevents the affected calculation or a complete draft; `REVIEW` identifies supported work needing judgment; `INFO` explains a limitation. Continue unaffected work and identify the precise field/amount at risk.

| Situation | Action / reviewer |
| --- | --- |
| Wrong framework, classification, period or form revision | Resolve configuration before dependent mapping; finance owner/tax adviser |
| Unbalanced TB or duplicated provision | Reconcile with controller; no plug or duplicate expense |
| Unsupported tax base or opening DTA/DTL | Hold affected deferred balance and expense; accounting/tax reviewers |
| Only a proposed or "substantively enacted" rate supplied | Verify enacted U.S. law at the measurement date; hold unsupported remeasurement |
| Losses or adverse evidence undermine a DTA | Prepare realization analysis and allowance alternatives; GAAP reviewer |
| Uncertain tax position or settlement | Obtain technical assessment; tax adviser; assess interest/penalties separately |
| State/foreign footprint unresolved | Identify affected provision and filing scope; relevant specialist |
| Missing installment dates | Preserve supported payment total; hold Form 2220 penalty and final balance |
| Return due date passed or extension status unknown | Record late-filing/late-payment exposure; tax adviser quantifies penalties and interest |
| Complex group, acquisition or international matter | Expand scoped workpapers and review; do not apply the simple example mechanically |
| Unavailable current accounting authority | Record limitation; require authorized reference or reviewer validation |

---

## 8. Human review and approval gate

The finance owner confirms records and completeness. The controller/GAAP reviewer approves tax-accounting judgments, presentation and proposed journals. The tax CPA/adviser approves tax treatment, elections, return mappings and deadlines. Management retains responsibility for the financial statements and any separate filing authorization.

- [ ] Confirm framework, PBE/adoption status, classification, jurisdictions and filing status.
- [ ] Approve the accounting baseline and opening tax balances.
- [ ] Review current-tax adjustments, attributes, rates and supporting schedules.
- [ ] Review temporary differences, realization evidence, allowance and UTP conclusions.
- [ ] Review allocation, proposed entries, payable reconciliation and disclosure support.
- [ ] Resolve required form fields and attachments, payment timing, penalties and open items.
- [ ] Record the exact dataset/output version accepted and any conditions.

```text
Dataset and output versions reviewed:
GAAP reviewer / role / review date:
Tax reviewer / role / review date:
Decision: Changes required / Draft reviewed
Conditions and unresolved matters:
Approval evidence reference:
Journal posting authorization: Not provided by this workflow
Return submission authorization: Not provided by this workflow
```

Leave reviewer names, decisions and dates blank until supplied. Shared project controls apply when provided; this file's embedded controls permit standalone use. Refer approved tax journals to accounting module 01 and data-quality issues to module 04 without assuming those files or integrations exist.

---

## 9. Worked example (input → output)

### A. Synthetic company and facts

**Example Finance Services Inc.** (`US-DEMO-001`) is a fictional domestic C corporation with U.S. GAAP books, accrual tax accounting and a December 31, 2025 year-end. Currency is USD. It is not a PBE and has not early adopted ASU 2023-09 for 2025; the exercise still produces ETR and cash-tax workpapers. Its real adoption assessment would be documented separately.

The example assumes no state/local or foreign income taxes, losses, credits, additional Schedule J taxes, uncertain positions or OCI/equity tax effects. These are explicit synthetic facts, not conclusions inferred from missing documents. No CPA has approved the data or treatment. The example does not determine a real entity's nexus, filing obligations or full GAAP compliance.

| Source ID | Embedded fact / locator |
| --- | --- |
| US-TB | Pre-provision TB below, by account code |
| US-MEALS | Account 5700 is 10,000 of otherwise qualifying non-entertainment business meals; 50% limitation under §274(n); business purpose and employee presence supplied as fixture facts |
| US-ASSET | Current-year asset cost 100,000; book depreciation 20,000; supported illustrative tax depreciation 40,000; no disposals; closing book/tax bases 80,000 / 60,000 |
| US-AR | Gross receivables 80,000; book allowance 12,000 arose this year; no debts qualify for a current charge-off deduction; tax base 80,000; future deduction supported under fixture assumptions |
| US-REALIZATION | Opening deferred balances and allowance are zero; forecast taxable income of appropriate character and timing supports the 12,000 future deduction; no limitation; zero valuation allowance is an explicit test assumption |
| US-PAY | 20,000 paid and applied to 2025 federal estimated tax, matching account 1250; **individual installment dates intentionally missing** |

The 40,000 tax depreciation is a supplied schedule input, **not a universal 40% rate or an automatically chosen election**. A real engagement must validate asset class, acquisition and in-service dates, bonus/§179 elections and applicable law on Form 4562. The bad-debt treatment assumes an ordinary service corporation, not a bank eligible for a reserve method.

### B. Approved-for-demonstration pre-provision TB

No income-tax provision is recorded yet. Revenue and expenses are unclosed; retained earnings exclude current-year income.

| Account | Description | Debit | Credit |
| --- | --- | ---: | ---: |
| 1000 | Cash | 100,000 | 0 |
| 1100 | Gross trade receivables | 80,000 | 0 |
| 1150 | Credit-loss allowance | 0 | 12,000 |
| 1200 | Prepaid insurance | 6,000 | 0 |
| 1250 | Federal estimated-tax prepayments | 20,000 | 0 |
| 1500 | Equipment cost | 100,000 | 0 |
| 1590 | Accumulated book depreciation | 0 | 20,000 |
| 2000 | Accounts payable | 0 | 25,000 |
| 2100 | Accrued payroll liabilities | 0 | 15,000 |
| 3000 | Common stock | 0 | 40,000 |
| 3100 | Opening retained earnings | 0 | 69,000 |
| 4000 | Service revenue | 0 | 400,000 |
| 4100 | Interest income | 0 | 1,000 |
| 5000 | Officer compensation | 50,000 | 0 |
| 5010 | Other salaries | 100,000 | 0 |
| 5100 | Employer payroll taxes | 16,000 | 0 |
| 5200 | Rent | 36,000 | 0 |
| 5300 | Insurance expense | 6,000 | 0 |
| 5400 | Professional fees | 14,000 | 0 |
| 5500 | Software subscriptions | 8,000 | 0 |
| 5600 | Utilities | 4,000 | 0 |
| 5700 | Business meals | 10,000 | 0 |
| 5800 | Book depreciation | 20,000 | 0 |
| 5900 | Credit-loss expense | 12,000 | 0 |
| **Total** | | **582,000** | **582,000** |

Income 401,000; operating expenses 276,000; **pretax book income 125,000**. Other ordinary deductions are assumed supported and allowable in the period. There are no unapproved baseline journals or existing tax entries to duplicate.

### C. Current-tax computation

| Item | Signed amount | Classification / evidence |
| --- | ---: | --- |
| Pretax book income | 125,000 | US-TB |
| A-01: Nondeductible meals (50%) | +5,000 | Permanent; US-MEALS; §274(n); IRS-INST line 26 |
| A-02: Book credit-loss allowance expense | +12,000 | Temporary; US-AR; IRS-INST line 15 |
| A-03: Reverse book depreciation | +20,000 | Temporary; US-ASSET |
| A-04: Deduct tax depreciation | −40,000 | Temporary; US-ASSET; IRS-INST line 20; Form 4562 |
| **Taxable income before NOL/special deductions** | **122,000** | Page 1, line 28 |
| NOL and special deductions | 0 | Explicit fixture fact (line 29c) |
| **Taxable income** | **122,000** | Page 1, line 30 |
| **Regular federal tax** | **25,620** | 122,000 × 21%; Schedule J, Part I |

Direct check: deductions are `50,000 + 100,000 + 36,000 + 16,000 + 40,000 + 37,000 = 279,000`; taxable income is `401,000 − 279,000 = 122,000`. The 37,000 other-deductions statement comprises insurance 6,000, professional fees 14,000, subscriptions 8,000, utilities 4,000 and deductible meals 5,000. Do not add the reconciliation adjustments again to that direct result.

### D. Deferred tax and valuation allowance

| Item | Closing carrying amount | Closing tax base | Temporary difference | Rate | Closing gross deferred balance |
| --- | ---: | ---: | --- | ---: | ---: |
| Receivables, net of allowance | 68,000 | 80,000 | Deductible 12,000 | 21% | DTA 2,520 |
| Equipment, net of depreciation | 80,000 | 60,000 | Taxable 20,000 | 21% | DTL 4,200 |
| Meals (permanent) | — | — | None | — | 0 |

Opening DTA and DTL are zero. The receivables item creates a deferred benefit of 2,520; the equipment item creates deferred expense of 4,200. The fixture's supported-realization assumption yields a zero valuation allowance. **Net deferred expense and net noncurrent DTL are both 1,680** in this P&L-only case. In a real case they need not be equal, because opening balances and non-P&L movements matter.

### E. Proposed entries and reporting amounts

All entries are `PENDING_REVIEW / NOT_POSTED`. Map account names to the client's approved chart.

| JE | Debit account | Debit | Credit account | Credit |
| --- | --- | ---: | --- | ---: |
| JE-01 | Current income-tax expense | 25,620 | Federal income tax payable | 25,620 |
| JE-02 | Deferred tax asset — receivables | 2,520 | Deferred income-tax benefit | 2,520 |
| JE-03 | Deferred income-tax expense | 4,200 | Deferred tax liability — equipment | 4,200 |

```text
Current tax expense                           25,620
Deferred tax expense, net                      1,680
Total income-tax expense                      27,300
Pretax book income                           125,000
After-tax book income                         97,700
Effective tax rate                    27,300 / 125,000 = 21.84%
```

ETR check: `125,000 × 21% = 26,250`; permanent meals effect `5,000 × 21% = 1,050`; total 27,300. Timing differences shift expense between current and deferred; under this fixture they do not change total tax expense.

Gross current payable is 25,620 and prepaid tax is 20,000, leaving 5,620 before any penalty or interest. Applying the prepayment against the payable is a separate proposed entry (`Dr Federal income tax payable 20,000 / Cr Federal estimated-tax prepayments 20,000`), subject to approval; it creates no new cash outflow and no new expense.

For the single federal tax-paying component, net deferred presentation is a noncurrent DTL of 1,680. Closing retained earnings are `69,000 + 97,700 = 166,700`. After the prepayment offset and net deferred presentation: assets 254,000; liabilities `40,000 + 5,620 + 1,680 = 47,300`; equity `40,000 + 166,700 = 206,700`. The balance sheet balances. This supports the fixture, not a complete financial-statement presentation opinion.

### F. Selected Form 1120 (2025) mapping

Descriptions are shortened; all entries remain draft. IRS-FORM controls exact labels, line numbering and any required printed zero. Line numbers below were checked against current IRS instructions during preparation; re-verify against the final 2025 revision before use.

| Form/schedule | Line(s) | Draft amount | Source / formula |
| --- | --- | ---: | --- |
| Page 1 | 1a / 1b / 1c | 400,000 / 0 / 400,000 | US-TB revenue; no returns or allowances |
| Page 1 | 2 / 3 | 0 / 400,000 | No cost of goods sold |
| Page 1 | 5 / 11 | 1,000 / 401,000 | Interest income / total income |
| Page 1 | 12 / 13 | 50,000 / 100,000 | Officer compensation / salaries and wages |
| Page 1 | 15 | 0 | No qualifying current bad-debt deduction (US-AR) |
| Page 1 | 16 / 17 | 36,000 / 16,000 | Rents / taxes and licenses (employer payroll taxes) |
| Page 1 | 20 | 40,000 | US-ASSET; Form 4562 must be completed and attached |
| Page 1 | 26 / 27 | 37,000 / 279,000 | Other-deductions statement / total deductions |
| Page 1 | 28 / 29c / 30 | 122,000 / 0 / 122,000 | Taxable-income bridge |
| Schedule J, Part I | Income tax line / 12 | 25,620 / 25,620 | Regular tax; no CAMT, BEAT, recapture or other components |
| Page 1 | 31 | 25,620 | Total tax = Schedule J, Part I, line 12 |
| Schedule J, Part III | 14 / 23 | 20,000 / 20,000 | US-PAY current-year estimated payments / total payments and credits |
| Page 1 | 32 | — | Reserved for future use on current revisions; leave blank |
| Page 1 | 33 | 20,000 | Total payments and credits = Schedule J, Part III, line 23 |
| Page 1 | 34 | UNRESOLVED | Estimated-tax penalty from Form 2220; requires installment dates (US-PAY) |
| Page 1 | 35 / 36 | UNRESOLVED / — | Amount owed = line 31 + line 34 − line 33; numeric field null until line 34 resolves |
| Schedule M-1 | 1 / 2 | 97,700 / 27,300 | Net income per books after proposed provision / federal income tax per books (current + deferred) |
| Schedule M-1 | 5a / 5c / 5 other | 20,000 / 5,000 / 12,000 | Book depreciation / nondeductible meals / book allowance expense |
| Schedule M-1 | 6 | 162,000 | 97,700 + 27,300 + 20,000 + 5,000 + 12,000 |
| Schedule M-1 | 8a / 9 / 10 | 40,000 / 40,000 / 122,000 | Tax depreciation / total / ties to page 1, line 28 |

Schedule M-1 assumes the proposed provision is accepted into the final book baseline; if approval changes the provision, refresh book net income and the tax add-back together. The gross depreciation presentation adds back book depreciation (5a) and deducts tax depreciation (8a); do not additionally apply the net 20,000 difference.

The 5,620 payment difference is **not** a final amount owed: US-PAY lacks installment dates, so the Form 2220 penalty and the dependent line 35 remain unresolved. Form 1120 header, Schedule K (including the total-receipts/total-assets question that determines whether Schedules L, M-1 and M-2 must be completed — here total assets of 254,000 exceed the 250,000 threshold, so they are required), Schedule L, Schedule M-2, Form 4562 and ownership disclosures are not completed here.

### G. Reviewer handoff and negative variants

| Issue | Action / effect |
| --- | --- |
| Tax depreciation input | Validate method, dates, bonus/§179 elections; affects current tax, DTL and Form 4562 |
| Credit-loss allowance | Confirm future deductibility and realization evidence; affects DTA/allowance |
| Payments/penalties | Obtain installment dates and prior-year tax for the Form 2220 safe harbor; line 35 unresolved |
| Filing status | Confirm whether the 2025 return was filed or extended; quantify late-filing/late-payment exposure if neither |
| Return completeness | Resolve state/foreign applicability, Schedule K, Schedules L/M-2 and attachments |
| GAAP reporting | Confirm enacted-rate measurement, allocation, adoption status and disclosure checklist |

**Valuation-allowance variant.** If new evidence supports realization of only half the 2,520 DTA, the proposed allowance is 1,260 (`Dr Deferred tax expense / Cr Valuation allowance`). Deferred expense becomes 2,940, total tax expense 28,560 and ETR 22.848%. Taxable income and current tax stay at 122,000 and 25,620. This is a supplied judgment scenario, not an automatic forecast conclusion.

**Imbalance variant.** Add 100 to cash's debit with no offset. Debits become 582,100; credits remain 582,000. Step 2's gate withholds affected tax totals until reconciled; do not force a balancing entry.

---

## 10. Acceptance tests

| ID | Test | Required behavior |
| --- | --- | --- |
| US-01 | Run the main fixture | Reproduce current tax 25,620, DTA 2,520, DTL 4,200, total tax expense 27,300, ETR 21.84% |
| US-02 | Add the 100 TB imbalance | Detect the difference; withhold dependent totals |
| US-03 | Attempt deferred tax on meals | Reject; the meals difference is permanent |
| US-04 | Apply the net depreciation adjustment after gross M-1 adjustments | Detect double counting; taxable income remains 122,000 |
| US-05 | Substitute 20,000 of payments for tax expense | Reject; preserve current/deferred expense and payable reconciliation |
| US-06 | Remove tax bases/opening balances | Hold affected deferred balances; do not default to zero |
| US-07 | Run the half-realization variant | Allowance 1,260; tax expense 28,560; current tax unchanged |
| US-08 | Use a proposed but unenacted rate | Flag unsupported U.S. GAAP measurement |
| US-09 | Use a weighted-average UTP benefit without a recognition test | Require recognition, then correct measurement |
| US-10 | Net different components/jurisdictions | Reject improper deferred netting |
| US-11 | Supply a 2026 form request with 2025 line mapping | Re-verify form/rules; no silent reuse |
| US-12 | Treat private-entity 2025 ASU 2023-09 adoption as mandatory | Apply the status and effective-date gate |
| US-13 | Remove payment dates | Keep supported total; Form 2220 penalty and line 35 unresolved |
| US-14 | Preparation date after the extended due date | Flag filing status as unresolved; require late-filing exposure analysis before stating amounts owed |
| US-15 | Change the dataset after review | New version and renewed review of affected content |
| US-16 | Request posting/filing under this module alone | Deliver proposed entries and draft return support; require separately authorized execution |

**Execution record.** The fixture arithmetic, current/direct/M-1 bridges, journal balance, closing balance sheet, half-realization variant and 100-imbalance detection were independently recalculated on November 2, 2026 and matched expectations. Form 1120 line references (lines 31–35, Schedule J lines 12/14/23) were checked against current IRS instructions on the same date. This is document-fixture validation, not a deployed automation, legal opinion or CPA approval. Other behavioral tests remain `NOT_TESTED` until an implementation records evidence.

---

## 11. Version history

| Version | Date | Change | Review status |
| --- | --- | --- | --- |
| 0.1 source | 2026-11-02 | Original `02_tax.md` tax-preparation workflow | Preserved as source |
| 0.2 | 2026-11-02 | U.S. GAAP/ASC 740 specialization; current/deferred accounting, realization/UTP controls, disclosure applicability, proposed journals, return linkage, tested fixture | Draft; professional review pending |
| 0.3 | 2026-11-02 | Editorial polish; corrected page 1 line 32/33 mapping (removed non-existent "section 1062" reference; line 32 is reserved); added filing calendar, late-filing timing note, 2025 law-change verification list, Schedule K completion threshold, Form 2220/estimated-tax sources, filing-status controls and test US-14 | Draft; professional review pending |

Maintain client configuration separately from the reusable core. On revision, record changed authority, effective dates, calculations, test evidence and reviewer acceptance.
