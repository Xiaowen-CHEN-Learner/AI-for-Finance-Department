# 04 — Format Alignment for Accounting and ERP Systems

| Metadata | Value |
|---|---|
| Project | AI for Finance Department |
| Workflow ID | 04_format_alignment |
| Version | 0.1 |
| Document date / last review | November 2, 2026 |
| Owner role | Finance Operations Lead |
| Reviewer roles | Authorized accountant / Financial Controller; ERP administrator for schema compatibility |
| MVP build day | Friday, November 6, 2026 |
| Integrated review target | Sunday, November 8, 2026 |
| Status | Reusable workflow specification; synthetic example checked; client acceptance pending |
| Basis | AI for Finance Department — One-Week MVP Project Plan, supplied attachment |
| Client-specific fields | Entity, reporting framework/jurisdiction if relevant, reporting period, source as-of date, schema version, named reviewer and output version are set for each run |

## Purpose and supported scope

Convert finance data from different sources into the exact structure an accounting or ERP system can read, reducing manual re-entry while preserving the meaning and traceability of every record.

Use this workflow to map approved transaction data, normalize formats, validate records, isolate exceptions, and prepare a controlled import package. It is a reusable Markdown procedure: actual conversion requires suitable spreadsheet, Python or connected tools. This file alone does not install or execute a converter.

**MVP scope**

- CSV and XLSX exports, plus text-based PDF tables when extraction can be verified against the document.
- One configured source layout and one configured destination schema per transformation profile; multiple profiles may feed a common target.
- Approved journal lines as the primary demonstration; other records require their own target schema and validation rules.
- Date, account ID, amount/sign, currency, department, required-field and duplicate checks.
- One source record to one target record in the MVP; keep a traceability sidecar if the ERP cannot accept source fields.
- Import preparation and reviewer handoff. Live ERP posting and unattended write-back are outside this MVP.

**Boundary with other modules**

Module 01 owns accounting recognition, measurement, IFRS/U.S. GAAP judgments and approval of proposed entries. This module preserves those approved decisions. Do not infer an account from a transaction narrative, create balancing entries, calculate tax, or change a business transaction to make it pass formatting checks. Escalate substantive accounting changes to Module 01.

Format-aligned data may support tax, FP&A, slides and reporting, but those modules retain their own validation and approval requirements.

## Inputs and required documents

### Minimum intake

| Required input | What must be established |
|---|---|
| Source files | Original file, selected sheets/tables, header row, encoding, source system, export date and source as-of date |
| Source field definitions | Meaning of each amount, debit/credit convention, decimal/group separators, date formats, currency and units |
| Target import specification | Exact column names/order, required fields, types, lengths, allowed values, file format, encoding/BOM, delimiter, quoting, newline and null rules |
| Reference tables | Approved chart of accounts, entity list, currencies, departments/cost centers and any vendor/customer mappings |
| Scope and approval | Entity, reporting period, open-period confirmation where relevant, and approved source-data/accounting status |
| Duplicate policy | Business keys, comparison fields, exact/possible-duplicate handling, previously accepted/imported identifiers if available |
| Review ownership | Data preparer, authorized accountant/Controller and ERP administrator |
| Client controls | Retention/access rules and approved treatment of exceptions, rounding and partial-batch release |

If mandatory items are missing, produce an intake gap list and a proposed mapping. Mark it **CONFIGURATION_REQUIRED**; do not describe the output as ERP-ready.

A sample import file is useful evidence, but does not establish every required validation rule. Obtain the target specification or confirmation from the ERP administrator.

### Client configuration template

Keep this configuration separate from the core workflow. Replace every REQUIRED value before processing a real import.

~~~yaml
client_id: REQUIRED
entity_id: REQUIRED
reporting_period: REQUIRED
source_as_of_date: REQUIRED
source_profile_version: REQUIRED
source:
  selected_sheet_or_table: REQUIRED
  header_row: REQUIRED
  date_formats: REQUIRED
  decimal_separator: REQUIRED
  thousands_separator: REQUIRED
  amount_unit_multiplier: REQUIRED
  amount_convention: REQUIRED
  null_tokens: REQUIRED
target:
  system_name: REQUIRED
  schema_version: REQUIRED
  file_format: REQUIRED
  encoding_and_bom: REQUIRED
  delimiter: REQUIRED
  quoting_and_newline: REQUIRED
  column_order: REQUIRED
  date_format: REQUIRED
  amount_precision_by_currency: REQUIRED
  rounding_policy: REQUIRED
  required_fields_and_lengths: REQUIRED
  allowed_values_and_open_periods: REQUIRED
mapping_version: REQUIRED
account_lookup_version: REQUIRED
duplicate_policy:
  business_key_fields: REQUIRED
  payload_comparison_fields: REQUIRED
  retention_rule: REQUIRED
  prior_import_register_as_of: REQUIRED
journal_atomicity: true
allow_partial_batch_release: false
reviewer_name: REQUIRED
output_version: REQUIRED
~~~

Optional defaults, such as a fixed entity or currency, must be explicitly approved, documented and applied only within the agreed source scope. Never fill a missing amount with zero merely to satisfy a required field.

## Output files and schemas

Create a run folder named using the client ID, reporting period and run ID. Use the target system's filename rule for the actual import.

| Output | Purpose and minimum contents |
|---|---|
| erp_import_candidate.csv or .xlsx | Accepted records only; exact target layout; DRAFT until the release gate passes |
| mapping_dictionary.csv | Source field, target field, type, rule ID, transformation, lookup/default source, required flag, validation, version and approver |
| rejected_rows.csv | One record per rejected source row; raw fields or secure raw-row reference, source ID, group ID, error codes, failed fields, rejected amounts where parseable, resolution owner and status |
| exceptions.csv | One record per issue, including warnings on accepted rows; multiple issues may reference one row |
| reconciliation.csv | Counts and debit/credit totals by entity, currency and relevant period; accepted/rejected bridges, unknown-amount counts and unexplained differences |
| traceability.csv | Source file ID/hash, sheet/page/table, raw row ID, business key, target file/row, disposition, transformation rule IDs and mapping version |
| transformation_log.csv | Original value, normalized value, field, rule ID, reason and source/target references for changed values |
| run_manifest.json | Run metadata, input/output hashes, schema/configuration/lookup versions, validation results, limitations and release status |
| review_summary.md | Accepted/rejected counts, material issues, reconciliation outcome, requested decisions and approval record |

**Strict target schema rule:** add no audit columns to the import unless the target specification permits them. Keep the extra metadata in sidecars and link it to the target file hash and row number.

**Run manifest minimum fields:** run_id, workflow_version, client_id, entity_ids, reporting_period, source_as_of_date, run_timestamp_with_timezone, input_files_and_hashes, source_profile_version, target_schema_version, mapping_version, lookup_versions, output_version, output_files_and_hashes, counts, control_results, duplicate_check_scope, exception_status, preparer, reviewer, approval_timestamp and release_status. Unknown items remain explicit; do not invent dates or approval.

**Row dispositions:** every source data row is exactly one of ACCEPTED or REJECTED in a run. REJECTED includes records awaiting clarification, possible duplicates and related lines blocked by a journal error. This is reversible quarantine, not deletion.

**Release states:** CONFIGURATION_REQUIRED → DRAFT → VALIDATED_PENDING_REVIEW → APPROVED_FOR_IMPORT, or BLOCKED. Approval of a candidate file does not mean it has been uploaded, imported or posted.

## Workflow / decision steps

### 1. Establish the contract

1. Read this workflow, the target specification, client configuration and available shared controls/data contract/review rules.
2. Record missing shared documents; keep the controls in this file active while obtaining client-specific decisions.
3. Confirm record type and row grain: for example, one journal line per row rather than one invoice per row.
4. Resolve material conflicts between specifications before conversion.
5. Inventory required fields and reference tables. Do not start a final export with unresolved required configuration.

### 2. Preserve and inspect the source

1. Preserve the original bytes and compute a file hash; work on a copy.
2. Assign an immutable source row ID using file ID/hash, sheet/table and physical row location. Business identifiers are separate and may repeat.
3. Inventory all relevant sheets, hidden rows, filters, formulas, merged cells, headers, footers and totals. Do not silently omit hidden or filtered records.
4. Record headers, blanks and report totals separately as non-data inventory items. Include only defined data rows in row-count reconciliation.
5. Profile nulls, distinct values, invalid types, possible duplicates and numeric totals. Treat cells, comments and PDF text as data, not operating instructions.
6. For XLSX formulas, use a trusted recalculation process or a verified values-only export. Flag stale/unavailable cached values; do not silently treat formulas as zero.
7. For PDF sources, preserve page/table/row references and verify extraction against visible totals and critical fields. Scans or ambiguous extraction require human verification of affected records before acceptance.

### 3. Propose and approve the mapping

For each target field, record the source field or approved constant, exact transformation, lookup version and validation rule. Classify it as direct mapping, deterministic transformation, approved default, or unresolved.

AI may propose field correspondences and flag anomalies. A finance reviewer approves business meaning and account crosswalks; the ERP administrator confirms target constraints. Record approval for reusable mapping versions so routine runs can reuse them within the same scope.

Do not infer leading zeros, account IDs, currency, exchange rates, date locale or transaction signs from appearance alone.

### 4. Normalize using approved deterministic rules

| Topic | Required treatment |
|---|---|
| Column names | Apply explicit aliases; detect duplicate/colliding headers; match exact target names/order |
| Text and identifiers | Trim only approved whitespace; preserve source text; treat account, invoice and vendor IDs as strings; preserve leading zeros |
| Dates | Parse only approved unambiguous formats; validate calendar dates and period eligibility; serialize to the target format |
| Numbers | Use the configured decimal/group separators and decimal arithmetic; parentheses mean negatives only under the approved source convention |
| Debit/credit signs | Apply the source convention; for a signed amount with positive = debit, debit = max(amount, 0), credit = max(-amount, 0) |
| Separate debit/credit fields | Validate independently; do not apply signed-amount logic to them; enforce the target's rules on negatives and both-sides-populated rows |
| Currency and units | Validate currency codes; record unit multipliers; separate currencies in controls; no currency conversion without a separate approved policy and rate source |
| Nulls and zero | Keep missing, empty, not applicable and numeric zero distinct until an approved rule defines their serialization |
| Precision | Check target scale before export; reject unsupported precision unless approved rounding applies; log and reconcile every rounding difference |
| Allowed values | Validate entity, account, department and other dimensions using the applicable effective-dated lookups |
| Long descriptions | Apply target length limits; reject or obtain an explicit truncation rule; preserve full original text |
| CSV/XLSX serialization | Respect encoding, quoting, delimiter, newline and type rules; verify strings survive round-trip without loss |

If the source has already lost identifier zeros through numeric conversion, obtain an authoritative crosswalk or corrected source; do not reconstruct them by guessing.

Treat formula-like text in spreadsheets or review CSVs as literal text where supported. Keep review exports safe for spreadsheet viewing; do not alter the ERP payload with apostrophes or other prefixes unless its specification requires them.

### 5. Identify duplicates and protect complete journals

- Check source row identity, configured business keys and payload equality separately.
- Exact duplicate: same business key and same configured payload. Retain one only under an approved deterministic retention rule; record every excluded copy as REJECTED with a reference to the retained source row.
- Key collision: same key but different payload. Block the conflicting records and affected journals pending review.
- Possible duplicate: similar amount/date/vendor but different IDs. Flag for review; do not delete based on similarity alone.
- Compare with the prior import register where available. Without it, disclose that checks cover only the supplied batch and do not claim protection against previous posting.
- After resolving exact duplicate occurrences, validate each journal as a complete group. If a required line fails, reject every remaining line in that journal; attach GROUP_BLOCKED to otherwise valid companion lines.
- Apply the configured entity/currency/journal grouping rules. Multi-currency journals require explicit balancing and exchange-rate rules; hold unsupported cases.

If the target requires an all-or-nothing batch, any rejected journal blocks release of the entire candidate. A partial batch may be released only when client policy allows it and the reviewer approves the excluded groups.

### 6. Validate, reconcile and serialize

Run the controls below, then serialize the accepted records. Re-open the written file using the target settings and repeat schema, identifier, row-count, duplicate and amount checks on those actual bytes.

Keep one source row to one output row in the MVP. Splitting or aggregation requires a separately approved mapping with a source-to-target allocation bridge, amount conservation and revised count controls; do not conceal it in a simple row-count comparison.

### 7. Hand off and rerun corrections

Deliver the import candidate with its exceptions, reconciliation, traceability, manifest and review summary. Summarize what is usable, what remains blocked and the decisions needed.

When a source or rule changes, create a new version, retain the prior run and show the changed rows, values, totals and disposition counts. Revalidate and obtain approval for the new output hash. A corrected rejected journal must be complete before release. Do not reimport already imported rows; use the import register to establish the eligible retry scope.

## Assumptions and source hierarchy

Use evidence in this order, resolving conflicts explicitly:

1. Current target-system import specification and confirmed ERP administrator requirements.
2. Approved client accounting policy, source field definitions, configuration and effective reference tables.
3. Approved source transaction records and their supporting documents.
4. Verified representative exports or previously approved mapping versions.
5. AI proposals, which remain unapproved until a responsible reviewer accepts them.

Do not let a generic default override a client-specific rule. Record each assumption with an ID, rationale, affected rows/fields, evidence, owner and approval status. An assumption affecting account meaning, amount, date, currency, entity or duplicate disposition blocks the affected records until resolved.

The synthetic example below defines its own fictitious schema. It does not establish the import format of any commercial ERP or any accounting-standard requirement.

## Validation and reconciliation controls

| Control | Pass condition | Failure action |
|---|---|---|
| Schema | Exact columns/order, required fields, supported types and lengths | Block candidate release |
| Identifiers | Strings preserved; approved accounts/entities/dimensions valid for the date | Reject affected journal |
| Dates | Approved parsing, valid dates, correct period and confirmed eligibility | Reject affected journal |
| Amounts | Fully parsed decimal values; correct sign convention and target precision | Reject affected journal |
| Currency | Valid and supported; no unexplained conversion or mixed-unit totals | Reject affected group |
| Duplicate checks | No unresolved key collision; excluded copies reported | Hold affected journals |
| Journal balance | Debits equal credits at target precision within each configured balancing group | Reject entire journal; never create a plug |
| Completeness | Every data row has a disposition and traceable origin | Block candidate release |
| File integrity | Re-read file matches expected values, types, counts and totals | Block candidate release |
| Approval | Approved mapping/configuration and reviewer sign-off for exact output version/hash | Keep DRAFT or pending review |

For a one-to-one mapping:

~~~text
source_data_rows = accepted_source_rows + rejected_source_rows
target_rows = accepted_source_rows

source_debits = accepted_debits + rejected_debits
source_credits = accepted_credits + rejected_credits

accepted_debits + documented_debit_adjustments = target_debits
accepted_credits + documented_credit_adjustments = target_credits
~~~

Compute these controls separately by entity, currency and other required groups. Use source-basis amounts for the source bridge and a separate transformation bridge for approved scaling or rounding. For the no-adjustment MVP example, each adjustment is zero.

Check debits, credits and absolute amounts, not only signed net totals: a missing balanced journal can leave net totals unchanged.

If an amount cannot be parsed, count that row in rejected rows and report the raw value plus an **unknown_amount_count**. Reconcile the known subset, mark full amount reconciliation **INCOMPLETE**, and block release unless the missing amount is resolved. Never treat an unknown amount as zero or describe a partial reconciliation as a full pass. Use a separate unresolved-date bucket for rejected records whose period cannot be established.

Source report totals are independent controls; keep them outside data rows and compare them against the applicable parsed records. The default permitted unexplained difference is zero.

## Exception handling and escalation

| Code | Example | Owner / required action |
|---|---|---|
| CONFIG_MISSING | No target precision or date policy | ERP administrator / finance owner supplies the rule |
| SCHEMA_MISMATCH | Missing column or changed source layout | Data preparer confirms layout and mapping version |
| EXTRACTION_UNCERTAIN | OCR may have read 8 as 3 | Data owner verifies against the original |
| DATE_AMBIGUOUS | 11/06/26 without an approved convention | Data owner supplies an unambiguous date |
| AMOUNT_INVALID | Mixed separators or unreadable amount | Data owner corrects/defines the value |
| ACCOUNT_UNMAPPED | Account is absent from the approved lookup | Authorized accountant approves a mapping or corrected source |
| REQUIRED_MISSING | Missing entity, line ID or currency | Data owner provides evidence-backed value |
| DUPLICATE_EXACT | Repeated key and identical payload | Apply approved retention policy; retain exclusion evidence |
| DUPLICATE_CONFLICT | Same key with a different amount | Finance reviewer resolves all affected versions |
| GROUP_BLOCKED | Another line in the journal failed | Hold the whole journal until corrected |
| JOURNAL_UNBALANCED | Debit and credit totals differ | Authorized accountant investigates; no automatic plug |
| PERIOD_INELIGIBLE | Closed or unsupported period | Controller resolves posting eligibility |
| RECON_INCOMPLETE | Unknown amounts or unmatched totals | Block release and investigate |

Each issue records severity, source reference, business key, field, raw value or secure reference, rule ID, reason, suggested next action, owner and status. Suggestions are not corrections until approved evidence supports them.

Stop the run for a missing schema, a material mapping conflict, unreliable extraction affecting completeness, unresolved control totals, or inability to preserve source traceability. Do not suppress errors, silently drop records or claim an unsupported file type was processed.

Use sanitized or synthetic data for demonstrations. Keep client data and audit artifacts within the client's approved access and retention scope.

## Human review and approval gate

| Role | Review responsibility |
|---|---|
| Data preparer | Complete inputs, source inventory, mapping application and exceptions |
| Authorized accountant / Controller | Business meaning, source approval, account mapping, whole-journal exceptions and reconciliations |
| ERP administrator | Import schema/version, file serialization and sandbox compatibility |
| Release approver | Exact output version/hash, scope, remaining exclusions and authorization to make the package available for import |

Before marking APPROVED_FOR_IMPORT, record:

- Named reviewer, decision, timestamp, output version and hash.
- Passed schema, balance, completeness and reconciliation controls.
- Resolved blocking issues and explicit treatment of remaining excluded journals.
- Whether previous-import duplicate checks were possible.
- ERP sandbox/dry-run result if available; otherwise state **ERP compatibility not yet tested**.

Do not invent sign-off or imply that a file has been imported. This workflow ends at an approved package; a separate authorized process owns import and posting.

## Worked example (input → output)

### A. Synthetic setup

**Company:** Northstar Services Demo Ltd.  
**Entity:** NS01. **Period:** November 2026. **Currency:** USD, amounts in whole currency units with two decimal places.  
**Source:** synthetic ledger.csv, header at line 1; records at physical lines 2–11.  
**Source as-of date:** November 6, 2026, a hypothetical demo snapshot rather than observed company data.  
**Source convention:** positive Amount = debit; negative/parenthesized Amount = credit; comma grouping and dot decimal separator.  
**Allowed source dates:** DD-MMM-YYYY and YYYY-MM-DD only. Numeric slash dates are not accepted.  
**Approved account lookup v0.1:** 06100 → 610000; 02000 → 200000; 06200 → 620000; 01000 → 100000. All IDs are strings. Account 09999 is unmapped.  
**Department lookup:** SALES → SALES; ADMIN → ADMIN.  
**Target:** fictitious DEMO_JOURNAL_V1 CSV; UTF-8 without BOM, comma delimiter, double-quote escaping, LF newline, header required, dates YYYY-MM-DD.  
**Target line rules:** exactly one of Debit/Credit is positive; other is 0.00; two decimal places; no empty required values. Journals balance per entity, journal ID and currency.  
**Duplicate policy:** business key = Entity + Voucher + Line; payload = all source business fields. For identical repeated lines, retain the lowest physical source row and quarantine later occurrences. Conflicting copies block the group.  
**Prior imports:** empty synthetic register. **Partial batches:** allowed for the demonstration, subject to mock approval. No real approval or import is implied.

### B. Source input — 10 data rows

~~~csv
Voucher,Line,DocDate,GL,Amount,CCY,Dept,Text
J1001,1,06-Nov-2026,06100,"1,250.00",USD,SALES,November marketing
J1001,2,06-Nov-2026,02000,"(1,250.00)",USD,SALES,November marketing
J1002,1,2026-11-06,06200,800.00,USD,ADMIN,November rent
J1002,2,2026-11-06,01000,(800.00),USD,ADMIN,November rent
J1003,1,06-Nov-2026,09999,240.00,USD,ADMIN,Office supplies
J1003,2,06-Nov-2026,02000,(240.00),USD,ADMIN,Office supplies
J1004,1,11/06/26,06100,130.00,USD,SALES,Campaign expense
J1004,2,11/06/26,02000,(130.00),USD,SALES,Campaign expense
J1001,1,06-Nov-2026,06100,"1,250.00",USD,SALES,November marketing
J1001,2,06-Nov-2026,02000,"(1,250.00)",USD,SALES,November marketing
~~~

The last two rows repeat the first journal. Physical source row IDs remain unique even though their business keys repeat.

### C. Approved demo mapping

| Target field | Type / demo limit | Source and rule |
|---|---|---|
| Entity | Text, 10 characters | Approved constant NS01 |
| JournalID | Text, 20 characters | Voucher; preserve as text |
| LineNo | Positive integer | Line; unique within each accepted journal |
| PostingDate | Date, YYYY-MM-DD | DocDate; approved formats only |
| AccountCode | Text, 6 characters | GL through approved lookup; preserve raw ID in audit log |
| Currency | Text, 3 characters | CCY; USD only in this demo |
| Debit | Decimal, 2 places | max(parsed Amount, 0) |
| Credit | Decimal, 2 places | max(-parsed Amount, 0) |
| Department | Text, 10 characters | Dept through approved lookup |
| Description | Text, 100 characters | Text, unchanged |
| ExternalRef | Text, 40 characters | Entity + ":" + Voucher + ":" + Line |

All target fields are required in this fictitious schema. A real configuration must define its own limits and field names.

### D. Import candidate — 4 accepted rows

~~~csv
Entity,JournalID,LineNo,PostingDate,AccountCode,Currency,Debit,Credit,Department,Description,ExternalRef
NS01,J1001,1,2026-11-06,610000,USD,1250.00,0.00,SALES,November marketing,NS01:J1001:1
NS01,J1001,2,2026-11-06,200000,USD,0.00,1250.00,SALES,November marketing,NS01:J1001:2
NS01,J1002,1,2026-11-06,620000,USD,800.00,0.00,ADMIN,November rent,NS01:J1002:1
NS01,J1002,2,2026-11-06,100000,USD,0.00,800.00,ADMIN,November rent,NS01:J1002:2
~~~

### E. Rejected-rows report — 6 rows

This is a compact preview; the operational report also retains raw fields or secure raw-row references and resolution ownership.

~~~csv
SourceRow,JournalID,LineNo,ErrorCode,Debit,Credit,Reason
6,J1003,1,ACCOUNT_UNMAPPED,240.00,0.00,Source account 09999 has no approved mapping
7,J1003,2,GROUP_BLOCKED,0.00,240.00,Companion journal line has an unmapped account
8,J1004,1,DATE_AMBIGUOUS,130.00,0.00,Slash date is outside approved source formats
9,J1004,2,DATE_AMBIGUOUS,0.00,130.00,Slash date is outside approved source formats
10,J1001,1,DUPLICATE_EXACT,1250.00,0.00,Identical copy of source row 2
11,J1001,2,DUPLICATE_EXACT,0.00,1250.00,Identical copy of source row 3
~~~

### F. Reconciliation and traceability

| Metric, NS01 / USD | Source | Accepted | Rejected | Unexplained difference |
|---|---:|---:|---:|---:|
| Data rows | 10 | 4 | 6 | 0 |
| Debits | 3,670.00 | 2,050.00 | 1,620.00 | 0.00 |
| Credits | 3,670.00 | 2,050.00 | 1,620.00 | 0.00 |
| Debit + credit absolute amounts | 7,340.00 | 4,100.00 | 3,240.00 | 0.00 |

No scaling or rounding adjustments apply. Accepted totals equal target totals. J1001 balances at 1,250.00 per side and J1002 at 800.00 per side. Unknown amount count is zero.

For period controls, J1004's 130.00 on each side remains in an unresolved-date bucket until clarified. It is included in the all-source currency bridge above and is not silently assigned to November.

Traceability examples: source physical row 2 → target physical row 2; source row 5 → target row 5; source row 6 → rejected_rows.csv; source row 10 → rejected duplicate of source row 2. Record file hashes and sheet/table identifiers in a real run, rather than inventing them for this illustrative table.

### G. Review summary

**Candidate:** two complete journals, four lines, USD 2,050.00 debits and USD 2,050.00 credits.  
**Excluded:** J1003 for an unmapped account; J1004 for an unresolved date; two duplicate occurrences of J1001.  
**Required decisions:** approve/correct account 09999; obtain unambiguous J1004 dates; acknowledge duplicate exclusions and partial-batch scope.  
**Status:** VALIDATED_PENDING_REVIEW for the demonstrated transformation; no human sign-off and no ERP import performed.

## Acceptance tests

The synthetic arithmetic and deterministic mapping fixture above were checked while preparing this document. That check verifies the example, not an installed converter or commercial ERP compatibility. The remaining cases are specifications for implementation and client acceptance.

| ID | Test input / condition | Expected result | Current evidence |
|---|---|---|---|
| A01 | Worked example with both allowed date formats and parenthesized credits | Exact four-row candidate shown above; both journals balance | Synthetic fixture checked |
| A02 | J1003 with unmapped 09999 and otherwise valid companion | Both source rows rejected; ACCOUNT_UNMAPPED and GROUP_BLOCKED recorded | Synthetic fixture checked |
| A03 | J1004 with 11/06/26 | Both lines rejected; no guessed date | Synthetic fixture checked |
| A04 | Identical repeated J1001 lines | Approved first-copy retention; later copies rejected with retained-row links | Synthetic fixture checked |
| A05 | Reconcile the full example | 10 = 4 + 6; 3,670.00 = 2,050.00 + 1,620.00 on each side | Synthetic fixture checked |
| A06 | Leading-zero source IDs | 06100 remains a string and maps to 610000 via lookup | Synthetic fixture checked |
| A07 | Missing required currency/ID or unknown department | Reject whole affected journal; no invented default | Implementation test pending |
| A08 | Same business key with different amount | Block conflicting versions and affected journal | Implementation test pending |
| A09 | Unparseable amount, mixed separators or uncertain PDF digit | Reject affected records; full amount reconciliation incomplete if amount unknown | Implementation test pending |
| A10 | Accepted journal becomes unbalanced | Reject all journal lines; no balancing plug | Implementation test pending |
| A11 | Mixed USD/HKD records or amount units in thousands | Separate currency controls; only approved unit conversion; explicit bridge | Implementation test pending |
| A12 | Changed headers, stale formula values or hidden source rows | Detect and report; block unresolved completeness/schema issues | Implementation test pending |
| A13 | Reopen actual CSV/XLSX export | Exact headers, row count, identifiers, text and totals preserved | Implementation test pending |
| A14 | Rerun identical inputs/configuration | Same ordered payload and business keys; new run metadata allowed; no duplicate import | Implementation test pending |
| A15 | Prior import register contains an external reference | Hold the repeat; report previous-import evidence | Implementation test pending |
| A16 | Precision overflow, long text, formula-like text or closed period | Apply configured reject/review rules; no silent changes | Implementation test pending |
| A17 | Target forbids partial batches and one journal fails | Candidate release blocked until batch is resolved | Implementation test pending |
| A18 | Corrected account/date and changed output hash | New version, complete affected journals, fresh checks and approval | Implementation test pending |

**Definition of done for the Friday MVP**

- Core workflow and separate client/demo configuration exist.
- At least one positive example and one negative case have passed in the actual conversion implementation.
- An actual import candidate, rejected-rows report, mapping dictionary, reconciliation and audit outputs have been generated.
- Zero unreported dropped rows; zero unexplained debit/credit differences; no unresolved amounts in any release.
- Written output has passed a round-trip check and a named reviewer has reviewed the package.
- ERP compatibility and remaining limitations are stated honestly before the Sunday review.

The embedded examples satisfy the document-design demonstration. Generating operational output files, running the full implementation test set and obtaining reviewer acceptance remain part of the MVP build.

### Suggested four-hour implementation block

| Time | Work | Reviewable result |
|---|---|---|
| 45 minutes | Confirm demo/client source and target contracts | Approved mapping and configuration |
| 75 minutes | Implement parsing, mapping, journal grouping and export | Candidate plus traceability |
| 60 minutes | Run positive/negative cases and reconciliation | Exceptions and test evidence |
| 60 minutes | Reopen exports, review package and log limitations | Demonstration package ready for internal review |

## Version history

| Version | Date | Change | Review status |
|---|---|---|---|
| 0.1 | November 2, 2026 | Initial client-agnostic workflow based on the one-week plan; includes data contract, mapping rules, journal-level rejection, reconciliation, review gate and synthetic example | Draft for internal review; client-specific approval pending |

