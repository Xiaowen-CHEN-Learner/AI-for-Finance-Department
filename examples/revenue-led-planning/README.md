# Worked Example — Revenue-Led Planning

[Project overview](../../README.md) · [FP&A workflow](../../Version_2/FPandA_Skills.md)

**All entities, clients, amounts, and assumptions in this example are fictional.** This is a small illustration of the planning sequence: Sales demand → delivery resources → departmental costs → profitability → scenarios.

The example covers one synthetic services company, one month (`2027-01`), and USD in whole currency units. It demonstrates the revenue/cost portion of the FP&A workflow. It is not a full execution of the playbook's 12-month model, linked balance sheet, cash flow, or review gates.

## Files

| File | Purpose |
| --- | --- |
| [sales_forecast.csv](sales_forecast.csv) | Three Sales lines by client, segment, service type, and region |
| [cost_plan.csv](cost_plan.csv) | Delivery cost driver and five departmental overhead lines |
| [scenario_assumptions.csv](scenario_assumptions.csv) | Explicit scenario drivers, capacity, and profitability target |
| [expected_summary.csv](expected_summary.csv) | Reference results for checking a calculation; not an input to the forecast |

## Assumptions and definitions

- One sales unit is one billable service hour. Each unit requires one delivery hour.
- All forecast services are delivered and revenue is recognized in the displayed month; price is constant within each service line. There is no pipeline probability weighting.
- Delivery is provided by an external hourly supplier at a base cost of USD 90 per hour, with 450 hours of available monthly capacity. For this example there is no minimum-volume commitment.
- Departmental fixed costs total USD 23,000 per month. They exclude direct delivery costs and remain unchanged when volume falls.
- The optimistic case adds USD 1,000 of IT support cost. This is an explicit demonstration assumption, not a benchmark.
- Costs are shown as positive expenses. The simplified EBITDA measure equals revenue less direct delivery costs and departmental operating expenses. Depreciation, amortization, interest, and tax are outside this example.
- The target EBITDA margin is 30%. It is a management target and does not overwrite forecast results.
- Every file is a synthetic demo version, with no real Sales, department, or Finance approval implied.

## Source schema

`sales_forecast.csv` contains one row per client/service/month. `base_units` is a quantity, `price_per_unit` is USD per billable hour, and `delivery_hours_per_unit` converts sold units into workload. `source_row_id` provides a unique source reference. All four commercial dimensions are alternative views of the same revenue.

In `cost_plan.csv`, `base_rate_or_amount` means USD per delivery hour for the variable line and USD per month for each fixed line. `cost_behavior` and `driver` determine which interpretation applies. Scenario rows contain decimal multipliers (for example, `1.2` means 120% of base volume), an incremental IT expense in USD, capacity in hours, and a decimal target margin (`0.30`).

## Reproduce the calculation

For each scenario, apply these formulas to the source rows:

```text
Scenario units = base units × volume multiplier
Scenario price = base price × price multiplier
Revenue = sum(scenario units × scenario price)
Delivery hours = sum(scenario units × delivery hours per unit)
Direct cost = delivery hours × base delivery hourly rate × rate multiplier
Gross profit = revenue − direct cost
Operating expenses = sum(fixed departmental costs) + incremental IT cost
EBITDA = gross profit − operating expenses
EBITDA margin = EBITDA / revenue
Target shortfall = max(0, revenue × target margin − EBITDA)
Capacity headroom = available delivery hours − required delivery hours
```

Keep calculations unrounded and round only the displayed margin. Do not add client, segment, service, and regional totals together: each view must independently reconcile to company revenue.

## Expected results

Amounts are USD; delivery requirements and capacity headroom are hours.

| Metric | Base | Optimistic | Conservative |
| --- | ---: | ---: | ---: |
| Revenue | 80,000 | 96,000 | 64,000 |
| Delivery hours | 350 | 420 | 280 |
| Direct delivery cost | 31,500 | 37,800 | 25,200 |
| Gross profit | 48,500 | 58,200 | 38,800 |
| Operating expenses | 23,000 | 24,000 | 23,000 |
| EBITDA | 25,500 | 34,200 | 15,800 |
| EBITDA margin | 31.88% | 35.63% | 24.69% |
| Target margin | 30.00% | 30.00% | 30.00% |
| EBITDA shortfall to target | 0 | 0 | 3,400 |
| Delivery capacity headroom | 100 | 30 | 170 |

Base revenue reconciles across each dimension:

| View | Components | Total |
| --- | --- | ---: |
| Client | SYN-001: 20,000; SYN-002: 30,000; SYN-003: 30,000 | 80,000 |
| Segment | Retail: 20,000; Technology: 60,000 | 80,000 |
| Service type | Advisory: 50,000; Analytics: 30,000 | 80,000 |
| Region | North America: 50,000; APAC: 30,000 | 80,000 |

## What the result means

The base case exceeds the profitability target. The optimistic case also meets the target, but leaves only 30 hours of delivery capacity. The conservative case falls USD 3,400 short of the EBITDA required for a 30% margin. Keep that shortfall visible and evaluate supported pricing, revenue, or cost actions; do not insert a balancing saving.

For a real engagement, replace the illustrative assumptions with supported revenue recognition, staffing/vendor capacity, commitments, timing, and departmental submissions. Add the opening balances and financial schedules required by the full FP&A workflow before claiming a complete company plan.

## Suggested demonstration task

```text
Use the FP&A workflow to demonstrate only its revenue, workload,
departmental cost, and scenario steps with these synthetic CSVs.
Keep the scope to January 2027, one entity, and USD.
Calculate from sales_forecast.csv, cost_plan.csv, and scenario_assumptions.csv.
Produce a scenario summary and reconcile revenue separately by client,
segment, service type, and region. Explain the profitability and capacity gaps.
Compare the calculated results with expected_summary.csv afterward.
Label the result SYNTHETIC DEMONSTRATION and list the full-model steps omitted.
```

The reference values were recomputed from the three input CSVs using decimal arithmetic when this example was added. That check covers the example's arithmetic and dimension totals; it does not establish execution or approval of the complete FP&A workflow.
