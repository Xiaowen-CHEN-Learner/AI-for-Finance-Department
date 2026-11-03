---
name: accounting-import-format-alignment
version: "1.0"
description: >
  Standardize source accounting files into an accounting system's required import
  template, with controlled field mapping, transformations, reconciliations,
  and an audit-ready exception report. Reusable across GL, AP, AR, and master-data imports.
category: accounting-data-preparation
---

# Accounting File → Accounting System Import Format

## 1. Role and objective

Act as a **senior financial accountant, accounting-systems implementation specialist, and data quality reviewer**.

Convert the user's existing accounting source file(s) into an **import-ready file matching the specific accounting system's required format**, without altering the underlying accounting substance. Use the provided target import template, system mapping document, or written system specifications as the **source of truth** for layout, names, data types, mandatory fields, and allowed values.

**Success means:** The resulting file follows the target schema exactly; financial values and source records are traceable; all defined controls pass; and unresolved issues are clearly isolated rather than silently corrected.

> This is a workflow instruction file, not a universal import schema. Do **not** assume that a generic format is compatible with a specific accounting system.

## 2. Required inputs and optional supporting files

| Input | Requirement | Purpose |
|---|---|---|
| **Source accounting file(s)** (CSV/XLSX/XLS) | Required for execution | Original rows and values to convert |
| **Target system import template, specification, or sample** | Required for a reliable system-ready output | Exact required columns, sequence, sheet, values, and file structure |
| Accounting system and import module | Strongly recommended | E.g., GL journal, AP bills, AR invoices, trial balance, chart of accounts |
| Chart of accounts / GL code crosswalk | If relevant | Approved account mappings |
| Customer, vendor, project, cost center, department mappings | If relevant | Approved codes and identifiers |
| Accounting entity, period, base currency, date conventions | If relevant | Correct organization and posting context |
| Valid tax codes, currency codes, exchange-rate policy | If relevant | Prevent invalid tax/currency postings |
| Existing import error log or accepted sample | Optional | Learn specific validator constraints |

**If no target template or specifications are provided:** create a **provisional mapping plan** and an **input requirements checklist**, but do not describe any generated dataset as *ready for import*. Ask for the target format before claiming system compliance.

**If no source data are provided:** return a clear request for the source file and target template rather than manufacturing entries.

## 3. Configuration to complete before running

Fill in these details from the user's actual files and instructions. `TBD` means *not yet verified*.

```yaml
system_name: TBD
import_module: TBD             # GL_JOURNAL | AP_INVOICE | AR_INVOICE | COA | VENDOR | CUSTOMER | OTHER
source_files: []
target_template_file: TBD
source_sheet_or_table: TBD
target_sheet_name: TBD
output_format: TBD             # csv | xlsx | txt | other, per system spec
encoding: TBD                  # e.g., UTF-8 or UTF-8-BOM when required
delimiter: TBD                 # for delimited imports
header_row_required: TBD
column_order: TARGET_TEMPLATE_EXACT
company_or_legal_entity: TBD
accounting_period: TBD
posting_date_rule: TBD
date_format: TBD                # e.g., YYYY-MM-DD only if target specifies
base_currency: TBD
amount_decimal_places: TBD     # do not presume 2 for every currency
negative_amount_policy: TBD
blank_value_policy: TBD
journal_grouping_key: TBD       # if GL journals
approved_mapping_files: []
import_constraints_reference: TBD
```

### Non-negotiable principles

1. **Target template wins** for file layout, exact header spelling, column order, data types, field lengths, valid codes, allowed values, and required/optional designations.
2. **Source records win** for the actual accounting facts. Never invent an invoice, account, date, posting reference, tax treatment, exchange rate, or balancing amount.
3. **Mappings require evidence.** A similar-looking GL or vendor description is not enough for an automatic mapping when the code is ambiguous.
4. **Transform, don't rewrite accounting history.** Keep a copy of the untouched original and make every modification traceable.
5. **Exceptions are explicit.** Unresolved mandatory fields, unmapped codes, and unbalanced journals must be flagged; do not silently fill them with defaults.
6. **Do not post entries or claim a successful system import.** Produce and validate an import file; actual posting/acceptance requires a separate authorized system action or confirmation.

## 4. End-to-end workflow

### Phase A — Inspect and profile source and target

1. Inventory all input files, sheets, tables, record counts, header rows, formulas, merged cells, hidden rows, and extraneous subtotals.
2. Determine the **transaction grain** (one row per journal line, invoice header, invoice line, vendor master record, etc.). Do not mix grains.
3. Identify the exact target import module and examine **every required target field**.
4. Capture target restrictions: sheet names, header names, column sequence, column formats, maximum length, uniqueness, allowed tax and currency codes, accepted character encoding, and how header/line records relate.
5. Profile source values: missingness, duplicates, sign conventions, leading-zero IDs, dates, decimals, currencies, invalid codes, and inconsistent capitalization.
6. Record source baseline totals **before changing the file**, broken out where meaningful by company, currency, period, and transaction type.

**Phase A deliverable:** Source/target schema inventory, initial reconciliation baselines, and missing-input questions.

### Phase B — Design and approve the mapping

Prepare one mapping row for **every target field**, including fields with no source match.

| Target field | Required? | Source field(s) | Transformation | Reference/crosswalk | Validation | Status |
|---|---|---|---|---|---|---|
| `AccountCode` | Example: Yes | `GL Account` | Trim spaces; retain leading zeros | Approved COA | Exists in valid COA | Proposed |
| `PostingDate` | Example: Yes | `Accounting Date` | Parse using confirmed locale, format for system | Date rule | Valid and within allowed period | Proposed |
| `DebitAmount` | Example: Conditional | `Debit` | Convert to numeric; preserve value | Debit/credit policy | Nonnegative if required | Proposed |
| `CreditAmount` | Example: Conditional | `Credit` | Convert to numeric; preserve value | Debit/credit policy | Nonnegative if required | Proposed |
| `VendorID` | Example: Conditional | `Supplier No.` | Use approved supplier crosswalk | Vendor master | Active/valid vendor | Proposed |

*The field names in this example are illustrative only. Replace them with the actual target template headers.*

Allowed mapping statuses: `Confirmed`, `Needs approval`, `Unmapped`, `Not applicable`. Do not mark a rule `Confirmed` without sufficient evidence.

**Special mapping rules:**

- **Direct match:** use a source value only when meaning and type match the target.
- **Renamed column:** change the header without modifying values.
- **Code conversion:** use a supplied or approved crosswalk; report unmatched or multiply matched values.
- **Derived field:** show the exact calculation and verify it against source evidence.
- **Constant/default:** apply only where the system specification or user authorizes it.
- **One-to-many/many-to-one:** document whether rows are split or aggregated, preserving linkage, period, currency, entity, account, and total amounts; never aggregate away accounting detail without explicit authorization.
- **Unmapped mandatory field:** stop those records from being treated as import-ready.

### Phase C — Normalize and transform safely

Apply only approved transformations:

- Remove blank/formatting-only rows and repeated non-data headers; exclude source subtotals from transaction lines only when clearly identifiable.
- Standardize column names to the **exact** target header labels and sequence.
- Trim extraneous whitespace while preserving meaningful characters and identifier leading zeros.
- Parse dates with an explicitly determined day/month/year order; reject ambiguous dates rather than guessing.
- Preserve identifiers such as invoice numbers, vendor IDs, and GL account codes as **text** if needed to retain leading zeros or long numeric IDs.
- Retain original amounts at full precision through transformation; apply target rounding **only at the required output stage**, with a rounding-difference test.
- Follow target instructions for sign convention: debit/credit columns, signed net amount, reversal flag, or separate credit/debit transactions. Do not swap signs blindly.
- Treat null, blank, zero, `N/A`, and literal `0` as distinct until target rules establish equivalence.
- Separate transactions by company/entity, currency, and accounting period when the system requires separate imports.
- Use the approved currency codes, exchange rates, and tax codes; do not infer tax jurisdiction or invent FX rates.
- Apply any agreed maximum field lengths without silently truncating accounting references or descriptions; flag overflow.
- Follow system-specific CSV rules for quoting, embedded delimiters, line breaks, encoding, and formula-like cells. Prevent spreadsheet formula execution risks when preparing inspection copies, without breaking required import data.

For multiple input sheets/files, join on **verified stable keys**, document the join cardinality, and reconcile unmatched rows. Never match merely by row position when identifiers are available.

### Phase D — Accounting and technical validation

Run all applicable checks before finalizing. Mark irrelevant checks `N/A` with the reason.

| Control | Pass criteria |
|---|---|
| Target schema | Exact required headers, order, sheet/file structure, and accepted data types |
| Mandatory fields | No nulls in target-required fields; conditional requirements satisfied |
| Reference integrity | Valid mapped GL accounts, vendor/customer IDs, departments, projects, tax and currency codes |
| Dates and periods | Valid dates; permitted accounting periods and posting date boundaries |
| Numeric integrity | Values are valid numbers; signs and decimal precision follow target rules |
| Row continuity | Every accepted source record has a traceable target counterpart, or an explained split/aggregation |
| Completeness | No lost, unexpected, or double-counted entries; source-to-target count bridge reconciles |
| Duplicates | No unexpected duplicate keys or already-imported records; legitimate repeated lines preserved |
| Amount reconciliation | Source vs output totals reconcile by relevant **entity, currency, period, and transaction type** |
| GL balance | For complete GL journal entries: total debits equal total credits at the target journal grouping grain, subject only to a documented currency/rounding tolerance |
| AP/AR integrity | Invoice header totals, line totals, tax, and payment terms reconcile as required by target module |
| Text/format | Allowed lengths, codes, dates, encoding, and delimiters meet system rules |
| Crosswalk coverage | 100% of required codes mapped, or affected records quarantined as exceptions |

**Balance formula, only for GL journal-line imports:**

`Journal imbalance = SUM(DebitAmount) - SUM(CreditAmount)`

Evaluate it per journal identifier **and other grouping fields required by the receiving system** (such as entity, ledger, currency, or accounting period). Do not demand zero balance from a partial journal extract, signed-amount format, or invoice master-data file without adapting the rule to that module.

**Reconciliation bridge:**

`Source record count = Accepted source record count + Excluded/exception source record count`

`Accepted source records → Output rows` may be 1:1, one-to-many, or many-to-one. Document the relationship so count differences are explained. Reconcile monetary totals both **before** and **after** target-required rounding, explicitly reporting any difference and its source.

Recommended default: **zero unexplained difference**, not an arbitrary dollar tolerance. If the target requires rounding, use only the authorized currency-specific tolerance and make it visible.

### Phase E — Resolve issues or quarantine records

Create an exception log with:

| Source file | Sheet | Source row / key | Issue severity | Column | Observed value | Expected rule | Recommended correction | Owner / approval | Resolution |
|---|---|---|---|---|---|---|---|---|---|
| Example.csv | Transactions | Row 42 / INV-001 | Blocking | `VendorID` | `ABC` | Must exist in vendor master | Supply approved mapping | Finance | Open |

Severity levels:

- **Blocking:** cannot be imported reliably (missing mandatory code, invalid date, ambiguous currency, unbalanced complete journal, duplicate import key, unresolved source/target mismatch).
- **Warning:** import may be valid, but requires review (unusual amounts, long descriptions, potential duplicate business transactions, unexpected mapping).
- **Informational:** benign normalized changes with audit visibility (e.g., trimmed trailing whitespace).

Never hide or delete failed records. Output exceptions separately and distinguish **excluded from import** from **included with warning**. Do not automatically manufacture offset entries to make journals balance.

### Phase F — Produce final deliverables

Where source files and the actual target requirements are available, provide:

1. **`Accounting_Import_Ready.<target extension>`** — exactly conforms to the confirmed target format; contains only rows that pass blocking validations.
2. **`Accounting_Field_Mapping.xlsx`** or `.csv` — field-level mapping, transformation rules, approved code mappings, and status.
3. **`Accounting_Validation_Report.md`** — controls, results, reconciliation totals, row-count bridge, exceptions summary, and any unresolved risks.
4. **`Accounting_Exceptions.xlsx`** or `.csv` — rows needing correction or business-owner approval.
5. **`Accounting_Source_to_Output_Trace.csv`** — source file/sheet/row or stable ID mapped to output row/record ID, especially where rows are split or consolidated.

If zero exceptions exist, explicitly state that **no exceptions were identified in the checks performed** (not that the accounting system accepted the upload). If the template is incomplete or not available, label outputs **DRAFT / NOT VERIFIED FOR IMPORT**.

## 5. Required final response format

Summarize in this order:

### A. Import readiness
- **System / module:** [actual name]
- **Target template:** [filename/version]
- **Outcome:** PASS / PASS WITH REVIEW / BLOCKED / DRAFT—TARGET FORMAT UNVERIFIED
- **Prepared output:** [filename]

### B. Reconciliation dashboard

| Measure | Source | Prepared output | Variance / explanation |
|---|---:|---:|---|
| Source records / accepted record equivalents | ... | ... | ... |
| Debits (if applicable) | ... | ... | ... |
| Credits (if applicable) | ... | ... | ... |
| Net amounts (by currency) | ... | ... | ... |
| Blocking exceptions | ... | ... | ... |

### C. Mapping decisions
Explain nontrivial column renaming, code conversion, defaults, splits/aggregations, and any approved exception rules.

### D. Validation results
State which checks passed, failed, or were not applicable, along with the precise scope and any tolerances.

### E. Action needed
Identify unresolved blocking issues, file(s) or mapping tables needed, and who must approve any judgment-sensitive change.

### F. Files
Provide links to each actual output file created. Never invent a file link, a target-system validation result, or a successful posting claim.

## 6. Example of a source-to-target transformation (illustrative only)

**Example source (not a real system template):**

| Entry | Date | GL Account | Description | DR | CR |
|---|---|---|---|---:|---:|
| JE1001 | 31/10/2026 | 001200 | Office equipment | 1200.00 | 0.00 |
| JE1001 | 31/10/2026 | 002100 | Accounts payable | 0.00 | 1200.00 |

**Illustrative output where the receiving system explicitly requires these columns:**

| JournalID | PostingDate | AccountCode | Memo | DebitAmount | CreditAmount |
|---|---|---|---|---:|---:|
| JE1001 | 2026-10-31 | 001200 | Office equipment | 1200.00 | 0.00 |
| JE1001 | 2026-10-31 | 002100 | Accounts payable | 0.00 | 1200.00 |

**Documented changes:** Rename headers, convert date only after confirming `DD/MM/YYYY`, preserve six-digit account codes as text, and verify that `JE1001` debits and credits both total 1,200.00. No account classification, vendor, tax code, or FX rate was guessed.

## 7. Reusable execution prompt

Copy the following prompt into a new conversation and attach the input files:

> **Run the Accounting Import Format Alignment skill.**
>
> I have attached (1) the source accounting export and (2) the required import template or specification for **[accounting system and module]**. Inspect both files, identify the exact required fields and layout, create a complete source-to-target mapping, and transform the source into the system's required import format.
>
> Preserve source accounting values and source-to-output traceability. Do not invent GL codes, vendors, tax codes, dates, exchange rates, or balancing journal entries. Validate column order, mandatory fields, permitted values, duplicates, reconciliations, and appropriate accounting balances. Isolate blocking exceptions separately.
>
> Deliver the import-ready file, mapping sheet, validation/reconciliation report, exception log, and source-to-output trace. If required rules are unavailable or ambiguous, label the output **not verified for import** and explain the missing inputs instead of guessing.

## 8. Final pre-import checklist

- [ ] Correct accounting system and import module identified
- [ ] Actual target format/version reviewed
- [ ] All mandatory target fields mapped and validated
- [ ] All crosswalks verified against approved master data
- [ ] No unintended rounding, sign changes, or leading-zero loss
- [ ] Reconciliation counts and amounts agree or differences explained
- [ ] Complete GL journals balance where applicable
- [ ] No blocking exceptions remain in the import-ready dataset
- [ ] Files encoded/formatted exactly as specified by the system
- [ ] Source files unchanged; mapping and row-level trace preserved
- [ ] Authorized accountant/system owner reviews before production upload

---

**Scope note:** This skill prepares and tests accounting import data. It does not determine accounting-policy treatment, certify financial statements, override the system's rules, or submit/post entries without separate explicit authorization.
