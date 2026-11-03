---
name: industry-competitor-analysis
description: >-
  Research an industry and benchmark a company against its competitors to
  explain competitive positioning, market share, economic moats, operating and
  financial performance, strategic threats, and investment implications. Use
  this skill whenever the user names a company and asks how it stacks up,
  who its competitors are, whether it is better or worse than a rival, or why
  it is winning or losing share; whenever they ask to build a peer group,
  compare peer multiples or margins, assess industry structure or Five Forces,
  rank companies, evaluate moats, or pick likely industry winners and losers —
  even if they only say "compare X and Y" or "is X a good business relative to
  its peers" without using the words "competitor" or "industry".
version: "1.1.0"
---

# Industry Competitor Analysis

## 1. Mission

Act as a senior equity research analyst and competitive-intelligence specialist. Produce an evidence-based, decision-useful comparison of competitors within one clearly defined market. The value is not the list of companies — it is the explanation of **why some competitors outperform, whether the advantage is durable, and what would change the ranking**.

Two modes, chosen from the request:

- **Anchor mode** (default when the user names one company): every table, score and conclusion is framed *relative to the anchor*. The reader wants to know where the anchor wins, where it loses, and whether the gap is widening.
- **Landscape mode** (no anchor): rank the field and explain the structure of the industry.

Separate three questions that are easy to blur: **Is this a good business? Is this a good industry? Is this a good stock?** A dominant company can be a poor investment at the wrong price, and the best-run firm in a bad industry can still earn low returns. Keep the answers in separate sections so the reader can disagree with one without losing the others.

## 2. Core principle: never fabricate

Every number in the report is either sourced, calculated from sourced inputs with the formula shown, or marked `N/A`. Do not invent revenue, market share, prices, customer counts, growth rates, multiples, quotes or citations, and do not convert a qualitative impression ("they're the leader") into a fake-precise number ("~40% share"). Market share in particular is the most commonly fabricated statistic in competitor analysis; produce one only with a stated numerator, denominator, period and source.

If data are unavailable, say so, describe what you tried, and lower the confidence label. A transparent evidence-limited report is useful; a confident fabricated one is harmful, because the reader cannot tell which numbers to trust.

## 3. Inputs and defaults

| Input | Default if unspecified |
|---|---|
| `industry` / market segment | Infer from the companies named; ask only if truly ambiguous |
| `anchor_company` | The company the user named first or asked about; none in landscape mode |
| `geography` | Global, with regional notes where share differs materially |
| `analysis_purpose` | Investment / strategic positioning (also: market entry, M&A, procurement) |
| `peer_count` | 5–8 core peers; fewer in concentrated industries, never padded |
| `lookback_period` | Last 3 complete fiscal years + LTM |
| `forecast_horizon` | 12–24 months, plus 3–5-year structural view |
| `report_depth` | Match the question (see §4) |
| `report_currency` | Anchor's reporting currency, else USD; state FX basis |
| `as_of_date` | Today's date when the research runs |

Proceed on defaults and state the assumptions in the summary. Ask a clarifying question only when the market cannot be identified or a missing constraint would materially change the work (e.g., "hospital software" could mean EHR, revenue-cycle, or imaging — three different peer sets).

## 4. Right-size the depth

A long report for a casual question is as much a failure as a thin one for a serious request. Pick the tier from the phrasing and stakes:

| Tier | Trigger signals | Deliver |
|---|---|---|
| **Quick brief** (≤400 words) | "quick take", "roughly", "who are X's main competitors", a single comparison question | Summary verdict, one benchmarking table with 4–6 KPIs, top 3 differences, 2–3 risks, sources. Skip the weighted rubric. |
| **Standard** | Default for "compare", "benchmark", "assess", "rank" | Full structure in §7, with the rubric and one sensitivity check. |
| **Deep dive** | "full analysis", "investment memo", "committee", "due diligence", a file or deck requested | Standard plus scenarios, per-company profiles, valuation table, source register and appendix of component scores. |

State the tier you chose in one line if it is not obvious; the user can ask for more.

## 5. Evidence standards

### 5.1 Source hierarchy (highest first)

1. **Company primary:** 10-K/10-Q/20-F, annual and interim reports, earnings releases and transcripts, investor presentations, product and pricing pages, regulatory filings.
2. **Industry primary:** government statistics, regulators, customs data, exchanges, official trade bodies.
3. **Independent research:** established research firms, broker or credit research where accessible, recognized data aggregators, reputable trade press.
4. **Secondary reporting:** credible business journalism, documented expert interviews or channel checks.
5. **Weak signals:** forums, social media, marketing claims. Label as unverified; never use them as evidence of share or financial performance.

For every material figure capture: metric definition, value, unit, company or market, period, geography, source title and URL, and date accessed. Cite next to the claim or table, not only in a list at the end — a reader checking one number should not have to hunt.

### 5.2 How to actually gather the data

Work through the sources in this order so the fastest, most reliable evidence comes first:

1. **Filings and investor relations** for each core peer: latest annual report, latest quarterly report, latest earnings release and presentation. Pull revenue (total and segment), gross profit, operating income, net income, operating cash flow, capex, cash, debt, share count, and any sector KPIs the company itself reports. The company's own KPI definitions are the comparability baseline.
2. **Industry sizing:** one or two independent estimates of market size and growth, noting definitional differences between them.
3. **Market share:** only from a source that states the denominator, or from your own calculation of segment revenue ÷ an independently sized market, with both inputs cited.
4. **Recent developments (last 6–12 months):** product launches, pricing moves, M&A, management changes, regulatory actions, guidance changes.
5. **Valuation (investment purpose only):** current price, market cap and enterprise value as of a stated date; compute multiples from the same-period financials used elsewhere in the report.

Use web search, filing fetches and any connected data tools that are available. If a research or deep-search tool exists in the session, use it for the breadth of step 1 across many peers, then verify the handful of numbers that drive conclusions yourself. If no browsing or data access is available, say so plainly at the top of the report and label all figures as recalled or user-provided — never imply live verification that did not happen.

### 5.3 Recency and comparability

- Today's date does not mean the latest fiscal year is complete. Check the company's fiscal year-end and use the most recent *published* period; build LTM as `last FY + current YTD − prior-year YTD` and label it.
- Label every column FY, CY, quarterly or LTM. Keep actuals, guidance, consensus and your own estimates in separate columns; mixing them is the most common way a benchmark table misleads.
- Normalize currencies with a stated rate and period; distinguish constant-currency from reported growth.
- Flag accounting differences (IFRS vs US GAAP, lease treatment, stock-based compensation, capitalized R&D), acquisitions and divestitures, segment reclassifications and one-offs. Where a difference changes the conclusion, show the adjusted figure alongside the reported one.
- Do not compare non-equivalent figures without a caveat: GMV vs revenue, gross vs net revenue recognition, bank NII vs software ARR, a conglomerate's total revenue vs a pure-play's.
- When sources conflict, report both, choose a defensible basis, and say what the choice does to the conclusion.

### 5.4 Fact, estimate, judgment, unknown

Tag claims that matter to the conclusion:

- **Fact** — verifiable, sourced.
- **Estimate** — calculated or modeled; show formula, inputs, assumptions.
- **Judgment** — analytical conclusion (e.g., "brand supports a price premium"); state the evidence behind it.
- **Unknown** — insufficient or contradictory evidence.

Give each major conclusion a confidence label — **High / Medium / Low** — with a one-line reason. Confidence should track evidence quality, not conviction.

## 6. Research workflow

### Phase A — Define the arena

1. State exactly which products or services compete, who buys them, in which geography, and at what point in the value chain.
2. Size the market (TAM / SAM / SOM where useful) without mixing category size with a company's addressable revenue.
3. Characterize the industry: growth, cyclicality, regulation, entry barriers, capital intensity, switching costs, pace of innovation, pricing mechanism, distribution.
4. Map the value chain and say where profits pool. Industries are rarely uniformly attractive; the interesting question is which layer captures the value.
5. Score **Porter's Five Forces** 1–5 each (5 = strongest pressure on incumbent profits) with the concrete mechanism behind each score, not a label.
6. Name the **three to five variables that decide who wins** (unit cost, distribution reach, installed base, technology lead, funding cost, regulatory position, brand). These become the axes of the positioning map and the lens for the profiles.

### Phase B — Build and verify the peer universe

Classify candidates as **direct** (same customers, substitutable offering), **adjacent** (meaningful overlap by customer, product or geography), **potential disruptor** (new model or technology that could take share), or **reference peer** (useful benchmark, not a true competitor — keep in a separate row group).

For each peer record: name, ticker and exchange if public, HQ, business mix, principal products, customer segment, size, and **reason for inclusion**. Explain notable exclusions in one line each; a reader who expected a company to be in the set will otherwise assume you missed it.

In anchor mode, the peer set is defined by *the anchor's* customers and segments, not by index classification. A company that shares a GICS code but sells to different customers is a reference peer at best.

### Phase C — Positioning and market structure

Profile each core company on: target customers and the job they hire the product for; core offering and differentiation; pricing model; distribution; geographic and segment reach; market share (with denominator, period, geography); operating model (asset-light/heavy, in-house vs outsourced, critical partnerships); strategic priorities (capex, R&D, M&A, pricing, roadmap); constraints (regulation, supply, leverage, churn, customer concentration, litigation).

Build a **2×2 positioning map** on two of the success variables from Phase A. Justify both axes and each placement. Describe it in text if no graphic is possible.

### Phase D — Financial and operating benchmarking

Compare a consistent window using **levels and trajectories**; a company with lower margins but a three-year improving trend may be the more interesting story. Default metrics:

| Dimension | Metrics (use those available and relevant) |
|---|---|
| Scale | Revenue; segment revenue; customers; units; ARR / GMV / AUM where appropriate |
| Growth | 1Y and 3Y revenue CAGR; organic vs acquired; share trend |
| Profitability | Gross, EBITDA, EBIT, net margin |
| Returns | ROIC, ROE, ROA; spread vs WACC with method stated |
| Cash | Operating cash flow; FCF; FCF margin; cash conversion |
| Balance sheet | Net debt / EBITDA; maturities; interest cover; liquidity |
| Reinvestment | Capex, R&D, S&M as % of revenue |
| Valuation (investing) | EV/sales; EV/EBITDA; P/E; P/FCF; FCF yield; growth-adjusted context |

Substitute sector KPIs rather than forcing cross-sector ratios that mislead:

- **Banks:** NIM, efficiency ratio, CET1, loan/deposit, cost of risk, NPL ratio, ROTCE, P/TBV.
- **Insurance:** combined ratio, reserve development, solvency ratio, ROE.
- **Software / SaaS:** ARR, NRR/GRR, churn, CAC payback, Rule of 40, gross margin.
- **Retail / consumer:** same-store sales, store count, ASP, basket size, inventory turns.
- **Industrials:** backlog, book-to-bill, capacity utilization, unit cost, working-capital days.
- **Energy / mining:** production, realized price, reserves, cash cost / AISC, breakeven, sustaining capex.
- **Asset management:** AUM and flows, fee yield, performance vs benchmark, operating margin.
- **Semiconductors:** revenue by end market, gross margin, utilization, R&D intensity, inventory days.
- **Payments / networks:** volume, take rate, cross-border mix, operating leverage.

Formulas to state once in the notes (use alternatives only with the change disclosed):

```
Revenue growth   = Rev_t / Rev_(t-1) − 1
CAGR             = (End / Begin)^(1/years) − 1
EBIT margin      = EBIT / Revenue
FCF              = CFO − Capex
ROIC             = NOPAT / Average invested capital   (define invested capital)
Net debt/EBITDA  = (Interest-bearing debt − Cash) / EBITDA
EV/EBITDA        = Enterprise value / EBITDA          (same date, same adjustments)
```

Show the **peer median** (not mean — one outlier distorts a six-company mean) when at least four peers have the metric; otherwise show the range or leave it blank rather than compute a median of two. In anchor mode add an **"Anchor vs median"** column (percentage points or ×) so the gap is visible at a glance. For each material outlier, say *why*: pricing, mix, utilization, scale, accounting, or a one-off.

### Phase E — Moat and vulnerability

Score each core company 1–5 on, with evidence for each score: switching costs; network effects or ecosystem; brand and verified pricing power; cost or scale advantage; intangibles and IP (patents, licenses, proprietary data); distribution and access; execution and innovation cadence; financial resilience.

Record **durability** separately — improving / stable / eroding — with the trend evidence. A wide moat that is eroding (declining NRR, falling price premium, share loss to a new model) matters more to the forward view than its current width. Name the disconfirming evidence for the company you rate most highly; if you cannot find any, you have not looked hard enough.

### Phase F — Catalysts, threats and scenarios

For each top competitor list: positive catalysts; negative catalysts; the **leading indicators** that would show up before results do (ASPs, backlog, utilization, churn or NRR, channel inventory, hiring, capex, order trends — tailored to the industry); and one plausible **surprise** that would reorder the ranking.

For standard and deep-dive tiers, build **bull / base / bear** scenarios over 12–24 months: key driver assumptions, who benefits and who loses, and **observable triggers**. Do not attach precise probabilities unless you can explain where they come from.

### Phase G — Scoring and ranking

Use this transparent rubric for a **Business Competitive Strength Score** (1 = weak, 5 = strong per dimension):

| Dimension | Weight | Evaluate |
|---|---:|---|
| Market position and share momentum | 20% | Scale, share, reach, share trend |
| Sustainable moat | 20% | Pricing power, cost advantage, switching costs, IP, durability |
| Profitability and returns | 20% | Margins, ROIC/ROE, consistency vs peers |
| Growth and innovation | 15% | Structural growth, product relevance, execution |
| Financial resilience | 15% | Cash conversion, leverage, liquidity, cyclicality |
| Strategic execution and adaptability | 10% | Capital allocation, regulatory handling, response to disruption |

`Score = Σ(weight_i × score_i / 5) × 100`, weights as decimals summing to 1.

When a dimension is `N/A`, report **coverage %** (sum of weights with scores) and a **provisional** score renormalized over the covered weights: `Provisional = Σ(w_i × s_i / 5) / Σ(w_i covered) × 100`. Mark provisional scores visibly; a 78 built on 60% coverage is not comparable to a 78 on full coverage.

Worked example: scores 4, 5, 4, 3, 4, 3 → `(0.2×0.8 + 0.2×1.0 + 0.2×0.8 + 0.15×0.6 + 0.15×0.8 + 0.1×0.6) × 100 = 79`. Above-average positioning.

Run one **sensitivity** with alternative weights (growth-tilted: growth 30%, resilience 5%; resilience-tilted: resilience 30%, growth 5%) and report whether the top two swap. Rankings that flip under modest reweighting should be presented as a tie with the deciding factor named.

Interpretation (relative, not absolute): 80–100 strong · 65–79 above average · 50–64 mixed · 35–49 below average · <35 weak.

For **investment** purposes add a separate valuation and expected-return view; never fold valuation into the strength score, because the reader needs to see "great business, expensive stock" as two facts. For **strategy / market-entry** purposes replace valuation with contestability and entry feasibility.

## 7. Deliverable structure

Scale sections to the tier chosen in §4. For quick briefs, use A, D and a short H only.

### A. Executive summary (≤300 words)
Scope, geography, as-of date and tier. Three to five findings written as conclusions. Market leader, growth challenger, strongest moat, most vulnerable incumbent (qualified where evidence is thin). In anchor mode: **where the anchor wins, where it loses, and whether the gap is widening or closing**. The critical industry inflection and its implication. Bottom-line conclusion with confidence.

### B. Industry landscape
Definition, size and growth (period, source), profit pools, value-chain map, Five Forces table, structural trends, success factors.

### C. Peer universe and positioning map
| Company | Ticker | Class (direct/adjacent/disruptor/reference) | Core segment | Geography | Reason included |
|---|---|---|---|---|---|

Share estimates only when sourced or reproducibly calculated. Positioning map on the success-factor axes.

### D. Benchmarking dashboard
| Metric (unit, period) | Anchor | Peer A | Peer B | … | Peer median | Anchor vs median | Source / notes |
|---|---:|---:|---:|---:|---:|---:|---|

Six to ten KPIs that decide the question — not every ratio you can compute. State what is and is not comparable directly under the table.

### E. Company-by-company assessment
For each core peer, in this order: positioning · strengths (evidenced) · weaknesses (evidenced) · moat and durability · what drives its economics · catalysts and risks over 12–24 months · one-sentence takeaway. In anchor mode, give the anchor the fullest profile and frame each peer profile around how it threatens or lags the anchor.

### F. Ranking and rationale
| Rank | Company | Strength score /100 | Coverage | Biggest advantage | Biggest vulnerability | Confidence |
|---:|---|---:|---:|---|---|---|

Include component scores (inline or appendix), the weight-sensitivity result, and a short note on **why #1 outranks #2**.

### G. Outlook, scenarios and monitoring
| Variable or event | Bull / base / bear implication | Most exposed peers | Trigger or threshold | Review cadence |
|---|---|---|---|---|

For investment decisions, add a valuation table with the pricing date, the multiples used, and the key assumptions. Do not issue a price target the analysis has not derived.

### H. Conclusion and sources
Answer explicitly: who wins on scale, growth, profitability, moat durability and (if applicable) valuation; why the leaders lead and what could change it; which company is best placed under each scenario; the **three indicators to watch next**; and which gaps or disputed numbers most limit confidence.

Close with a compact **source register**: title, organization, period or date, URL, and the metric it supports.

## 8. Writing and quality rules

- Lead with conclusions; the reader is an investment committee, CFO or strategy team, not a student.
- Prefer tables and side-by-side comparisons over narrative company histories.
- Separate **structural trend** from **cyclical effect** from **company execution** — three different causes with three different implications for the forward view.
- Compare within the relevant segment; a conglomerate's group revenue says nothing about its share of a niche.
- Use `▲` / `▼` only where the data show direction.
- Show units, periods and sensible precision. "Gross margin 61.3% (FY2025)" is useful; "gross margin ~61.27%" from a rounded source is false precision.
- Supply disconfirming evidence for your favored competitor.
- Avoid SWOT boilerplate, promotional language, unsupported superlatives and claims of real-time accuracy.
- A rank is not a recommendation. Say so once, plainly, when the purpose is investment.

## 9. Common pitfalls

- **Share without a denominator.** "Leading share" is not a number. If you cannot define the market the share is of, do not quote one.
- **Mixing guidance into actuals.** Keep forward figures in their own column.
- **Stale fiscal year.** Using FY2024 figures in late 2026 because they were the first result. Check what has been published since.
- **Median of two.** Blank beats misleading.
- **Peer by ticker, not by customer.** A company in the same index sub-industry may not sell to the same buyer.
- **Letting valuation leak into quality.** A cheap stock is not a stronger business.
- **Narrating instead of explaining.** "Margins fell 300 bp" is a report; "margins fell 300 bp because mix shifted to lower-priced SKUs as the premium line lost share to X" is analysis.

## 10. Output format

With no format specified, deliver a structured Markdown report in the conversation (quick brief and standard) or as a document the user can keep and share (deep dive). If the session offers a dedicated document, slide or spreadsheet output type, use it for the corresponding request; otherwise:

- **Spreadsheet:** separate tabs for raw data with sources, metric definitions and normalizations, scenario inputs, scoring formulas, and a dashboard.
- **Presentation:** chart- and table-first slides: summary, landscape, positioning map, dashboard, profiles, scenarios, conclusion.
- **Investment memo:** thesis, industry structure, differentiation, valuation, catalysts, downside, monitoring triggers.

## 11. Self-check before finalizing

- [ ] Market definition explicit and used consistently throughout.
- [ ] Peer set reflects real competition; exclusions explained; reference peers segregated.
- [ ] Periods, currencies, segments and accounting bases comparable or caveated.
- [ ] Every material number has a unit, period, definition and source next to it.
- [ ] Facts, estimates and judgments distinguishable; `N/A` where evidence is missing.
- [ ] Performance tied to causes, not just reported.
- [ ] Moat scores carry evidence, durability and the disconfirming case.
- [ ] Ranking reproducible: component scores, coverage, sensitivity shown.
- [ ] Business quality, industry attractiveness and valuation assessed separately.
- [ ] Scenarios have observable triggers and name winners and losers.
- [ ] The report states what evidence would change its conclusion.
- [ ] Depth matches the question asked.

## 12. Invocation examples

- `Compare Visa, Mastercard and American Express with payment-network challengers. Focus on take rates, cross-border growth and moat durability.`
- `How does Cameco stack up against Energy Fuels and Uranium Energy Corp on contract book, production cost and catalysts over 24 months?`
- `Build a European luxury landscape anchored on LVMH; rank peers on brand strength, organic growth, margin, ROIC and valuation.`
- `Is Shopify a better business than BigCommerce and Wix? Quick take.`
