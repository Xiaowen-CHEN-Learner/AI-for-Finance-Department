# 2.2 — IFRS Income-Tax Reporting and Hong Kong Profits-Tax Support

**Project:** AI for Finance Department
**Module ID:** `2.2_HK_IFRS_tax`
**Workflow version:** `0.2` (developed from `02_tax.md` v`0.1`)
**Source review date:** November 2, 2026
**Owner:** Finance workflow owner; assigned per engagement
**Reporting focus:** IFRS Accounting Standards, principally IAS 12 and IFRIC 23. Engagements expressly configured for full HKFRS use HKAS 12 and HK(IFRIC)-Int 23.
**Tax focus:** Hong Kong corporate profits tax under the Inland Revenue Ordinance (IRO), with BIR51 preparation support
**Reviewers:** Financial reporting controller and Hong Kong CPA/tax adviser, named per engagement
**Default status:** `DRAFT — FOR PROFESSIONAL REVIEW — NO POSTING OR FILING`
**Demonstration:** IFRS reporting at March 31, 2026; Hong Kong year of assessment (YA) 2025/26; return preparation dated after a subsequent tax-law change

This standalone Markdown workflow extends the original tax-return support module to cover income-tax accounting, proposed journals, and reporting disclosures. It specifies procedures and evidence requirements; calculations, workbook creation, and form population require appropriate tools. It does not certify IFRS compliance and does not constitute a completed tax return.

## 1. Purpose and supported scope

### 1.1 Role and objective

Act as a finance-department tax support analyst. From one controlled accounting dataset, produce two linked sets of working papers:

1. **Financial reporting:** current income-tax expense, deferred tax assets (DTAs) and liabilities (DTLs), recoverability conclusions, uncertain tax treatments, proposed journal entries, effective tax rate (ETR), and draft tax-note information.
2. **Hong Kong tax preparation:** book-to-assessable-profit reconciliation, loss and allowance schedules, BIR51 mapping, final/provisional tax reconciliation, missing-information list, and tax-adviser questions.

Accounting standards determine financial-statement recognition, measurement, presentation, and disclosure. The IRO and applicable IRD guidance determine assessable profits and tax obligations. Neither book profit nor an IFRS recognition decision establishes tax treatment on its own.

### 1.2 Reporting-basis selection

The default basis is **full IFRS Accounting Standards**. Record the actual basis of the client's accounts: Hong Kong incorporation or a Hong Kong tax filing does not by itself establish that the accounts use IFRS. Where the engagement expressly selects full HKFRS, apply HKAS 12 and HK(IFRIC)-Int 23 and confirm their editions and effective amendments. Never silently substitute HKFRS for Private Entities, SME-FRF/SME-FRS, or another framework; route any other basis for separate configuration. The IRD accepts financial statements prepared under specified accounting frameworks as the starting point for the tax computation, subject to tax adjustments. [S01–S04, S08]

### 1.3 Supported scope

| Workstream | Included | Separate specialist configuration when relevant |
| --- | --- | --- |
| IFRS income-tax reporting | Current/deferred tax schedules, recognition review, uncertainty assessment, journal proposals, tax-note support | Business combinations, complex investments, unusual initial-recognition exceptions, foreign currencies, multiple jurisdictions |
| Hong Kong profits tax | Ordinary corporate BIR51 preparation support and two-tier eligibility review | Concessionary regimes, restructurings, transfer pricing, treaty claims, detailed FSIE and Pillar Two computations |
| Book/tax integration | Evidence-linked permanent and temporary differences; return-to-provision analysis | Corrections to the underlying revenue, expense, asset, or provision accounting |
| Execution | Draft working papers and review questions | Filing, signatures, tax payments, portal submissions, and ledger posting are outside this module |

The core case is a domestic operating corporation. Screen for other obligations rather than treating that scope as proof of exemption. This module does not prepare salaries tax, employer's returns, property tax, stamp duty, or other filings, but dependencies on them must be flagged.

### 1.4 Invocation

> Run 2.2_HK_IFRS_tax.md using the attached configuration, trial balance, tax schedules, forecasts, and IRD documents. Confirm the financial reporting date separately from the year of assessment and the preparation date. Prepare the IFRS tax provision and Hong Kong tax working papers, reconcile them, and show sources, proposed journals, uncertainties, missing items, and reviewer questions. Leave unknown values explicit. Do not post, sign, file, or pay.

## 2. Inputs and required documents

### 2.1 Engagement configuration

```yaml
engagement:
  client_id: null
  entity_id: null
  legal_name: null
  business_registration_reference: null  # Secure reference; mask in general output
  ird_file_reference: null
  legal_entity_type: null
  tax_jurisdiction: "Hong Kong"
  financial_reporting_framework: "IFRS Accounting Standards"
  reporting_framework_confirmed: false
  reporting_period_start: null
  reporting_period_end: null
  financial_statements_authorisation_date: null
  reporting_standard_edition_and_amendments: null
  hk_year_of_assessment: null             # E.g. 2025/26; confirm separately
  basis_period_start: null
  basis_period_end: null
  basis_period_type: null                # Ordinary / commencement / cessation / change
  return_type: null                      # Original / amendment support
  preparation_as_of: null
  tax_form: "BIR51"
  issued_return_year_and_revision: null
  official_form_and_notes_verified_on: null
  return_issue_date: null
  filing_deadline_and_extension_evidence: null
  book_functional_currency: null
  presentation_currency: null
  return_currency: "HKD"
  fx_method_and_rate_evidence: null
  approved_trial_balance_version: null
  accounting_close_status: null
  source_cutoff: null
  dataset_version: null
  two_tier_eligibility: "UNCONFIRMED"
  connected_entity_list_reference: null
  two_tier_electing_entity_and_year: null
  special_regime_screening: "UNCONFIRMED"
  offshore_and_fsie_screening: "UNCONFIRMED"
  pillar_two_hkmtt_screening: "UNCONFIRMED"
  tax_loss_and_credit_status: "UNCONFIRMED"
  opening_current_and_deferred_tax_reference: null
  future_taxable_profit_forecast_reference: null
  current_tax_offset_evidence: null
  deferred_tax_offset_evidence: null
  preparer_name: null
  controller_name: null
  hk_tax_reviewer_name: null
  output_version: "v0.2"
  permitted_data_environment: null
  retention_policy_reference: null
```

Never infer a YA from the upload date. An ordinary accounting year ending March 31, 2026 forms the basis period for YA 2025/26; other accounting dates, commencements, cessations, and changes of accounting date require their own analysis. Record the reporting date, basis period, YA, and settlement dates independently. [S05]

### 2.2 Required-document checklist

| Document group | Typical evidence | Key use |
| --- | --- | --- |
| Entity and ownership | Incorporation/registration, ownership chart, connected entities, business activities | Taxpayer identification, two-tier eligibility, group screening |
| Accounting baseline | Approved adjusted TB, ledger, financial statements, chart of accounts, approved journals | Reconciled book results and carrying amounts |
| Prior tax position | Filed returns, computations, assessments, loss statements, objections, correspondence | Opening positions and return-to-provision differences |
| Asset tax bases | Fixed-asset register, tax pools, additions/disposals, depreciation allowances | Tax bases, current allowances, temporary differences |
| Provisions and accruals | Contracts, payment/settlement evidence, provision calculations | Timing and eventual tax deductibility |
| Source and exemptions | Transaction contracts, performance locations, decision-making records, income receipts | Territorial-source and FSIE analysis |
| Forecasts | Approved taxable-profit forecasts, reversal schedule, support for assumptions | DTA recognition and expected deferred-tax rates |
| Payments | Demand notes, provisional assessments, payment receipts, allocation records, holdover decisions | Separation of tax expense, assessed amounts, and cash paid |
| Special matters | Related-party transactions, losses/credits, non-resident payments, incentives, MNE group revenue | Required schedules and specialist referrals |
| Reporting governance | Tax policies, materiality, audit/review instructions, authorisation date | Reporting judgements and sign-off |

Each document request states applicability, source ID, period, received/missing status, owner, affected output, and next action. Use masked identifiers in review summaries and synthetic data in demonstrations. Never put confidential client details into public searches. Retain originals and work only in the approved client environment.

## 3. Output files and schemas

### 3.1 Default output package

Produce `{client_id}_{entity_id}_{YA}_{output_version}_HK_IFRS_tax_review.md` with these sections:

1. Scope, dates, framework, dataset/form versions, and readiness status.
2. Source register and missing-document checklist.
3. Book-to-tax computation, losses, allowances, and estimated final tax.
4. IAS 12 provision, tax-base schedules, DTA recognition evidence, and uncertainties.
5. Proposed balanced journals, ETR bridge, presentation decisions, and tax-note checklist.
6. BIR51 mapping and final/provisional/paid-tax reconciliation.
7. Open issues, validation results, and separate controller and tax-adviser approval records.

An Excel workbook, structured CSV exports, or a populated draft form may be added when requested and supported. A field-mapping table is not an edited return, and a reference specimen is never a filing document. Tie every format to the same dataset and output version.

### 3.2 Minimum schemas

| Schedule | Required fields |
| --- | --- |
| `sources` | ID, file/embedded section, version, entity, period, exact locator, numerical or corroborating role, receipt date, verification status |
| `tax_rules` | rule ID, jurisdiction, YA/effective period, authority/section, retrieval date, substantive-enactment date, enactment date, reporting-date applicability |
| `book_to_tax` | adjustment ID, account, book amount, signed adjustment, permanent/temporary/uncertain class, timing, evidence, authority, review status |
| `deferred_tax` | item ID, entity/jurisdiction, carrying amount, tax base, temporary difference and type, opening DTA/DTL, reversal period, expected rate, recognition support, closing DTA/DTL, P&L/OCI/equity movement |
| `dta_support` | deduction/loss category, available amount, permitted utilisation, forecast and version, reversal evidence, recognised and unrecognised amounts, sensitivity, reviewer |
| `uncertainties` | position ID, issue and facts, unit of account, acceptance assessment, method, outcomes/probabilities, estimate, current/deferred effects, evidence, review status |
| `journals` | entry/line ID, date, account, debit, credit, currency, provision schedule, P&L/OCI/equity destination, approval, posting status |
| `form_mapping` | form/revision/YA, page/item, official label, value, display value, formula, source locator, adjustment links, data and review status |
| `payments` | assessment ID, YA, final/provisional type, charged amount, paid amount and date, credited amount, notice/receipt, remaining amount, next-year allocation |
| `checks_and_issues` | ID, expected/actual result, status, impact, resolution owner, action and date, evidence |

### 3.3 Status vocabulary

- **Data:** `SUPPORTED`, `CALCULATED`, `CONFIRMED_ZERO`, `NOT_APPLICABLE`, `MISSING`, `CONFLICT`
- **Review:** `PENDING_CONTROLLER`, `PENDING_TAX_ADVISER`, `APPROVED_BY_NAMED_REVIEWER`, `CHANGES_REQUIRED`
- **Package:** `INTAKE_INCOMPLETE`, `DRAFT_WITH_OPEN_ITEMS`, `READY_FOR_REVIEW`, `REVIEWED_DRAFT`
- **Validation:** `PASS`, `FAIL`, `NOT_TESTED`, `NOT_APPLICABLE`

Unknown numeric data remain null, with the reason recorded in a separate field. Where an official form prescribes a fallback entry, preserve the underlying unknown in the working paper and document both the rule and the reviewer's decision; a displayed zero is not evidence that a balance is zero. Retain source precision in working papers, then omit cents on BIR51 as its instructions require, and record the conversion and display treatment. Do not import U.S. rounding conventions. [S08]

## 4. Workflow

### Step 1 — Confirm scope, framework, and the three dates

Identify the financial reporting date, the tax basis period and YA, and the preparation date. Confirm IFRS versus full HKFRS and obtain the applicable standard text and edition. Capture the issued return, notices, source cutoff, and reviewer identities. Missing scope information blocks affected calculations; document inventory can continue.

Maintain a tax-law timeline. A measure known at the preparation date may not have been enacted or substantively enacted at the reporting date. HKICPA guidance treats passage of a bill through the Legislative Council's Third Reading as substantive enactment; a Budget announcement alone is insufficient. Assess subsequent-event disclosure where appropriate. [S04]

### Step 2 — Freeze the accounting baseline

Reconcile the TB, ledger, financial statements, opening tax balances, and approved adjustments. Establish whether any tax expense is already recorded and whether book income is pre-tax or after tax. Proposed entries stay outside the approved ledger until authorised.

Record exact source locators and distinguish ledger amounts from corroborating invoices: an invoice already reflected in the ledger must not be added again. Quarantine duplicates, entity or period mismatches, uncertain OCR, incomplete pages, and unsupported FX conversions. An unexplained TB imbalance blocks dependent tax and provision totals. Never use a plug.

### Step 3 — Establish Hong Kong tax applicability

Build an issue-specific register rather than applying a blanket "Hong Kong income" label:

- Identify the activities producing each income stream and the source facts supporting them. Customer location, place of incorporation, invoice currency, or place of remittance alone does not settle source.
- Review foreign-sourced interest, dividends, IP income, and disposal gains under the FSIE regime where an MNE entity is involved. The regime is not limited to large-revenue groups; do not confuse its scope with the Pillar Two threshold. Identify accrual and receipt years, applicable exceptions, and supplementary reporting. [S10]
- Establish two-tier eligibility for the entity and YA, including connected entities, the nominated entity, and excluded or concessionary categories. Do not give each group company its own reduced-rate band without review. [S06]
- Screen group revenue and structure for Pillar Two and the Hong Kong minimum top-up tax (HKMTT). IRD describes the EUR 750 million, two-of-four-years test and application to fiscal years beginning on or after January 1, 2025. Route in-scope computations to a specialist; 15% is not a general Hong Kong corporate rate. Apply the IAS 12 Pillar Two exception and disclosures when relevant. [S01, S11]
- Identify losses, foreign tax relief, related-party transactions, non-resident payments, special deductions, and elections. Maintain losses by legal taxpayer and category; never pool group losses without an identified legal mechanism and specialist approval.

### Step 4 — Build the current-tax computation

Start from pre-tax book profit wherever possible. Add back non-deductible and unsupported expenses and book depreciation; deduct only supported tax allowances and other supported adjustments. Evaluate each provision on its facts: not every accrual is disallowed and not every cash payment is deductible. Analyse actual expenditure under the IRO and IRD guidance; U.S. conventions such as partial meal deductibility have no place in a Hong Kong computation. [S05, S08]

Keep permanent differences, temporary differences, and unresolved treatments separate. A tax allowance may give rise to a temporary difference, but the year-end deferred balance is derived from carrying amounts and tax bases, not from the current-year adjustment total.

```text
Book profit before income tax
+ signed current-year adjustments
= assessable profits before losses brought forward
- allowable losses utilised, supported by the loss schedule
= profits used for the tax calculation
```

Map BIR51 item 1.1 before losses brought forward and record item 1.3 separately. When starting from after-tax book income, add back both current and deferred income-tax expense to restore the pre-tax starting point; do not add them again if already starting from pre-tax income. [S07–S08]

For an eligible ordinary corporation, apply 8.25% to the first HK$2 million of assessable profits and 16.5% to the remainder; otherwise determine the applicable standard or concessionary treatment. Treat any year-specific final-tax reduction as a separate step, recording its reporting-date and tax-return-date applicability. Do not carry a one-off reduction into provisional or deferred-tax calculations without applicable authority. [S06, S09]

### Step 5 — Prepare the IAS 12 deferred-tax schedule

For every relevant asset, liability, and loss or credit category:

1. Reconcile the carrying amount to the approved reporting dataset and establish its tax base from the legal treatment and tax schedules.
2. Classify the resulting taxable or deductible temporary difference. For an asset, a carrying amount above its tax base normally produces a taxable difference; a liability whose settlement is deductible in future produces a deductible difference. Do not apply one sign formula to both assets and liabilities.
3. Assess recognition exceptions and special rules. Examine leases, decommissioning obligations, business combinations, investments, and initial recognition on their facts rather than copying a legacy exemption policy. The IAS 12 amendments address equal taxable and deductible differences arising from a single transaction. [S01]
4. Schedule reversals and the expected manner of recovery or settlement. Use rates and laws enacted or substantively enacted at the reporting date. Where two-tier rates apply, estimate the **average rate on expected taxable profits, including reversals**, for each relevant future period. Neither 8.25% nor 16.5% is an automatic deferred-tax rate. [S04, Q4]
5. Recognise a DTA only to the extent that sufficient future taxable profit is probable. Reconcile the sources of utilisation, avoid double-counting taxable reversals and forecast profits, and retain convincing evidence where there is a history of losses. Track unrecognised amounts and reassess at each reporting date. This is an IFRS recognition assessment, not a U.S.-style valuation allowance. [S01; IAS 12 paragraphs 24, 28–37, 56]
6. Calculate undiscounted closing recognised balances and explain the movement by origination/reversal, rate change, recognition change, acquisition, FX, and destination. [IAS 12 paragraphs 47–56]

In a simple case, an increase in the net deferred liability is deferred tax expense when every movement belongs in P&L. Never infer P&L expense from the balance movement until OCI, equity, acquisition, FX, and other movements have been identified.

### Step 6 — Assess uncertain tax treatments

Apply IFRIC 23, or its HKFRS equivalent where expressly selected. Decide whether positions are assessed separately or together, and assume the tax authority examines with full knowledge of all relevant information. If acceptance is probable, use the supported filing treatment. Otherwise select the most likely amount or the probability-weighted expected value, whichever better predicts resolution. Use consistent assumptions for the affected current and deferred tax and reassess when facts change. Document the reviewer's reasoning; do not invent probabilities or import a U.S. cumulative-probability method. [S02–S03; IFRIC 23 paragraphs 6–14]

Keep the accounting estimate distinct from the tax-adviser-approved filing position. Evaluate the classification of related interest and penalties under the applicable standards and accounting policy; not every charge belongs in income-tax expense.

### Step 7 — Prepare reporting outputs and journal proposals

Present current tax for the period, adjustments relating to prior periods, deferred tax, and amounts recognised outside P&L separately. Allocate tax consistently with the underlying transaction under IAS 12, considering OCI and equity rather than sending every adjustment to P&L.

Propose entries with exact account mappings and a debit/credit check. Review existing provision journals first to avoid duplication. Reconcile current tax assets and liabilities and deferred balances to opening balances, expense, payments, adjustments, and closing balances.

Prepare a presentation memo. Deferred balances are non-current where current/non-current classification is used. Test current-tax and deferred-tax offset criteria separately: current-tax offset requires a legally enforceable right and an intention to settle net or simultaneously; deferred offset also depends on taxation authority and entity conditions, and group membership alone is insufficient. Never offset current tax against deferred tax. [S01; IAS 12 paragraphs 71–76; applicable presentation standard]

Draft tax-note support: current and deferred components, a quantified rate or amount reconciliation, significant temporary-difference categories, recognised and unrecognised DTA and loss data, significant judgements and uncertainties, and relevant tax-law changes. Check required disclosures against the current standard, including Pillar Two where applicable. This is a tax-note checklist, not a claim that the financial statements as a whole comply with IFRS.

### Step 8 — Reconcile assessments, provisional tax, and cash

Keep five amounts separate: financial-reporting tax expense, the current final-tax estimate, provisional tax **charged**, provisional tax **paid or credited**, and the following year's provisional charge. The BIR51 notes instruct that the Part 2 computation include the following year's provisional tax and deduct the provisional tax charged for the current year. The settlement ledger must still distinguish paid from unpaid. [S08]

Use demand notes and allocation evidence. Do not treat final tax less cash paid as BIR51 item 2.1 or as the full amount payable on an assessment. Record holdover applications and decisions separately; an application is not an approval. Obtain notice-specific dates before stating any payment deadline.

### Step 9 — Map, validate, and hand over

Verify the issued BIR51 revision, all required supporting documents, supplementary forms, and electronic-filing applicability. The current reference specimen supports the selected mappings in the worked example; a real engagement must use the actual issued return or portal schema. Leave signatures and representative authorisations to the authorised parties. [S07–S08]

Generate source-linked mappings, exceptions, professional decisions required, and actual test results. New data, law changes, or mapping changes require a new output version and renewed review of affected content. Use the project's shared controls where supplied; otherwise use the controls embedded in this file without inventing shared-file contents.

## 5. Assumptions and source hierarchy

### 5.1 Evidence policy

Use official standards and legislation for rules, official authority and standard-setter guidance for interpretation, and client records for facts. The approved ledger establishes the numerical baseline but does not prove tax deductibility. Prior returns provide continuity, not authority for current treatment.

For each material judgement, record source ID, exact paragraph/section/item, edition, effective period, access date, factual dependency, and review status. Preserve assumptions as assumptions. Never assume the absence of losses, overseas income, connected entities, or other taxes merely because records were not supplied.

### 5.2 Official reference register

Links were reviewed on November 2, 2026. Recheck them for every client period. The professional reviewer must have access to the full IFRS/HKFRS text and amendments; some public full-standard links were subscription-restricted or unavailable during preparation. This workflow relies on official public summaries, accessible HKICPA guidance, and identified paragraph references; it does not claim exhaustive verification against current full-standard text.

| ID | Source | Relevant use |
| --- | --- | --- |
| S01 | [IFRS Foundation — IAS 12](https://www.ifrs.org/issued-standards/list-of-standards/ias-12-income-taxes/) | Current/deferred tax framework and amendment history; paragraphs 24–37, 46–61A, 71–87 and Pillar Two provisions |
| S02 | [IFRS Foundation — IFRIC 23](https://www.ifrs.org/issued-standards/list-of-standards/ifric-23-uncertainty-over-income-tax-treatments/) | Uncertainty framework; paragraphs 6–14 |
| S03 | [HKICPA — HK(IFRIC)-Int 23](https://www.hkicpa.org.hk/-/media/HKICPA-Website/Members-Handbook/volumeII/hkifricint23.pdf) | Official interpretation; direct PDF unavailable in this review — obtain current text before relying on it |
| S04 | [HKICPA — HKAS 12 FAQ](https://www.hkicpa.org.hk/en/Tools/FAQ/Standards/HKFRS/HKAS-12-Income-Taxes) | Q1–Q2 substantive enactment; Q3–Q4 two-tier deferred-tax measurement |
| S05 | [IRD — Profits Tax](https://www.ird.gov.hk/eng/tax/bus_pft.htm) | Basis periods, deductions, allowances, losses, and ordinary rates; read with FSIE updates |
| S06 | [IRD — Two-tiered Profits Tax Rates FAQ](https://www.ird.gov.hk/eng/faq/2tr.htm) | Rates, eligibility, connected entities, and elections |
| S07 | [IRD — 2025/26 specimen hub](https://www.ird.gov.hk/eng/tax/bus_returnspecimen.htm) and [BIR51 specimen](https://www.ird.gov.hk/eng/pdf/ebir512.pdf) | Specimen for the 2025/26 exercise; retrieved PDF footer BIR51 (4/2025); reference only |
| S08 | [IRD — BIR51 notes](https://www.ird.gov.hk/eng/tax/bir51e_notes.htm) and [specimen notes PDF](https://www.ird.gov.hk/eng/pdf/e51notes2.pdf) | Introduction, Parts 1, 2, 11, and 12; item 12.18 before-tax definition |
| S09 | [IRD — 2026/27 Budget tax measures](https://www.ird.gov.hk/eng/tax/budget.htm) | YA 2025/26 final-tax reduction, legislative dates, provisional-tax distinction |
| S10 | [IRD — Foreign-sourced Income Exemption](https://www.ird.gov.hk/eng/tax/bus_fsie.htm) | MNE scope, specified income, receipt, and exceptions |
| S11 | [IRD — Global minimum tax and HKMTT](https://www.ird.gov.hk/eng/tax/bus_beps.htm) | Group threshold, commencement, return and notification screening |
| S12 | [IRD — BIR51/BIR52 completion FAQ](https://www.ird.gov.hk/eng/faq/cpt51.htm) | Practical field definitions; question 176 confirms net profit per accounts is before tax |

The public IRD profits-tax overview contains broad territorial-source statements; do not use a general sentence from it to override the later, specific FSIE rules. Resolve apparent conflicts by date, scope, law, and adviser review.

## 6. Validation and reconciliation controls

| Control | Required evidence / result |
| --- | --- |
| Scope and dates | Reporting date, basis period, YA, issued form, preparation date, and law-effective dates agree |
| Financial baseline | Debits equal credits; GL, statements, schedules, and opening balances reconcile |
| Provenance | Every figure has a source locator or reproducible formula; no invoice/TB double counting |
| Current-tax bridge | Pre-tax and after-tax starting points give the same assessable profits |
| Losses and allowances | Current movement and carry-forward reconcile; legal-taxpayer restrictions preserved |
| Temporary differences | Carrying amounts and tax bases reconcile independently of current-year adjustments |
| Deferred rate | Reversal-year taxable-profit forecast and eligibility justify each average rate |
| DTA recognition | Probable-recovery evidence documented; unrecognised amounts retained and reassessed |
| Uncertainty consistency | Current/deferred assumptions and filing-versus-accounting differences explained |
| Roll-forward | Opening balances plus all movements equal closing balances; P&L separated from OCI, equity, and other |
| Journals | Debits equal credits; proposed/unposted status and human approval explicit |
| ETR | Tax-note bridge ties to P&L tax expense; denominator is defined pre-tax profit |
| Assessment and cash | Final, provisional charged, paid, credited, and following-year amounts kept separate |
| Form consistency | BIR51 items agree with verified definitions, including before-tax item 12.18 |
| Timing | A later law change is not inserted retrospectively into an earlier reporting-date provision |
| Version and review | Every export identifies dataset, rules version, reviewer status, and unresolved items |

Require zero unexplained arithmetic difference at stored precision. Disclose prescribed display rounding or truncation separately. Materiality never permits hiding an unexplained discrepancy. A balance check does not establish tax eligibility, DTA recoverability, or return completeness.

## 7. Exception handling and escalation

| Exception | Action | Owner |
| --- | --- | --- |
| Unknown IFRS/HKFRS basis or unavailable standard text | Continue intake; hold affected reporting conclusions | Controller / reporting specialist |
| Missing or ambiguous YA, basis period, or form | Request issued documents and scope confirmation | Tax adviser |
| Unreconciled TB, OCR conflict, duplicates | Quarantine and diagnose; hold dependent figures | Accountant / data owner |
| No two-tier group election evidence | Do not apply the reduced rate as fact; show labelled scenarios only | Tax adviser |
| DTA forecast not supportable | Leave recognition unresolved or present reviewer-supported unrecognised amount | Controller / tax reviewer |
| Budget proposal before or after reporting date | Determine enactment and substantive-enactment timeline before recognition | Reporting reviewer |
| Uncertain source, FSIE, treaty, or Pillar Two position | Document trigger, facts, and affected outputs; obtain specialist decision | International tax specialist |
| Missing demand note or allocation | Keep the complete payable/refund amount unresolved | Finance owner / tax adviser |
| Data or law changes after review | New version; rerun dependent calculations and review | Preparer / reviewers |

Severity labels: `BLOCKER` for missing information that prevents an affected calculation or a complete package; `REVIEW` for a supported calculation that needs judgement; `INFO` for a documented limitation. Continue useful unaffected work. Never invent an approval, tax position, filing deadline, or absent schedule.

## 8. Human review and approval gate

The finance owner confirms completeness and the accounting baseline. The controller reviews IFRS/HKFRS recognition, estimates, presentation, disclosures, and proposed journals. The Hong Kong tax adviser reviews source, deductions, allowances, elections, losses, returns, assessments, and tax-law timing. Obtain specialist review for escalated matters.

- [ ] Confirm financial reporting basis and effective standards and amendments.
- [ ] Confirm reporting date, YA, basis period, and law timeline.
- [ ] Approve supported book-to-tax adjustments and tax-base schedules.
- [ ] Review two-tier eligibility, reversal rates, and DTA recognition evidence.
- [ ] Review uncertain tax treatments and specialist conclusions.
- [ ] Reconcile current/deferred balances, ETR, journals, and draft disclosures.
- [ ] Resolve issued-return mappings, supplementary forms, and payment notices.
- [ ] Resolve blockers and record separate reporting and tax decisions.

```text
Dataset / output version reviewed:
Controller name, role and review date:
Financial-reporting decisions / conditions:
Hong Kong tax reviewer name, qualification and review date:
Tax-preparation decisions / conditions:
Unresolved items and owner:
Evidence of human sign-off:
Journal posting authorisation: NOT PROVIDED unless separately documented
Filing/payment authorisation: OUTSIDE THIS MODULE
```

Leave this record blank until a person supplies a decision. Draft journals remain unposted. Do not contact reviewers, sign declarations, file returns, or make payments as an inferred next step.

## 9. Worked example (input → output)

### A. Fictional entity, dates, and evidence

**Entity:** Example HK Services Limited (`HK-DEMO-001`), a fictional ordinary corporation
**Framework:** Full IFRS Accounting Standards; income tax under IAS 12
**Reporting and basis period:** April 1, 2025 – March 31, 2026; YA 2025/26
**Preparation date:** November 2, 2026
**Currency:** HKD throughout
**Dataset:** `HK-DEMO-2025-26-v1`; all records below are embedded synthetic inputs
**Status:** `DRAFT_WITH_OPEN_ITEMS`; no accountant, CPA, or auditor approval is implied

Explicit fictional facts: Hong Kong-source ordinary service income; no connected entity; two-tier eligibility; no brought-forward losses; no foreign income or foreign tax credit; no special tax regime or Pillar Two obligation; no tax uncertainty affecting the fixture. These are stated assumptions, not inferences from missing records. The underlying book accounting is accepted as an input for the demonstration. A real engagement must substantiate each assumption.

| Source ID | Embedded evidence | Locator |
| --- | --- | --- |
| HK-TB | Pre-provision trial balance | Subsection B |
| HK-ASSET | Existing 20% tax pool; no additions or disposals in the year | Subsection C |
| HK-PROVISION | Warranty facts and future tax deduction | Subsection C |
| HK-FORECAST | Probable taxable profit, reversal, and eligibility assumptions | Subsection E |
| HK-PAY | YA 2025/26 provisional tax charged and paid: 250,000, allocated to this taxpayer and year | Subsection H |
| HK-FACTS | Explicit scope and eligibility assumptions | This subsection |

### B. Pre-provision trial balance

Current-year revenue and expense accounts are not closed. No current or deferred tax provision is yet recorded. Opening deferred tax is zero. All amounts are HKD.

| Account | Description | Debit | Credit |
| --- | --- | ---: | ---: |
| 1000 | Cash | 2,000,000 | 0 |
| 1100 | Trade receivables | 1,500,000 | 0 |
| 1200 | Provisional profits tax paid | 250,000 | 0 |
| 1500 | Equipment cost | 4,000,000 | 0 |
| 1590 | Accumulated depreciation | 0 | 1,800,000 |
| 2000 | Trade payables | 0 | 1,000,000 |
| 2100 | Other operating accruals | 0 | 250,000 |
| 2200 | Warranty provision | 0 | 100,000 |
| 3000 | Issued share capital | 0 | 1,000,000 |
| 3100 | Opening retained earnings | 0 | 600,000 |
| 4000 | Service revenue | 0 | 8,000,000 |
| 5000 | Supported ordinary operating costs | 4,500,000 | 0 |
| 5100 | Book depreciation | 300,000 | 0 |
| 5200 | Warranty expense | 100,000 | 0 |
| 5300 | Non-deductible regulatory penalty | 100,000 | 0 |
| **Total** | | **12,750,000** | **12,750,000** |

Book profit before tax: `8,000,000 − 4,500,000 − 300,000 − 100,000 − 100,000 = 3,000,000`.

### C. Current-tax adjustments and tax bases

**Equipment.** HK-ASSET states that the opening carrying amount and the opening tax written-down value of the pool were both 2,500,000. The 20% annual-allowance classification is a synthetic input; no initial allowance applies this year. Annual allowance: `2,500,000 × 20% = 500,000`. Closing carrying amount: 2,200,000. Closing tax base: 2,000,000. The 200,000 excess of carrying amount over tax base is a taxable temporary difference. In practice the client's asset classification must be verified; 20% is not a universal rate. [S05]

**Warranty provision.** HK-PROVISION states that the 100,000 liability is recognised in the books but, being an uncrystallised provision, is not deductible in this year's computation; qualifying actual settlement will produce a future deduction. Tax base: `100,000 − 100,000 = 0`, giving a deductible temporary difference of 100,000. This is the fixture's stated treatment, not a rule that every provision must be added back.

| Adjustment | Description | Signed amount | Classification | Source |
| --- | --- | ---: | --- | --- |
| HK-A01 | Regulatory penalty add-back | +100,000 | Permanent | HK-TB 5300; S08 Part 1 |
| HK-A02 | Book depreciation add-back | +300,000 | Temporary component | HK-TB 5100; HK-ASSET |
| HK-A03 | Tax depreciation allowance | −500,000 | Temporary component | HK-ASSET; S05 |
| HK-A04 | Warranty provision add-back | +100,000 | Temporary | HK-PROVISION |
| **Total** | | **0** | Permanent +100,000; net temporary −100,000 | |

```text
Book profit before income tax                    3,000,000
Penalty                                            100,000
Book depreciation                                  300,000
Tax depreciation allowance                        (500,000)
Warranty provision                                 100,000
Assessable profits before losses                 3,000,000
Losses brought forward utilised                          0
Profits used for tax calculation                 3,000,000
```

### D. March 31 provision versus later final-tax computation

At March 31, 2026, current tax under the two-tier regime is:

`2,000,000 × 8.25% + 1,000,000 × 16.5% = 330,000`

**Tax-law timeline.** The 2026-27 Budget of February 25, 2026 proposed a one-off reduction of YA 2025/26 final profits tax of 100%, capped at HK$3,000 per case. The Inland Revenue (Amendment) (Tax Concessions, Concessionary Deductions and Allowances) Bill 2026 was gazetted on March 6, 2026, passed its Third Reading on May 13, 2026, and was gazetted as an Ordinance on May 22, 2026. Under the HKICPA substantive-enactment principle, the measure was neither enacted nor substantively enacted at March 31, 2026, so it does **not** reduce the March 31 provision. Evaluate subsequent-event disclosure if the financial statements are authorised after May 13, 2026. [S04, S09]

For the return computation prepared after enactment, expected final profits tax is `330,000 − 3,000 = 327,000`. The reduction does not alter assessable profits, does not apply to provisional tax, and is not carried into the future deferred-tax rate. A later-period journal is proposed in subsection F; it does not revise the March 31 expense.

### E. Deferred tax and DTA support

HK-FORECAST assumes both temporary differences reverse in the following period and that the entity remains two-tier eligible. The equipment is assumed to be disposed of as a whole pool for its carrying amount of 2,200,000, before any following-year depreciation or allowance; against the opening tax pool of 2,000,000 this produces a balancing charge of 200,000 and no book gain. The warranty is settled for 100,000 in the same period with no further book expense and a supported tax deduction. A real engagement must verify disposal proceeds, timing, pool rules, and settlement evidence rather than assume full reversal from continued depreciation.

Expected taxable profits before reversals are 2,900,000. Adding the 200,000 taxable reversal and deducting the 100,000 warranty deduction gives expected taxable profits of 3,000,000. The taxable-profit and reversal schedule supports probable utilisation of the deductible difference; a real engagement requires the underlying forecast and evidence.

Expected average rate, applying HKICPA FAQ Q4: `330,000 ÷ 3,000,000 = 11%`. [S04]

| Item | Closing carrying amount | Tax base | Temporary difference | Expected rate | Recognised closing balance |
| --- | ---: | ---: | ---: | ---: | ---: |
| Equipment | 2,200,000 | 2,000,000 | 200,000 taxable | 11% | DTL 22,000 |
| Warranty liability | 100,000 | 0 | 100,000 deductible | 11% | DTA 11,000 |
| **Net deferred position** | | | | | **Net DTL 11,000** |

Opening deferred balances and non-P&L movements are zero under the fixture. The DTL origination gives 22,000 deferred expense; the DTA origination gives 11,000 deferred benefit; net deferred expense is 11,000. Do not replace the forecast-derived 11% with 16.5% or 8.25%.

### F. Proposed unposted journals and reporting totals

| Entry | Proposed account | Debit | Credit |
| --- | --- | ---: | ---: |
| HK-J01, March 31 | Current income-tax expense | 330,000 | 0 |
| HK-J01, March 31 | Current profits-tax liability | 0 | 330,000 |
| HK-J02, March 31 | Deferred income-tax expense | 22,000 | 0 |
| HK-J02, March 31 | Deferred tax liability | 0 | 22,000 |
| HK-J03, March 31 | Deferred tax asset | 11,000 | 0 |
| HK-J03, March 31 | Deferred income-tax benefit | 0 | 11,000 |

All entries balance and remain unposted. The 250,000 provisional payment is already in the input TB; do not debit the tax-paid asset again. Determine legally permitted presentation separately from maintaining gross ledger balances.

| Reporting metric at March 31, 2026 | HKD / rate |
| --- | ---: |
| Profit before tax | 3,000,000 |
| Current tax expense | 330,000 |
| Net deferred tax expense | 11,000 |
| **Total P&L income-tax expense** | **341,000** |
| **Profit after tax** | **2,659,000** |
| **ETR (total P&L tax ÷ pre-tax profit)** | **11.3667%** |
| Current tax less allocated prepayments, before offset review | 80,000 |
| Net deferred liability, before offset review | 11,000 |

**Tax-note amount bridge**

| Component | HKD |
| --- | ---: |
| Pre-tax profit × 16.5% reference rate | 495,000 |
| Two-tier benefit on the first 2,000,000 | (165,000) |
| Permanent penalty difference × 16.5% | 16,500 |
| Deferred measurement at 11% versus 16.5% on the net temporary balance | (5,500) |
| **Total tax expense** | **341,000** |

Cross-check from after-tax book income: `2,659,000 + 330,000 + 11,000 = 3,000,000` pre-tax profit; applying HK-A01 to HK-A04 again gives assessable profits of 3,000,000. Neither deferred tax expense nor the provisional payment enters the deductible-expense computation.

For the subsequent reporting period containing May 13, 2026, propose **Dr Current profits-tax liability 3,000 / Cr Current income-tax benefit 3,000**, subject to reviewer confirmation of substantive enactment and allocation. This reflects a later tax-law change relating to YA 2025/26; it is neither a March 31 journal nor a correction of the original provision.

### G. Selected BIR51 mappings

The reference is the specimen supplied through IRD's 2025/26 hub, footer BIR51 (4/2025). All mappings are draft and must be compared with the actual issued return. These selected fields do not complete every part or supplementary form. [S07–S08]

| Page / item | Field meaning | Draft value | Evidence / control |
| --- | --- | ---: | --- |
| Page 1, 1.1 | Assessable profits before brought-forward loss | 3,000,000 | HK-A01–HK-A04 bridge |
| Page 1, 1.2 | Adjusted loss before brought-forward loss | 0 | Positive fixture result |
| Page 1, 1.3 | Loss brought forward | 0 | Explicit HK-FACTS assumption; verify for clients |
| Page 1, 2.3 | Two-tier eligibility | Yes, proposed | HK-FACTS; reviewer must confirm |
| Page 1, 2.1 / 2.2 | Tax payable / repayable under return computation | UNRESOLVED | Following-year provisional charge not supplied |
| Page 4, 11.9 | Machinery and plant annual allowance | 500,000 | HK-ASSET |
| Page 4, 12.1 / 12.2 | Gross income / turnover | 8,000,000 / 8,000,000 | HK-TB 4000; no other income |
| Page 4, 12.18 | Net profit per accounts **before tax** | 3,000,000 | Pre-tax P&L, not profit after tax [S12] |
| Page 4, 12.20 / 12.21 | Trade receivables / trade payables | 1,500,000 / 1,000,000 | HK-TB 1100 / 2000 |
| Page 4, 12.22 | Issued share capital | 1,000,000 | HK-TB 3000 |

The 4,500,000 operating-cost aggregate must be broken into the financial-data categories the full form requires; do not force it into an arbitrary expense box. Confirm audited-accounts requirements, declarations, connected-entity supplementary information, foreign-income screening, and electronic-filing applicability separately.

### H. Payment reconciliation and remaining questions

HK-PAY states that provisional tax of 250,000 was charged, paid, and properly allocated for YA 2025/26. The fixture omits the following-year provisional assessment and full demand-note details.

| Separate amount | HKD / status |
| --- | ---: |
| March 31 current-tax estimate | 330,000 |
| Later enacted reduction of YA 2025/26 final tax | (3,000) |
| Post-enactment estimated final tax | 327,000 |
| YA 2025/26 provisional tax paid and allocated | (250,000) |
| Remaining final-tax component only | 77,000 |
| YA 2026/27 provisional component | UNRESOLVED |
| Full assessment / return payable | UNRESOLVED |

The 77,000 is not a payment instruction and must not populate BIR51 item 2.1 by default. Current-tax expense is not cash tax paid, and the following year's provisional charge is not an expense of the March 2026 reporting period.

| Question | Severity | Reviewer action |
| --- | --- | --- |
| HK-Q01 | REVIEW | Confirm two-tier and connected-entity facts and projected eligibility |
| HK-Q02 | REVIEW | Confirm warranty deduction timing, pool classification, and the forecast-supported 11% deferred rate |
| HK-Q03 | REVIEW | Confirm reporting-date exclusion and later-period recognition of the 3,000 law-change benefit |
| HK-Q04 | BLOCKER | Obtain demand notes and the next-year provisional amount before completing Part 2 |
| HK-Q05 | BLOCKER | Obtain granular expense categories, required audited documents, and remaining form answers |
| HK-Q06 | REVIEW | Confirm current and deferred offset rights and presentation separately; do not net unlike balances |

## 10. Acceptance tests

### 10.1 Test specifications

| ID | Condition | Expected result |
| --- | --- | --- |
| HK-T01 | Run the embedded positive fixture | Reproduce current tax 330,000, DTL 22,000, DTA 11,000, tax expense 341,000, and post-enactment final tax 327,000 |
| HK-T02 | Add 100 to one TB debit without an offset | Detect a 100 imbalance; withhold dependent form and provision totals |
| HK-T03 | Apply 16.5% or 8.25% automatically to deferred differences | Reject against the supported 11% expected average rate |
| HK-T04 | Apply the May law change to the March 31 provision | Detect date mismatch; retain 330,000 March current tax |
| HK-T05 | Deduct the one-off 3,000 from future provisional or deferred tax | Flag inappropriate propagation; verify separately |
| HK-T06 | Replace the Part 2 amount with final tax less paid tax only | Leave full payable unresolved until provisional and assessment data are complete |
| HK-T07 | Populate item 12.18 with profit after tax | Reject 2,659,000; correct value is pre-tax 3,000,000 |
| HK-T08 | Recognise a DTA with unsupported recovery assumptions | Hold recognition for reviewer decision; retain unrecognised/support-gap schedule |
| HK-T09 | Give every connected entity a reduced-rate band | Require nominated-entity evidence and eligibility review |
| HK-T10 | Treat all foreign income as automatically exempt | Require source and FSIE applicability analysis |
| HK-T11 | Sum supporting invoices into an already supported ledger expense | Detect duplicate numerical feed; preserve corroboration only |
| HK-T12 | Change tax year, framework, source data, or standards after review | New version and renewed review of affected work |
| HK-T13 | Missing losses, notice, form answer, or zero support | Keep underlying status MISSING; follow a documented form-specific fallback only if appropriate |
| HK-T14 | Journal or whole-return approval not actually supplied | Keep proposed/unposted and pending-review statuses |

### 10.2 Verification record for this document

The embedded fixture was checked by executable decimal arithmetic on November 2, 2026. Checks covered the balanced TB, both profit bridges, two-tier tax, the 11% expected deferred rate, DTA/DTL movements, balanced journals, the ETR bridge, and final/provisional separation. All numerical expectations matched. A test copy with a 100 debit increase failed the balance check as expected, and the workflow gate withheld dependent totals. The date and field-definition negative fixtures returned the expected mismatches.

These are document-fixture checks, not deployed-system tests or professional sign-off. Other acceptance-test behaviours remain `NOT_TESTED` until an implementation records evidence. For every client run, record the input version, actual result, tester, date, and reviewer decisions.

## 11. Version history

| Version | Date | Change | Review status |
| --- | --- | --- | --- |
| 0.2 | 2026-11-02 | Created Hong Kong/IFRS specialisation from 02_tax v0.1; added IAS 12 and IFRIC 23 reporting, two-tier deferred-rate analysis, tax-law timing, BIR51 mappings, provisional-tax reconciliation, and integrated fixture | Draft; arithmetic fixtures checked; professional review not performed |

Keep client configurations separate from this reusable core. Subsequent revisions must identify changed standards, laws, periods, form mappings, calculations, tests, and renewed review requirements.
