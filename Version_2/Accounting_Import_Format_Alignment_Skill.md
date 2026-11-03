---
name: accounting-import-format-alignment
version: "1.1"
description: >
  Convert an existing accounting export (CSV/XLSX) into the exact import template an
  accounting system requires — GL journals, AP bills, AR invoices, trial balances,
  chart-of-accounts, vendor/customer masters — with a field-by-field mapping,
  controlled transformations, debit/credit and count reconciliations, and an
  audit-ready exception log. Use this whenever the user wants data "loaded into",
  "imported into", "formatted for", "migrated to", or "made compatible with" an
  accounting or ERP system (QuickBooks, Xero, NetSuite, SAP, Dynamics, Sage, Oracle,
  Odoo, Workday, or any in-house ledger), whenever they mention an import template,
  upload file, bulk journal, or "the system rejected my file", and whenever a
  spreadsheet of transactions needs its columns renamed, reordered, retyped, or
  re-coded to match a target layout — even if they never say the word "import".
category: accounting-data-preparation
---

# Accounting File → Accounting System Import Format

## 1. What this skill is for

Act as a **senior financial accountant, systems-implementation specialist, and data-quality reviewer** rolled into one.

The job: take the user's source accounting file(s) and produce a file that the **target system will accept**, without changing what the numbers mean. The target system's import template, specification, or sample file is the source of truth for layout; the user's source rows are the source of truth for accounting facts. Everything else is controlled transformation plus evidence.

**Done well means:** the output matches the target schema exactly; every output row traces back to a source row; every control you ran is reported with its result; and anything you could not resolve with evidence is quarantined and explained, not quietly patched.

> This file describes a workflow, not a universal import layout. There is no generic "accounting CSV" that every system accepts — a column set that loads cleanly into one system is rejected by another over header spelling, date order, sign convention, or a single missing field. That is why the target spec drives every layout decision.

## 2. Inputs

| Input | Need | Why it matters |
|---|---|---|
| **Source accounting file(s)** (CSV / XLSX / XLS / TSV) | Required | The rows and values being converted |
| **Target import template, spec, or accepted sample file** | Required for an import-ready claim | Exact headers, order, types, required fields, allowed codes, file/sheet structure |
| System name and import module | Strongly recommended | GL journal vs AP bill vs vendor master have different grains and different rules |
| Chart of accounts / GL crosswalk | When accounts are re-coded | Approved mappings instead of guesses |
| Vendor / customer / department / project / cost-center lists | When those codes appear | Validate reference integrity |
| Entity, period, base currency, date convention | When ambiguous in source | Correct posting context; prevents wrong-period or wrong-entity loads |
| Tax codes, currency codes, FX policy | When tax or multi-currency present | Tax jurisdiction and FX rates must never be inferred |
| A previous import error log or a known-good accepted file | Optional but valuable | Reveals the validator's real constraints, which specs often omit |

### What to do when inputs are missing

| Situation | Action |
|---|---|
| No source data | Ask for the file. Do not fabricate sample entries to "show the shape". |
| Source present, no target spec | Profile the source, draft a **provisional mapping plan** and a short **input checklist** of what the user must supply. Label any generated file **DRAFT — TARGET FORMAT UNVERIFIED**. Never call it import-ready. |
| Spec present but silent on a rule (date format, sign convention, encoding) | Look for evidence in a sample/accepted file. If none, list the open question in the report and apply the most conservative choice *only* for a labeled draft. |
| Crosswalk missing for a required code | Quarantine the affected rows as Blocking; produce the rest. |
| User says "just make it work" | Still don't invent codes or balancing entries. Explain that the system will reject or, worse, silently mis-post. Offer the draft plus the exact list of what is needed. |

Prefer finishing a partial, clearly-labeled deliverable over stopping entirely — but prefer stopping over guessing an accounting fact.

## 3. Run configuration

Fill this from the user's files and instructions before transforming anything. `TBD` means *not yet verified* and is itself a finding to report.

```yaml
system_name: TBD
import_module: TBD             # GL_JOURNAL | AP_INVOICE | AR_INVOICE | TRIAL_BALANCE | COA | VENDOR | CUSTOMER | OTHER
source_files: []
source_sheet_or_table: TBD
target_template_file: TBD
target_sheet_name: TBD
output_format: TBD             # csv | xlsx | txt | iif | xml | json — per spec
encoding: TBD                  # UTF-8 / UTF-8-BOM / Windows-1252 — per spec
delimiter: TBD                 # ',' ';' '\t' '|' — per spec
quoting_rule: TBD              # always / minimal / none — per spec
header_row_required: TBD
column_order: TARGET_TEMPLATE_EXACT
record_structure: TBD          # flat lines | header+lines in one file | header and lines in separate files
company_or_legal_entity: TBD
accounting_period: TBD
posting_date_rule: TBD
date_format: TBD               # e.g. YYYY-MM-DD — only what the target specifies
source_date_order: TBD         # DMY | MDY | YMD — confirmed from evidence, not assumed
base_currency: TBD
amount_decimal_places: TBD     # per currency; JPY=0, KWD=3, most=2
sign_convention: TBD           # separate Dr/Cr columns | signed net | reversal flag | per-row Dr/Cr indicator
blank_value_policy: TBD        # what the target wants in optional empty fields: empty / 0 / NULL
journal_grouping_key: TBD      # GL only: the field(s) that define one balanced journal
max_rows_per_file: TBD         # some systems cap upload size
approved_mapping_files: []
import_constraints_reference: TBD
```

### Principles that do not bend

1. **Target template wins on layout.** Header spelling (case and spaces included), column order, data types, field lengths, allowed values, required/optional flags, sheet names, file structure.
2. **Source records win on accounting facts.** Never invent an invoice, account, date, reference, tax treatment, exchange rate, or balancing amount. If the system needs something the source doesn't have, that is an exception, not an opportunity.
3. **Mappings need evidence.** "Office Supplies" looking like account 6120 is not evidence. A crosswalk, a system export, or the user's explicit instruction is.
4. **Transform; don't rewrite history.** Keep the original untouched, keep full precision until the final write, and make every change traceable to a rule.
5. **Exceptions stay visible.** Unmapped codes, missing mandatory values, unbalanced journals, ambiguous dates — flagged and quarantined, never defaulted away.
6. **Never claim the system accepted anything.** You produce and validate a file. Posting is a separate authorized act by the user or system owner.

## 4. Workflow

### Phase A — Inspect and profile (before touching anything)

1. **Inventory inputs:** every file, sheet, and table; row counts; where the real header row is (often not row 1); formulas, merged cells, hidden rows/columns, filters, freeze panes; embedded subtotal/total rows; multi-line cells.
2. **Determine the grain** of the source and the target: one row per journal line? per invoice header? per invoice line? per master record? A mismatch here is the single most common cause of a wrong import. Do not mix grains in one output.
3. **Read every required target field**, then the optional ones. Note which are conditionally required (e.g. `TaxCode` required only when `TaxAmount` ≠ 0).
4. **Capture target constraints** the spec states *and* the ones it implies: max lengths, uniqueness keys, allowed enumerations, how header rows link to line rows, whether multi-entity / multi-currency / multi-period loads must be separate files.
5. **Profile source values:** nulls, duplicates, leading zeros, IDs that Excel has turned into `1.23E+11`, dates stored as text vs serial numbers, thousands separators, negatives shown as `(1,200.00)` or `1200.00-` or `1200 CR`, inconsistent casing, trailing spaces, non-breaking spaces, BOMs, mixed encodings.
6. **Record source baselines now:** row count, sum of debits, sum of credits, net by currency, and totals by entity / period / transaction type where meaningful. These are what you reconcile the output against.

**Deliverable:** a short schema inventory (source vs target), baseline totals, grain statement, and the list of open questions.

### Phase B — Design the mapping (one row per target field, no exceptions)

| Target field | Required? | Source field(s) | Transformation | Reference / crosswalk | Validation | Status |
|---|---|---|---|---|---|---|
| `AccountCode` | Yes | `GL Account` | Trim; keep as text; preserve leading zeros | Approved COA | Exists in COA, active | Confirmed |
| `PostingDate` | Yes | `Accounting Date` | Parse as DMY (confirmed from sample row 7: `31/10/2026`); write `YYYY-MM-DD` | Date rule | Valid; within open period | Confirmed |
| `DebitAmount` | Conditional | `DR` | To numeric; strip `,`; full precision | Sign policy | ≥ 0; not both Dr and Cr on one line | Confirmed |
| `VendorID` | Conditional | `Supplier No.` | Lookup in vendor crosswalk | Vendor master | Found and active | Needs approval (14 unmatched) |
| `Department` | No | — | Leave blank per target blank policy | — | — | Not applicable |

*Headers above are illustrative; use the target's actual names.*

Statuses: `Confirmed` · `Needs approval` · `Unmapped` · `Not applicable`. Only mark `Confirmed` when you can point to the evidence.

**Mapping patterns and how to handle each:**

- **Direct:** meaning *and* type match. Copy the value.
- **Rename:** same values, new header.
- **Code conversion:** apply the supplied crosswalk. Report every unmatched value and every value that matches more than one target code.
- **Derived:** state the exact formula (`Net = Gross − Tax`) and check it against source rows that already carry the derived value, if any.
- **Constant / default:** only when the spec or the user authorizes it (e.g. `Currency = USD` for a single-currency entity). Record it as a rule, not as data.
- **Split (one source row → many output rows)** — e.g. a gross invoice split into net + tax lines — or **merge (many → one)** — e.g. invoice lines rolled to a header: keep the linkage key, preserve totals, and never collapse detail the target can accept. Get explicit authorization before aggregating.
- **Unmapped mandatory field:** the affected records are not import-ready. Period.

**Header + lines structures:** when the target expects a header record followed by its lines (or two linked files), derive the header from the lines (or vice-versa) only from fields that are constant across the group; any field that varies within a group is a Blocking exception, not a "pick the first one" decision.

### Phase C — Transform (only approved rules)

Work on a copy. For anything non-trivial, write a small script (pandas / openpyxl are fine) rather than editing by hand — scripts are repeatable, and the trace file falls out of them naturally.

- Drop blank, formatting-only, and repeated-header rows. Drop source subtotal/total rows **only** when they are unambiguously identifiable (label text, missing account, or sums matching the lines above); otherwise flag them.
- Rename to the **exact** target headers and reorder to the exact sequence. Add required columns with no source counterpart as empty (or the target's blank value) and record them as `Unmapped` or `Constant` in the mapping.
- Trim leading/trailing whitespace and non-breaking spaces; leave internal spacing alone.
- **Identifiers are text.** Account codes, invoice numbers, vendor IDs, cost centers: read them as strings from the start so leading zeros survive and long IDs don't become scientific notation. If the source already lost them (e.g. `6120` where the COA has `006120`), that is a crosswalk question, not a padding decision.
- **Dates:** determine day/month order from evidence (a value > 12 in one position, the file's locale, the user's confirmation). Excel serial numbers must be converted with the correct epoch. Any date that remains ambiguous (`03/04/2026` with no disambiguating rows) is an exception, not a guess.
- **Amounts:** parse `(1,200.00)`, `1200.00-`, `-1,200.00`, `1.200,00`, and `1200 CR` deliberately and consistently; keep full precision; round **only** at the final write, to the target's per-currency decimals, with a rounding-difference check (Phase D).
- **Signs:** follow the target's convention exactly — separate Dr/Cr columns, signed net, Dr/Cr indicator column, or reversal flag. Converting between conventions is a documented rule applied uniformly; never flip signs row-by-row to "make it balance".
- Treat `null`, `""`, `0`, `0.00`, `N/A`, `-`, and `NULL` as different things until the target's rules say which are equivalent.
- Split output by entity / currency / period / file-size cap when the target requires separate imports.
- Use only approved tax codes, currency codes, and FX rates. If the source has an amount in a foreign currency and the target wants base currency, the rate must come from the user or an approved table.
- Enforce max field lengths by **flagging** overflow, not truncating a reference or description silently.
- Output hygiene per spec: delimiter, quoting, embedded line breaks, encoding (BOM or not), line endings, no formulas, no leading `=`/`+`/`-`/`@` in text cells unless the target needs them (formula injection in review copies).

**Joining multiple sources:** join on verified stable keys only; state the cardinality you expect (1:1, 1:n); report unmatched rows on both sides. Never align by row position when a key exists.

### Phase D — Validate (every applicable control; mark the rest `N/A` with a reason)

| Control | Pass criteria |
|---|---|
| Target schema | Exact headers, order, sheet/file structure, data types |
| Mandatory fields | No blanks in required fields; conditional requirements satisfied |
| Reference integrity | Every GL account, vendor/customer, department, project, tax code, currency code exists and is active in the approved lists |
| Dates / periods | Parse cleanly; fall inside the allowed posting period(s); not in a closed period |
| Numeric integrity | Valid numbers; correct decimals per currency; sign convention followed; no line with both Dr and Cr unless the target allows it |
| Row continuity | Every accepted source row maps to ≥1 output row (or a documented merge); every output row traces to a source row |
| Completeness bridge | `Source rows = Accepted + Excluded`, and `Accepted → Output` relationship documented |
| Duplicates | No unexpected duplicate import keys (e.g. same invoice number + vendor); legitimately repeated lines preserved |
| Amount reconciliation | Source vs output totals agree by entity, currency, period, and transaction type — before rounding and after rounding, with the rounding delta shown |
| GL balance (journal imports only) | Per `journal_grouping_key` (plus entity/ledger/currency/period if the system requires): `Σ Debits − Σ Credits = 0`, within the documented per-currency rounding tolerance only |
| AP/AR integrity | Header total = Σ lines; net + tax = gross; payment terms and due dates valid per target |
| Format / text | Lengths, enumerations, encoding, delimiter, quoting all meet spec |
| Crosswalk coverage | 100% of required codes mapped, or the rows are quarantined |
| Round-trip read | Re-read the file you wrote with a strict parser (and, for CSV, with the delimiter/encoding the target declares) and confirm it parses to the same row count and totals |

**Balance rule scope:** apply the journal-balance test only to complete journals. A partial extract, a signed-net trial balance, or a master-data file does not have to balance — say so instead of forcing it. **Never generate an offsetting line to make a journal balance.** An unbalanced journal is a Blocking exception the user must resolve.

**Tolerance:** default to *zero unexplained difference*. The only acceptable non-zero difference is a rounding delta the target's decimal rule forces, and it is reported with its cause.

### Phase E — Resolve or quarantine

Exception log columns:

| Source file | Sheet | Source row / key | Severity | Column | Observed value | Expected rule | Recommended correction | Owner | Resolution |
|---|---|---|---|---|---|---|---|---|---|
| ap_oct.csv | Bills | Row 42 / INV-10077 | Blocking | `VendorID` | `ACME` | Must exist in vendor master | Add crosswalk ACME → V-00231 (candidate; needs confirmation) | AP lead | Open |

Severity:

- **Blocking** — cannot import reliably: missing mandatory code, unparseable or ambiguous date, unknown currency, unbalanced complete journal, duplicate import key, unresolved grain mismatch, overflow in a key field.
- **Warning** — may be valid but deserves a human look: unusual magnitude, possible duplicate business transaction, mapping chosen from a fuzzy match, description truncated by the user's own choice.
- **Informational** — benign normalization with an audit trail: trimmed whitespace, header renamed, date reformatted.

Blocking rows are **excluded** from the import-ready file and listed separately. Warning rows are **included** and listed. Both are visible; nothing is deleted. When a recommended correction is a judgment call (which vendor, which account, which period), it is a *candidate* for the owner to approve, not a change you apply.

### Phase F — Deliverables

When source and target requirements are both available:

1. **`<Module>_Import_Ready.<ext>`** — conforms exactly to the target; contains only rows that passed all Blocking checks. If the target demands separate files per entity/currency/period, name them accordingly.
2. **`<Module>_Field_Mapping.xlsx`** (or `.csv`) — the Phase B table, plus every crosswalk actually applied.
3. **`<Module>_Validation_Report.md`** — configuration used, controls with results, reconciliation tables (counts and amounts, before/after rounding), open questions, residual risks.
4. **`<Module>_Exceptions.xlsx`** (or `.csv`) — the Phase E log.
5. **`<Module>_Source_to_Output_Trace.csv`** — source file / sheet / row (or stable ID) → output file / row, including split and merge relationships.

If there were no exceptions, say **"no exceptions were identified in the checks performed"** — not that the system will accept the file. If the target spec was incomplete or missing, every file carries **DRAFT — NOT VERIFIED FOR IMPORT** in its name and its header comment or first sheet.

## 5. Final response format

Keep it to what a reviewer needs to decide whether to upload. In this order:

### A. Import readiness
- **System / module:** actual name
- **Target template:** filename / version used
- **Outcome:** `PASS` · `PASS WITH REVIEW` · `BLOCKED` · `DRAFT — TARGET FORMAT UNVERIFIED`
- **Prepared output:** filename(s)

### B. Reconciliation dashboard

| Measure | Source | Output | Variance / explanation |
|---|---:|---:|---|
| Rows (source → accepted → output) | | | e.g. 2 Blocking excluded; 1 split into 2 |
| Σ Debits | | | |
| Σ Credits | | | |
| Net by currency | | | |
| Rounding delta | | | |
| Blocking / Warning exceptions | | | |

### C. Mapping decisions worth knowing about
Renames are not worth a sentence; code conversions, constants, splits/merges, sign-convention changes, and anything that `Needs approval` are.

### D. Validation results
Which controls passed, failed, or were N/A, with scope and any tolerance actually used.

### E. Action needed
Blocking items, missing inputs, and who must approve each judgment call. Be specific: "AP lead to confirm 14 vendor mappings in `Exceptions.xlsx` rows 2–15", not "resolve exceptions".

### F. Files
Actual links to each deliverable. No invented links, no invented validator results, no "successfully imported".

## 6. Worked example (illustrative)

**Source** (as received; header on row 1, dates DMY confirmed by row with `31/10/2026`):

| Entry | Date | GL Account | Description | DR | CR |
|---|---|---|---|---:|---:|
| JE1001 | 31/10/2026 | 001200 | Office equipment | 1,200.00 | |
| JE1001 | 31/10/2026 | 002100 | Accounts payable | | 1,200.00 |

**Target spec** (this system's actual template): `JournalID, PostingDate, AccountCode, Memo, DebitAmount, CreditAmount`; dates `YYYY-MM-DD`; amounts numeric with 2 decimals, blank not allowed → write `0.00`; account codes 6 characters, text.

**Output:**

| JournalID | PostingDate | AccountCode | Memo | DebitAmount | CreditAmount |
|---|---|---|---|---:|---:|
| JE1001 | 2026-10-31 | 001200 | Office equipment | 1200.00 | 0.00 |
| JE1001 | 2026-10-31 | 002100 | Accounts payable | 0.00 | 1200.00 |

**Recorded changes:** headers renamed; date parsed as DMY (evidence: day value 31) and written in target format; thousands separator stripped; blank amount written as `0.00` per target's blank policy (rule, not data); account codes kept as 6-character text. **Checks:** JE1001 Dr 1,200.00 = Cr 1,200.00; 2 source rows → 2 output rows; totals reconcile to the cent. **Not done:** no account re-classification, no vendor, tax, or FX assumed.

## 7. Pitfalls that cause rejected or — worse — silently wrong imports

- Opening a CSV in Excel before processing: leading zeros gone, long IDs in scientific notation, dates re-interpreted in the local locale.
- Assuming MDY because the user is in the US; the export came from a system configured DMY.
- Treating a column of `0.00` as "no credit" when the target distinguishes blank from zero (or vice-versa).
- Matching vendors by name instead of ID; "ACME Ltd" and "Acme Ltd." become two vendors.
- Letting a subtotal row ride along as a transaction line — doubles the totals.
- Flipping signs on individual rows to force balance instead of fixing the convention mapping.
- Rounding at the source before summing: cents drift and the journal no longer balances.
- Writing UTF-8 without the BOM a Windows-based importer insists on (or with a BOM a Linux-based one chokes on).
- Mixing entities or periods in one file for a system that posts per entity/period.
- Reporting "all checks passed" without the round-trip read, then discovering an embedded line break shifted every row after 1,037.

## 8. Reusable execution prompt

> **Run the Accounting Import Format Alignment skill.**
>
> Attached: (1) the source accounting export, (2) the import template / specification for **[system and module]**, and (3) [any crosswalks or master lists]. Inspect both files, identify every required target field and the file layout, build a complete source-to-target mapping, and transform the source into the system's required import format.
>
> Keep source accounting values and full traceability. Do not invent GL codes, vendors, tax codes, dates, exchange rates, or balancing entries. Validate headers, column order, mandatory fields, permitted values, duplicates, reconciliations, and journal balances where applicable. Quarantine blocking exceptions separately.
>
> Deliver the import-ready file, mapping sheet, validation/reconciliation report, exception log, and source-to-output trace. If rules are missing or ambiguous, label the output **not verified for import** and tell me exactly what you need.

## 9. Pre-upload checklist

- [ ] Correct system and import module confirmed with the user
- [ ] Actual target template / version reviewed (not a generic layout)
- [ ] Source and target grain match, or the split/merge is documented and authorized
- [ ] Every mandatory target field mapped and validated; every optional one accounted for
- [ ] All crosswalks verified against approved master data
- [ ] No leading-zero loss, scientific notation, sign flips, or premature rounding
- [ ] Counts and amounts reconcile; rounding delta (if any) shown with cause
- [ ] Complete GL journals balance at the system's grouping grain
- [ ] Output re-read with a strict parser and matches
- [ ] No Blocking exceptions in the import-ready file; all exceptions listed
- [ ] Encoding, delimiter, quoting, line endings per spec
- [ ] Originals untouched; mapping and row-level trace delivered
- [ ] An authorized accountant / system owner reviews before production upload

---

**Scope:** this skill prepares and tests import data. It does not decide accounting-policy treatment, certify financial statements, override the receiving system's validation, or post entries. Those remain with the accountable humans.
