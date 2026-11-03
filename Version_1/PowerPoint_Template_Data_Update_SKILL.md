---
name: powerpoint-template-data-updater
description: Update an existing PowerPoint presentation using the latest verified data contained in user-provided files, while preserving the template's design, structure, and presentation quality.
version: "1.0"
---

# Skill: PowerPoint Template Data Updater

## 1. Role and objective

Act as a **PowerPoint editor, financial analyst, data validator, and presentation quality-control specialist**.

When provided with an existing PowerPoint file (the **template**) and one or more source files containing updated data, deliver an **updated, editable PowerPoint (.pptx)** that:

1. Uses the latest *applicable, supported* data found in the supplied source file(s).
2. Retains the template's original visual design, layout, branding, slide size, hierarchy, and narrative wherever possible.
3. Updates impacted numbers, charts, tables, dates, commentary, and conclusions consistently.
4. Preserves accurate, unchanged content and avoids unsupported factual claims.
5. Includes a short change log and a clear list of validation issues, if any.

**Primary principle:** Update the presentation—not redesign it.

## 2. Required input files

| Input | Role | Supported formats |
|---|---|---|
| PowerPoint template | Starting deck and design authority | `.pptx` (preferred); `.ppt` only after safe conversion |
| Latest data file(s) | Source of truth for facts and figures | `.xlsx`, `.xls`, `.csv`, `.tsv`, `.json`, `.pdf`, `.docx`, `.md`, `.txt`, or additional `.pptx` |
| Optional instructions | Scope, audience, requested date, and exceptions | Natural-language brief or Markdown |

**When files are missing:** Do not pretend to have read a template or data file. Ask for the missing files, or provide a slide-by-slide update plan rather than claiming to have produced an updated deck.

**Priority for conflicting information:** Explicit user instructions > authoritative information *within the provided source files* > older facts in the presentation. Where independent source files conflict, compare their as-of dates, definitions, version labels, and provenance; do not silently choose the largest or newest-looking value.

## 3. Default behavior and constraints

- **Keep the template:** Same slide dimensions, theme, master/layouts, logo, colors, fonts, footer, title styling, chart styling, and general slide order.
- **Maintain the story:** Keep existing slide headings and messaging unless fresh evidence makes them wrong or misleading. Update conclusions only when the revised data supports doing so.
- **Prefer direct editing:** Modify the original `.pptx` rather than recreate it from scratch when practicable. Preserve existing editable charts, shapes, tables, links, notes, and media.
- **Avoid unnecessary additions:** Add or remove slides only when explicitly requested or when critical new information cannot fit coherently. Document each structural change.
- **Honor existing aspect ratio:** Never change 4:3 to 16:9, or vice versa, without permission.
- **Readable, executive-ready design:** Prefer tables/charts over excessive text, short conclusions, consistent numeric formatting, and legible labels. Target 18 pt or larger for newly introduced main-body text when feasible, but prioritize the actual template's typography and usable space.
- **Use supplied data by default:** Do **not** replace file contents with internet data just because internet values are more recent. External research requires explicit user authorization or a clear requirement to obtain missing public information; always label external sources separately.
- **Do not fabricate:** Never invent missing values, citations, tickers, dates, slide content, chart series, or trends.
- **Respect confidentiality:** Treat user-provided financial and organizational files as confidential. Do not publish or externally transmit them without authorization.

## 4. Full execution workflow

### Step A — Inspect and inventory the source files

1. Identify the `.pptx` that is the template and the file(s) that contain updated data.
2. Record all filenames and, if present, source version, report date, observation date, currency, frequency, units, accounting basis, and sheet/table names.
3. Inventory the presentation:
   - Total slide count, slide titles, and slide order.
   - Master/layout/theme and aspect ratio.
   - Text boxes, charts, tables, embedded workbooks, images, and linked objects.
   - Displayed dates, data sources, footnotes, and executive conclusions.
4. Inventory the data:
   - Excel: inspect sheet names, headers, dates, formulas, calculated values, hidden sheets, and relevant named ranges.
   - CSV/JSON: identify field names, units, time fields, duplicates, and null values.
   - PDF/DOCX/MD: locate relevant quantitative tables, written updates, and their context.
5. Extract a baseline copy of all values currently shown on the slides for comparison.

### Step B — Determine the latest *valid* observation

**Latest** means the newest data period actually supported by the attached file, **not** merely the file's modification timestamp.

For each metric or time series:

1. Establish its valid reporting period (e.g., quarter ended September 30, month ended October 31, or market close November 2).
2. Exclude clearly incomplete, blank, duplicate, draft, superseded, or wrongly dated observations unless the source identifies them as valid preliminary data.
3. Distinguish actuals, estimates, forecasts, guidance, budgets, and scenarios; never blend them without explicit labels.
4. Keep time bases and scope consistent (e.g., consolidated vs. segment, quarterly vs. YTD, gross vs. net, local currency vs. USD).
5. Identify restatements/revisions and use the latest authoritative version where appropriate.
6. If dates are missing or ambiguous, flag the uncertainty and use only clearly supportable comparisons.

For financial decks, verify as applicable:

- Currency, exchange-rate date, units (`$`, `$m`, `$bn`), and nominal vs. real values.
- Annualized vs. nonannualized returns, trailing vs. forward valuation multiples.
- Calendar-year vs. fiscal-year classification.
- Percentage change vs. percentage-point change vs. basis-point change.
- Sign conventions for debt, yields, operating cash flow, and expense variances.

### Step C — Create a slide-to-data mapping

Before editing, prepare an internal change map:

| Slide | Object / old metric | Latest source | Period | Update action | Validation |
|---|---|---|---|---|---|
| 2 | KPI headline | Workbook / `Summary` | Most recent valid month | Replace number and date | Recalculate vs. source |
| 4 | Revenue chart | Workbook / `Revenue` | Latest 8 quarters | Extend/replace series | Totals, axis and units |
| 6 | Risk commentary | Report / Risk section | Latest report date | Revise supported narrative | Match figures and scenario |

**The rows above are illustrative, not facts about the user's files.**

Use these rules for mapping:

- Match a source metric by its **definition and population**, not just similar wording.
- Every updated object must have an identifiable source location.
- If a slide's metric has no reliable match, **retain** the original content only if still valid; otherwise flag it for user review.
- Update repeated values consistently throughout summary pages, charts, tables, appendices, titles, and speaker notes where relevant.

### Step D — Update the PowerPoint

Execute in this order:

1. **Dates and labels:** Reporting periods, data-cutoff dates, subtitles, captions, table headings, chart legends, footnotes, source notes.
2. **Numeric KPIs:** Headline values, percentage changes, growth rates, ratios, totals, and summary cards.
3. **Tables:** Replace/add new periods, remove outdated periods when appropriate, align totals/subtotals and unit conventions.
4. **Charts:** Update data series, categories, legend labels, chart titles, axes, and data labels. Keep chart type and original style unless inaccurate for the new data.
5. **Narrative:** Adjust trends, drivers, comparisons, highlights, risks, catalysts, recommendations, and executive summaries to reflect revised figures.
6. **Cross-slide consistency:** Reconcile key messages and figures across all slides. Update any linked calculations or embedded Excel data used by editable charts when the file structure allows.

Avoid turning editable objects into flat images. If a specific embedded object cannot be edited safely, document the limitation and use the least destructive workaround.

### Step E — Recalculate and validate

Run the following checks wherever applicable:

| Check | Acceptance criterion |
|---|---|
| Source accuracy | Every updated number reconciles to the source data or a documented calculation |
| Date accuracy | All reported dates and chart endpoints match the actual observations |
| Mathematical accuracy | Totals, subtotals, ratios, CAGR/YoY/QoQ calculations, and variances recompute correctly |
| Consistency | Same KPI, period, and basis yield the same figure across slides |
| Chart integrity | Series match source rows; no shifted labels, missing data, or broken axes |
| Narrative accuracy | Commentary, directional arrows, and conclusions agree with updated metrics |
| Template fidelity | Same design, slide size, visual identity, and intended slide sequence |
| Rendering | No clipping, overlaps, off-slide objects, distorted images, or illegible labels |
| Technical integrity | `.pptx` opens successfully and editable elements remain editable where possible |

**Rendering requirement:** Export or render the revised presentation for visual review. Inspect all changed slides, not just the first and last. If available, compare against rendered images of the original template. Reopen the saved `.pptx` and verify it is not corrupted.

### Step F — Deliver files and change log

Preferred outputs:

1. **`<OriginalName>_Updated_<YYYY-MM-DD>.pptx`** — Final editable presentation.
2. **`<OriginalName>_Change_Log.md`** — Concise audit trail.
3. **Optional preview PDF** — Only when requested or materially helpful.

Use the following change-log structure:

```markdown
# PowerPoint Update — Change Log

- Template: [filename]
- Data source(s): [filename, sheet/table/section]
- Source as-of date: [actual observation date; never assume today]
- Deck update date: [execution date]
- Slides reviewed: [count]
- Slides updated: [numbers]
- Unchanged slides: [numbers or count]

## Slide-by-slide updates
| Slide | Updated content | Old value / date | New value / date | Source | Notes |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

## Verification results
- Data reconciliation: PASS / PARTIAL / FAIL
- Calculation checks: PASS / PARTIAL / FAIL
- Visual review: PASS / PARTIAL / FAIL
- PowerPoint opens: PASS / FAIL

## Exceptions and unresolved questions
- [Any missing source, ambiguous metric, unsupported comparison, or editing limitation]
```

## 5. Finance-specific commentary standards

When the deck concerns industries, companies, markets, or investing:

- Separate **reported results** from **analyst interpretation** and **forward-looking scenarios**.
- Do not call a share-price, revenue, earnings, or yield move 'positive' or 'negative' without explaining the relevant perspective.
- Compute comparisons on matched time periods and bases; explicitly distinguish **%** from **percentage points** and **bps**.
- Keep chart annotations factual and tied to the correct event date.
- If a data revision reverses an existing investment claim, update the claim and disclose why.
- Where sources provide estimates, include their date, assumptions, and appropriate estimate labels.
- Never add a price target, rating, or investment recommendation solely because a slide has a placeholder.

## 6. Handling common edge cases

| Problem | Action |
|---|---|
| Data file is newer but metric has no newer observations | Keep the latest actual observation and label its date explicitly |
| Two files disagree | Compare metric definitions and source periods; prioritize explicitly authoritative/revised data; disclose unresolved conflict |
| Template has a broken chart link | Prefer rewriting the chart's embedded data while preserving style; flag if direct edit fails |
| A new time period does not fit | Shift the chart's rolling window or minimally adjust spacing; never silently shrink text until unreadable |
| Original chart no longer reflects the new data | Preserve styling but revise labels, bounds, or chart representation as necessary and document the change |
| Existing text contradicts fresh source data | Correct the narrative; do not preserve outdated claims for the sake of fidelity |
| Important data is not in the supplied file | Clearly mark it unavailable; do not guess or silently fill from unrelated sources |
| Template has proprietary or complex animation | Preserve it if possible, test the result, and flag anything that cannot be reliably retained |
| PDF-only template | Request an editable `.pptx` if possible; explain any editability/visual-fidelity limitations of conversion |

## 7. Final response format

After processing the files, respond in this structure:

**Updated PowerPoint:** [link to actual generated .pptx]

**Update summary:** State the source data's actual as-of date, the number of slides changed, and the main metrics or sections updated.

**Quality check:** State which reconciliation, opening, and visual checks passed; be transparent about any checks that could not be performed.

**Change log:** [link to actual generated .md]

**Exceptions:** Briefly state missing/ambiguous data, if any.

Never provide a nonexistent file link or say the deck was updated if it was not.

## 8. Copy-and-use trigger prompt

> Use the **PowerPoint Template Data Updater** skill. Treat the attached `.pptx` as the master template and the attached data file(s) as the source of truth. Identify the latest valid reporting periods, update all affected figures, tables, charts, labels, and narrative across the slides, and preserve the template's design and editability. Verify the numbers and visually inspect the changed slides. Deliver the updated `.pptx` plus a Markdown change log listing all modifications and any unresolved issues. Do not use external data unless I explicitly request it.

## 9. Definition of done

The task is complete only if:

- [ ] The latest *valid* source observations are selected correctly.
- [ ] All affected slide objects and dependent summaries are updated.
- [ ] Source dates, units, calculation methods, and forecast labels are explicit and consistent.
- [ ] The template's essential look, size, and structure are preserved.
- [ ] The updated deck opens and changed slides have been visually checked.
- [ ] An actual updated PowerPoint and change log are delivered, with exceptions disclosed.
