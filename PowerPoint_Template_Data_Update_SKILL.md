---
name: powerpoint-template-data-updater
description: Update an existing PowerPoint deck (.pptx) with the latest verified figures from attached data files (Excel, CSV, JSON, PDF, Word, Markdown, or another .pptx) while preserving the template's design, layout, editable charts and tables, and narrative. Use this whenever the user has an existing deck and newer data and asks to "update", "refresh", "roll forward", "bring current", "re-run with Q3 numbers", or "swap in the new figures" — even if they don't say "template". Also use when they ask to update only the charts, only the KPIs, or only the commentary in a deck. Do not use for building a deck from scratch (use the pptx skill) or for Google Slides (use the google-workspace skill).
version: "2.0"
---

# PowerPoint Template Data Updater

Act as a combined PowerPoint editor, financial analyst, data validator, and QC reviewer. Given an existing deck (the **template**) and one or more files with newer data, deliver an **updated, editable .pptx** plus a **change log**.

**Core principle: update the deck, don't redesign it.** The user chose this template for a reason — its branding, structure and narrative are the product; the numbers are the payload. Every design choice you make on your own is a choice they didn't ask for and will have to undo.

## 1. Inputs

| Input | Role | Formats |
|---|---|---|
| Template deck | Design authority and starting content | `.pptx` (`.ppt` only after converting with LibreOffice) |
| Data file(s) | Source of truth for facts and figures | `.xlsx` `.xls` `.csv` `.tsv` `.json` `.pdf` `.docx` `.md` `.txt` `.pptx` |
| Instructions (optional) | Scope, audience, as-of date, exceptions | Chat message or Markdown brief |

**If a file is missing**, don't pretend to have read it. Ask for it, or offer a slide-by-slide update plan instead of claiming to have produced a deck. Check the uploads directory before concluding a file is absent — people often forget to mention an attachment.

**Priority when information conflicts:** explicit user instructions → authoritative content within the supplied files → older facts already in the deck. When two supplied files disagree, compare as-of dates, definitions, version labels and provenance; never silently pick the newest-looking or largest value, and disclose any conflict you couldn't resolve.

## 2. Standing rules

- **Keep the template.** Same slide size and aspect ratio, theme, masters/layouts, logo, colors, fonts, footer, chart styling and slide order. Never switch 4:3 ↔ 16:9 unless told to.
- **Keep the story.** Retain slide titles and messaging unless the new data makes them wrong. Change a conclusion only when the numbers actually support the change, and say so in the log.
- **Edit in place.** Modify the original file with python-pptx rather than rebuilding it. A rebuilt deck loses animations, notes, links, hidden formatting and the subtle layout tweaks the author made by hand.
- **Keep objects editable.** Don't flatten charts or tables into images. If an object can't be edited safely, document the limitation and use the least destructive workaround.
- **Add or remove slides only when asked** or when critical new content truly can't fit. Log every structural change.
- **Supplied data only.** Don't replace file contents with web data just because the web is newer — the user supplied these files because they are the agreed source. Search externally only with explicit authorization or to fill a gap the user has acknowledged, and label any external figure as such.
- **Never fabricate** values, dates, series, tickers, citations or trends. A visible "n/a — not in source" is far better than a plausible guess.
- **Treat the files as confidential.** Don't publish them or send them anywhere the user hasn't asked.

## 3. Workflow

### Step A — Inventory both sides

1. Identify which file is the template and which hold data.
2. Inventory the deck with python-pptx: slide count, titles, order, layout names, aspect ratio, and every text frame, table, chart, picture and note. Record every number, date, period label, footnote and source note currently shown — this baseline is what you reconcile against later.
   ```bash
   python -m markitdown template.pptx > baseline.md   # quick text dump
   ```
   For charts, also pull the embedded series (`chart.plots[0].categories`, `series.values`) so you know exactly what each chart currently plots.
3. Inventory the data: sheet/table names, headers, units, currency, frequency, accounting basis, as-of or observation dates, hidden sheets, formulas vs. values, duplicates and blanks. With openpyxl, load once with `data_only=True` for computed values and once without to see formulas.
4. Render the original deck to images so you have a visual reference before you touch anything:
   ```bash
   soffice --headless --convert-to pdf template.pptx && pdftoppm -png -r 60 template.pdf before
   ```

### Step B — Find the latest *valid* observation

"Latest" means the newest period the file actually supports — not the file's modification time, and not the last row if that row is blank, draft, or a forecast. For each metric:

- Pin down its reporting period (quarter ended 30 Sep, month ended 31 Oct, close of 2 Nov…).
- Exclude incomplete, duplicate, superseded or mis-dated rows unless the source labels them valid preliminary data.
- Keep actuals, estimates, forecasts, guidance and scenarios separate and labeled. Blending them is the single most common way an updated deck becomes misleading.
- Match basis and scope: consolidated vs. segment, quarterly vs. YTD, gross vs. net, local currency vs. USD, calendar vs. fiscal year, nominal vs. real, annualized vs. not.
- Prefer restated/revised figures when the source identifies them as authoritative.
- If a date is ambiguous, flag it rather than guess.

For finance decks, also check: currency and FX date; units (`$`, `$m`, `$bn`); trailing vs. forward multiples; **% change vs. percentage-point vs. bps**; sign conventions for debt, yields, cash flow and expense variances.

### Step C — Build the change map before editing

Write it as a table (it becomes the spine of the change log):

| Slide | Object / old value | Source location | Period | Action | How verified |
|---|---|---|---|---|---|

Rules for mapping:

- Match metrics by **definition and population**, not by similar wording. "Revenue" on a slide may be segment revenue while the sheet's "Revenue" is consolidated.
- Every updated object needs a traceable source cell/row/section.
- A metric with no reliable match stays as-is if still valid; otherwise it's flagged for the user, not guessed.
- Trace every repeated figure — executive summary, KPI card, chart label, appendix, speaker notes — so one number changes everywhere or nowhere.

### Step D — Edit the deck

Work in this order, because later steps depend on earlier ones:

1. **Dates and labels** — periods, as-of dates, subtitles, captions, table headers, legends, footnotes, source notes.
2. **Headline KPIs** — values, deltas, growth rates, ratios, totals.
3. **Tables** — add/replace periods, drop stale columns when the design implies a rolling window, re-foot totals and subtotals, keep unit conventions.
4. **Charts** — replace series with `chart.replace_data(CategoryChartData(...))`, which rewrites the embedded workbook while keeping chart type, colors and styling. Then check legend text, axis bounds (clear a hard-coded `value_axis.maximum_scale` if the new data exceeds it), data-label number formats and the chart title.
5. **Narrative** — trends, drivers, comparisons, risks, catalysts, recommendations and the executive summary. Direction words ("rose", "fell", "accelerated") and arrows must agree with the new numbers.
6. **Cross-slide reconciliation** — same KPI, same period, same basis → same figure on every slide.

**Text-editing technique that matters:** replace text at the **run** level, not the paragraph or frame level. Setting `text_frame.text = ...` wipes the fonts, sizes, colors and bold/italic the template author applied. Find the run containing the old value and set `run.text` so formatting survives. If a value spans several runs, edit the first run and blank the rest.

When text genuinely needs more room, prefer shortening the wording over shrinking the font; never autofit below legibility. Keep newly added body text at 18 pt or larger when the template's typography allows.

### Step E — Validate

| Check | Passes when |
|---|---|
| Source accuracy | Every updated number ties to a source cell or a documented calculation |
| Date accuracy | Period labels and chart endpoints match the actual observations |
| Arithmetic | Totals, ratios, YoY/QoQ/CAGR and variances recompute correctly (recompute in Python; don't eyeball) |
| Consistency | Same KPI/period/basis gives the same figure on every slide |
| Chart integrity | Series lengths equal category counts; no shifted labels, missing points or clipped axes |
| Narrative | Commentary, arrows and conclusions agree with the figures |
| Template fidelity | Slide size, theme, visual identity and slide order unchanged |
| Rendering | No clipping, overlap, off-slide shapes or illegible labels |
| File integrity | Saved .pptx reopens cleanly in python-pptx and converts in LibreOffice |

Rendering is not optional. Convert the updated deck and look at **every changed slide**, side by side with the "before" images:

```bash
soffice --headless --convert-to pdf updated.pptx && pdftoppm -png -r 60 updated.pdf after
```

A deck that reconciles perfectly but has a KPI overflowing its box is not done. Also diff the text dump of the new deck against `baseline.md` to catch anything that changed by accident.

### Step F — Deliver

Outputs:

1. `<OriginalName>_Updated_<YYYY-MM-DD>.pptx` — editable deck
2. `<OriginalName>_Change_Log.md` — audit trail (template below)
3. Preview PDF only if requested or clearly useful

Change-log template:

```markdown
# PowerPoint Update — Change Log

- Template: [filename]
- Data source(s): [filename — sheet/table/section]
- Source as-of date: [actual observation date, never today's date by assumption]
- Deck update date: [date of this update]
- Slides reviewed / updated / unchanged: [n / list / list]

## Slide-by-slide updates
| Slide | Updated content | Old value / date | New value / date | Source | Notes |
|---|---|---|---|---|---|

## Verification results
- Data reconciliation: PASS / PARTIAL / FAIL
- Calculation checks: PASS / PARTIAL / FAIL
- Visual review: PASS / PARTIAL / FAIL
- File opens: PASS / FAIL

## Exceptions and open questions
- [missing source, ambiguous metric, unsupported comparison, editing limitation]
```

## 4. Finance commentary standards

- Keep **reported results**, **analyst interpretation** and **forward-looking scenarios** visibly separate.
- Don't call a price, revenue, earnings or yield move "positive" or "negative" without saying for whom.
- Compare matched periods and bases; be explicit about %, percentage points and bps.
- Tie chart annotations to the correct event date.
- If new data reverses an investment claim in the deck, change the claim and explain why in the log.
- Carry estimates with their date, source and assumptions.
- Never add a price target, rating or recommendation just because a placeholder exists.

## 5. Edge cases

| Situation | Do this |
|---|---|
| Data file is newer but a metric has no newer observation | Keep the latest actual and label its date explicitly |
| Two files disagree | Compare definitions and periods; prefer explicitly revised data; disclose what's unresolved |
| Chart has a broken external link | Rewrite its embedded data with `replace_data`, keep styling, flag if it fails |
| New period doesn't fit the chart or table | Roll the window forward or adjust spacing minimally; don't shrink text into illegibility |
| Chart type no longer suits the data | Keep styling, revise labels/bounds/representation only as needed, document it |
| Existing text contradicts the new data | Correct it — fidelity to the template never justifies a false statement |
| Needed data isn't in the files | Mark it unavailable; don't fill from unrelated sources |
| Complex animation or transitions | Preserve, test the render, flag anything that can't be reliably kept |
| Template is PDF-only | Ask for the .pptx; explain the editability and fidelity limits of conversion |
| Template slides share a picture-based chart (screenshot) | You can't edit it; replace only with user approval, otherwise flag |

## 6. Final response format

**Updated PowerPoint:** [the actual delivered .pptx]
**Update summary:** source as-of date, number of slides changed, main metrics/sections updated.
**Quality check:** which reconciliation, arithmetic, visual and open-file checks passed; name any check that couldn't be run.
**Change log:** [the actual delivered .md]
**Exceptions:** missing or ambiguous data, in a line or two.

Never link a file that wasn't produced, and never say the deck was updated if it wasn't.

## 7. Definition of done

- [ ] Latest *valid* observation chosen per metric, with actuals/estimates kept separate
- [ ] Every affected object and every dependent summary updated, formatting preserved at run level
- [ ] Units, bases, dates and estimate labels explicit and consistent
- [ ] Slide size, theme, structure and story preserved
- [ ] Saved deck reopens cleanly; every changed slide rendered and visually checked
- [ ] Updated .pptx and change log delivered, exceptions disclosed
