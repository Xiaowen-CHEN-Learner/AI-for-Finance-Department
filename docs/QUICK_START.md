# Quick Start

[Project overview](../README.md) · [Workflow catalog](../Version_2/README.md)

Use one workflow on a small, clearly defined task before combining modules. The repository supplies instructions; your execution environment supplies file access, calculations, document generation, and research capabilities.

## 1. Choose a task and a reviewer

Select a playbook from the [catalog](../Version_2/README.md). Define the deliverable and intended reviewer: for example, an import candidate for the Controller, a monthly forecast for the Finance Manager, or a refreshed board deck for the CFO.

Confirm that the request fits the file's scope. An import-format conversion does not determine accounting treatment, and a combined entity dataset does not automatically constitute accounting consolidation.

## 2. Prepare the engagement

Copy the [engagement brief](../templates/ENGAGEMENT_BRIEF.md) into your approved private workspace. Complete the selected playbook's detailed configuration too. The brief is an index to that configuration, not a replacement for it.

| Common input | What to specify |
| --- | --- |
| Business objective | Decision or operational task the output supports |
| Entity and scope | Included entities, departments, accounts, products, or clients |
| Time | Reporting period, source as-of date, forecast horizon; tax year separately when relevant |
| Basis | Reporting framework, currency, units, signs, monthly/YTD basis |
| Sources | Authoritative files, versions, sheets/ranges, owners, control totals |
| Target | Import schema, report layout, workbook specification, or editable deck |
| Review | Named reviewer, tolerances, unresolved questions, intended use |

Use the [synthetic planning example](../examples/revenue-led-planning/README.md) to explore the process before preparing client files.

## 3. Supply the instructions and inputs

Open the selected workflow file on GitHub and use its Raw view to copy or download the Markdown. Give the complete file and inputs to an AI assistant in an environment approved for that data. If the tool supports repository access, point it to the exact file and commit.

Start with this task brief, replacing the brackets:

```text
Use the attached [workflow filename and internal version] for [objective].

Entity and period: [scope, reporting period, source as-of date].
Inputs: [source files and authoritative versions].
Configuration: [engagement brief and module configuration].
Target deliverable: [file type, template, audience].

First inspect the inputs and confirm which steps your tools can execute.
Identify missing information that would materially change the result.
Proceed with supported work and keep unresolved items explicit.
Return the deliverables, reconciliations, assumptions, exceptions, and
a concise reviewer handoff. Record which checks were actually performed.
```

The workflow's input requirements and output schemas govern the run. If a required file or capability is unavailable, produce the supported analysis and identify the incomplete deliverable.

## 4. Review the result

Apply the module's validation rules, then summarize the evidence in the [review record](../templates/REVIEW_RECORD.md).

- Tie record counts and financial totals to the stated source version.
- Inspect rejected or excluded records and account for their amounts.
- Confirm consistent periods, units, currencies, scenarios, and signs.
- Trace a sample of figures to the source and transformation rule.
- Distinguish facts, calculated results, assumptions, and judgments.
- For presentations, inspect the numbers and the rendered slides.

Arithmetic checks support review; they do not establish that a forecast assumption, tax treatment, or management decision has been approved.

## 5. Record the handoff and refresh

Keep inputs, configuration, workflow version, outputs, checks, exceptions, and reviewer decisions together. When data changes, rerun from the new authoritative source and record the changes. Preserve the prior result for comparison.

Across modules, pass the reviewed output version needed by the next workflow. Carry the entity, period, currency, scenario, source version, and review status through every handoff.

## Practical capability checks

| Deliverable | Capability needed |
| --- | --- |
| CSV or Excel transformation | Read data, transform values, export files, reconcile totals |
| Forecast or tax working papers | Reproducible calculations, required evidence, reviewable output |
| Current competitor research | Dated primary sources and source attribution |
| PowerPoint refresh | Editable PPTX access, supported chart/table editing, rendering |

There is no repository-wide installer or universal dependency list at this stage. Use the tooling required by the selected workflow and record limitations. See the [roadmap](ROADMAP.md) for packaging and integration work.
