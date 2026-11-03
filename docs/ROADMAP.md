# Roadmap and Readiness

[Project overview](../README.md) · [Workflow catalog](../Version_2/README.md)

The goal is to turn reusable finance workflow specifications into demonstrable, reviewable processes that can be configured for different clients. This roadmap separates material present in the repository from future implementation work.

## Current baseline

| Area | Current state | Evidence |
| --- | --- | --- |
| Workflow coverage | Nine specifications covering import/data alignment, two tax jurisdictions, FP&A, presentations, board reporting, consolidation, and competitor analysis | [Version 2 catalog](../Version_2/README.md) |
| Version history | Earlier and current collections retained | [Version 1](../Version_1/README.md), [Version 2](../Version_2/README.md) |
| Onboarding | Quick-start instructions and engagement/review templates | [Quick start](QUICK_START.md), [engagement brief](../templates/ENGAGEMENT_BRIEF.md), [review record](../templates/REVIEW_RECORD.md) |
| Introductory demonstration | One-month synthetic revenue, resource, cost, and scenario example with expected arithmetic | [Planning example](../examples/revenue-led-planning/README.md) |
| Validation | Workflow-level notes vary; introductory example arithmetic can be checked against source CSVs | Individual playbooks and example files |
| Integrated execution | End-to-end client acceptance and a common execution layer remain pending | Milestones below |

## Milestones

| Stage | Work to complete | Completion evidence |
| --- | --- | --- |
| 1. Reproducible module demos | Run each selected workflow with synthetic inputs and meaningful exception cases | Fixtures, generated outputs, reconciliations, execution record |
| 2. Integrated finance pilot | Use one sample company across format alignment, FP&A/consolidation as applicable, board reporting, and presentation refresh | Matching figures, definitions, period, scenario, source version, and review status |
| 3. Professional review | Have finance and jurisdiction-specific reviewers assess applicable modules | Named reviewer, dated findings, corrections, acceptance scope |
| 4. Client configuration | Separate shared instructions from client mappings, templates, policies, and private data | Configuration pack and successful rerun without editing the shared workflow |
| 5. Repeatable delivery | Add implementation tooling, dependency documentation, and regression checks where useful | Reproducible setup, versioned examples, passing checks, measured run results |

These are planned milestones, not claims of completed client pilots, professional sign-off, or software releases.

## Known gaps and decisions

- **General accounting support:** add a dedicated journal-entry and accounting-treatment workflow; the existing accounting import playbook covers data preparation.
- **Shared references:** reconcile older proposed `skills/` paths and module numbers after choosing stable packaging. The [catalog](../Version_2/README.md) maps today's files.
- **Integrated evidence:** execute complete output-to-output demonstrations; a documented process or checked example does not establish full execution.
- **Execution packaging:** identify transformations needing scripts, tool integrations, or reviewer-led procedures.
- **Jurisdiction maintenance:** establish an owner and review cadence for dated accounting/tax references and applicable periods.
- **Distribution terms:** the maintainer should choose licensing terms before presenting the collection as a licensed reusable package.

## Measure pilot results

Collect a baseline and observed results before publishing efficiency claims.

| Measure | Suggested definition |
| --- | --- |
| Preparation time | Complete input receipt to first reviewable draft |
| Review effort | Reviewer time and number of correction cycles |
| Completeness | Required records, schedules, or objects delivered versus expected |
| Reconciliation | Count and value of unexplained differences, with resolution status |
| Traceability | Sampled figures successfully linked to source and calculation |
| Refresh reliability | Updated inputs produce explained changes and consistent controls |

Record workload, data quality, tooling, and reviewer scope alongside each measure.
