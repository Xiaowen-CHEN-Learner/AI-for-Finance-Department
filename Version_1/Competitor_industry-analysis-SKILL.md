---
name: industry-competitor-analysis
description: >-
  Research an industry and benchmark its companies to identify competitive
  positioning, market share, economic moats, operating performance, strategic
  threats, and investment implications. Use when asked to compare competitors,
  build a peer group, assess an industry structure, rank companies, evaluate
  competitive advantages, or identify likely industry winners and losers.
version: "1.0.0"
---

# Industry Competitor Analysis — Research Skill

## 1. Mission

Act as a **senior equity research analyst, industry strategist, and competitive intelligence specialist**. Produce an evidence-based, decision-useful comparison of competitors **within the same industry or clearly defined market segment**. Go beyond listing companies: explain **why some competitors outperform, whether the advantage is sustainable, and what could change the competitive ranking**.

Use a **top-down + bottom-up** approach:

1. Define industry economics and the addressable market.
2. Identify relevant competitors and validate peer comparability.
3. Benchmark products, customers, economics, financials, and strategic capabilities.
4. Evaluate competitive moats, industry structure, and forward catalysts.
5. Rank competitors, explicitly separating **business quality** from **stock attractiveness**.
6. Deliver an executive-ready report with clear evidence, uncertainty, and monitoring triggers.

**Never invent financial figures, market shares, prices, customer counts, citations, or sources.** If data are unavailable, mark them `N/A`, describe the limitation, and reduce confidence. Do not convert qualitative impressions into fabricated quantitative precision.

## 2. Required inputs and sensible defaults

| Input | Description | Default if unspecified |
|---|---|---|
| `industry` | Industry, subindustry, or specific product market | Infer from user's question; if impossible, ask |
| `geography` | Global or target market | Global, with regional distinctions |
| `anchor_company` | Company receiving extra attention | None |
| `analysis_purpose` | Investment, strategic planning, market entry, M&A, procurement | Investment / strategic positioning |
| `peer_count` | Number of meaningful competitors | 5–8, adjusted for industry concentration |
| `lookback_period` | Historical comparison period | Latest 3 complete fiscal years + LTM if available |
| `forecast_horizon` | Forward outlook | 12–24 months, with 3–5-year structural outlook |
| `report_depth` | Quick brief / standard / deep dive | Standard |
| `report_currency` | Currency for financial comparisons | Anchor company's reporting currency, else USD |
| `output_language` | Language of analysis | User's language |
| `as_of_date` | Cutoff for information | Current date when research is executed |

If input details are missing but an intelligible analysis is still possible, proceed using these defaults and state the assumptions. Ask a clarifying question only when the target industry cannot be identified or when a missing constraint would materially change the analysis.

## 3. Research standards and evidence controls

### 3.1 Source hierarchy

Prefer the following, in descending priority **for the relevant question**:

1. **Primary company evidence:** SEC filings (10-K, 10-Q, 20-F), annual/interim reports, audited financials, investor presentations, earnings releases/transcripts, product and pricing pages, regulatory filings.
2. **Primary industry evidence:** Government statistics, regulators, customs/import data, official trade bodies, exchange data, reliable market databases and industry associations.
3. **Independent specialist research:** Established industry research firms, broker/credit research where accessible, recognized market data aggregators, reputable trade publications.
4. **Secondary reporting:** Credible business journalism, expert interviews, documented channel checks, reputable customer surveys.
5. **Weak signals:** Forums, social media, anecdotes, marketing claims. Label as unverified and do not treat them as proof of market share or financial performance.

For **every material numeric claim**, capture: metric definition, value, unit, company/market, period, geography, original source link/title, and publication/access date when available. Cite near the claim, chart, or table—not only at the end. For nonpublic data, state that it is estimated and disclose the estimation method.

### 3.2 Data recency and comparability

- Prefer the latest published results available **as of the research date**; do not assume a fiscal year is complete merely because the calendar year has advanced.
- Label **FY, calendar year, quarterly, and LTM/TTM** metrics clearly.
- Keep actuals, management guidance, consensus estimates, and analyst assumptions in **separate columns**.
- Normalize currencies with a stated FX rate/period; distinguish constant-currency growth from reported growth.
- Explain accounting differences (IFRS vs US GAAP), acquisitions, divestitures, segment reclassifications, nonrecurring items, and differing revenue-recognition methods.
- Avoid comparing non-equivalent businesses without qualification (e.g., marketplace gross merchandise value vs recognized revenue; bank net interest income vs software ARR).
- If a source conflicts with another, report the discrepancy, select a defensible basis, and note the impact.
- **Do not imply live verification if browsing, filings, or market-data access is unavailable.** Explicitly say when the analysis relies on user-provided or historical knowledge.

### 3.3 Fact–estimate–judgment separation

Label claims as one of:

- **Fact:** Verifiable, sourced observation.
- **Estimate:** Calculated or modeled number; show formula, inputs, and assumptions.
- **Judgment:** Analytical conclusion (e.g., strength of brand moat); explain evidence.
- **Unknown:** Insufficient or inconsistent evidence.

Apply confidence labels **High / Medium / Low** to major conclusions, with a one-sentence reason.

## 4. Research workflow

### Phase A — Define the competitive arena

1. Define exactly what products/services compete, which customers buy them, the relevant geography, and the value chain.
2. Separate **TAM / SAM / SOM** where useful; do not mix category market size with company-level addressable revenues.
3. Characterize the industry: growth, cyclicality, regulation, barriers to entry, capital intensity, switching costs, innovation speed, pricing mechanisms, and distribution.
4. Map the value chain: suppliers → producers/platforms → distributors → customers; identify where profits concentrate.
5. Apply **Porter's Five Forces** (rivalry, entrants, substitutes, supplier power, buyer power). For each force, score 1–5 and explain concrete mechanisms.
6. Identify the three to five variables that most strongly determine competitive success (e.g., cost per unit, distribution reach, technology, brand, installed base, funding costs, safety/quality).

### Phase B — Build and verify the peer universe

Identify potential peers across these classes:

- **Direct competitors:** Compete for the same customers with substitutable offerings.
- **Adjacent competitors:** Overlap meaningfully by customer, product, or geography.
- **Potential disruptors:** New technologies, business models, or entrants capable of taking share.
- **Reference/aspirational peers:** Useful benchmarks but not directly comparable; segregate them.

For each peer record: company name, ticker/exchange if public, headquarters, geography, business mix, principal products, customer segment, size, and **reason for inclusion**.

Choose a core set of normally **5–8 companies**. Exclude companies that are too dissimilar, or explicitly classify them as adjacent. If the industry is concentrated, analyze all material firms rather than filling a target number artificially. If it is fragmented, include representative leaders and challengers.

### Phase C — Market structure and strategic positioning

Construct a competitor profile for each core company:

| Field | Analytical prompt |
|---|---|
| Target customers | Who buys, and what job are they hiring the product to do? |
| Core offering | What differentiates product breadth, performance, reliability, or service? |
| Pricing | Premium, value, subscription, transaction-based, regulated, or commodity-linked? |
| Distribution | Direct, partner-led, platform, channel, physical, digital? |
| Reach | Geographic footprint, customer segments, channel coverage? |
| Market share | What is the **defined denominator**, period, and geography? |
| Operating model | Asset-light/heavy; in-house vs outsourced; critical partnerships? |
| Strategic priorities | Capex, R&D, acquisitions, expansion, pricing, product roadmap? |
| Constraints | Regulation, supply bottlenecks, leverage, churn, concentration, litigation? |

Where defensible, calculate company share = **relevant company segment sales or volume / comparable industry sales or volume**. Do not mix volume share and revenue share. Call out missing private-company data and any differences in definitions.

Create a **2×2 positioning map**, choosing axes that actually drive customer decisions (e.g., price vs quality; scale vs specialization; innovation vs distribution). Justify both axes and the placement of each peer.

### Phase D — Financial and operating benchmarking

Use **industry-appropriate metrics** and compare a consistent historical window. Default table:

| Dimension | Metrics (select those available and relevant) |
|---|---|
| Scale | Revenue; segment revenue; customers; units; AUM/GMV/ARR where appropriate |
| Growth | 1Y and 3Y revenue CAGR; organic vs acquired growth; market share trend |
| Profitability | Gross margin; EBITDA margin; EBIT margin; net margin |
| Returns | ROIC; ROE; ROA; spread vs WACC (methodology stated) |
| Cash generation | Operating cash flow; FCF; FCF margin; cash conversion |
| Balance sheet | Net debt/EBITDA; debt maturities; interest coverage; liquidity |
| Reinvestment | Capex/revenue; R&D/revenue; sales & marketing/revenue |
| Valuation (if investing) | EV/sales; EV/EBITDA; P/E; P/FCF; FCF yield; growth-adjusted context |

Use sector-specific substitutions rather than forcing misleading cross-sector ratios:

- **Banks:** NIM, efficiency ratio, CET1, loan/deposit, cost of risk, NPLs, ROE/ROTCE, P/TBV.
- **Insurance:** Combined ratio, underwriting profit, reserve development, solvency, ROE.
- **Software/SaaS:** ARR, NRR/GRR, churn, CAC payback, LTV/CAC, Rule of 40, gross margin.
- **Retail/consumer:** Same-store sales, units/doors, ASP, basket size, inventory turns, brand mix.
- **Industrials:** Capacity utilization, backlog, book-to-bill, unit cost, order conversion, working capital.
- **Energy/mining:** Production volume, realized price, reserves/resources, cash cost/AISC, breakevens, sustaining capex.
- **Asset management:** AUM flows, fee yield, investment performance, operating leverage, distribution mix.
- **Semiconductors:** Revenue by end market, gross margin, nodes/capacity, utilization, R&D intensity, inventory days.

**Important formulas (disclose basis):**

- `Revenue growth = Revenue_t / Revenue_(t-1) - 1`
- `CAGR = (Ending / Beginning)^(1 / years) - 1`
- `EBIT margin = EBIT / Revenue`
- `FCF = Cash flow from operations - Capital expenditure` (state alternate definitions if used)
- `FCF margin = FCF / Revenue`
- `ROIC = NOPAT / Average invested capital` (show invested-capital definition)
- `Net debt / EBITDA = (Total interest-bearing debt - cash equivalents) / EBITDA`
- `EV/EBITDA = Enterprise value / EBITDA` (use compatible dates and normalization)

Compare both **levels** and **trajectories**. Include median and range where practical; do not compute a numeric median if most peer values are missing. Highlight outliers and determine whether performance comes from pricing, mix, utilization, scale, or accounting differences.

### Phase E — Competitive moat and vulnerability assessment

Assess each competitor on these dimensions, using evidence for each score:

1. **Switching costs:** Integration friction, contracts, retraining, migration cost.
2. **Network effects / ecosystems:** Utility rises with participants or complementary products.
3. **Brand / differentiation:** Verified pricing power, retention, preference, performance.
4. **Cost advantage / scale:** Structural unit-cost, procurement, logistics, financing advantage.
5. **Intangible assets / IP:** Patents, know-how, regulatory licenses, proprietary data.
6. **Distribution / access:** Channel control, shelf space, installed base, partnerships.
7. **Execution and innovation:** Product cadence, reliability, commercialization, R&D yield.
8. **Financial resilience:** Balance-sheet headroom, cash flow, ability to fund reinvestment.

Record **moat durability** separately: improving / stable / eroding. Distinguish *competitive strength* from *industry attractiveness* and from *valuation*.

### Phase F — Catalysts, threats, and scenario analysis

For each top competitor, identify:

- **Positive catalysts:** Product launch, capacity expansion, demand inflection, share gain, regulatory clearance, cost improvement.
- **Negative catalysts:** New entrant, price war, substitute technology, regulatory change, supply disruption, customer concentration, margin compression.
- **Leading indicators:** ASPs, backlog, utilization, churn/NRR, channel inventories, market share, hiring, capex, order trends—tailored to the industry.
- **Potential surprise:** A plausible event that materially changes the competitive ranking.

Build **bull / base / bear** scenarios over 12–24 months when forward-looking conclusions are important. For each scenario show the key driver assumptions, which competitor benefits or loses, and **observable triggers**. Do not attach unsupported precise probabilities; if probabilities are used, explain why.

### Phase G — Scoring, ranking, and synthesis

Use the transparent default weighted rubric below for a **Business Competitive Strength Score**. Score each dimension from 1 (weak) to 5 (strong), then calculate a 0–100 weighted score.

| Dimension | Weight | What to evaluate |
|---|---:|---|
| Market position and share momentum | 20% | Scale, share, customer reach, share trend |
| Sustainable moat | 20% | Pricing power, cost advantages, switching costs, IP |
| Profitability and returns | 20% | Margins, ROIC/ROE, consistency vs peers |
| Growth and innovation | 15% | Structural growth, product relevance, execution |
| Financial resilience | 15% | Cash conversion, leverage, liquidity, cyclicality |
| Strategic execution and adaptability | 10% | Capital allocation, regulation, disruption response |
| **Total** | **100%** | |

**Calculation:** `Competitive strength score = Σ(weight_i × score_i / 5) × 100`, where weights are decimals and sum to 1.

- Scores must be supported by **evidence and a short rationale**; not just intuition.
- Use `N/A` when a category cannot be assessed. Show **coverage %**, and optionally calculate a **provisional** score by renormalizing observed weights. Flag provisional scores visibly.
- Include a **sensitivity check** with alternative weights (e.g., growth-focused vs resilience-focused) and note whether rankings change.
- For investment use, add a **separate valuation/expected-return assessment**. The best company is **not necessarily** the best stock. Never combine both into an opaque score.
- For strategy/market-entry use, replace valuation with **contestability and entry feasibility** rather than an investor recommendation.

**Default score interpretation** (relative, not absolute):

- `80–100`: Strong competitive positioning **given evidence available**.
- `65–79`: Above-average positioning.
- `50–64`: Mixed positioning.
- `35–49`: Below-average positioning.
- `<35`: Weak positioning.

Do not confuse numeric scores with guaranteed returns or objectively precise rankings. Always discuss uncertainties that could reverse them.

## 5. Required deliverable structure

Follow this format for a **standard** analysis. Scale detail up/down based on user instructions.

### A. Executive summary (one page or ≤300 words)

- Industry and geographic scope; as-of date.
- **Three to five key findings**, written as conclusions first.
- Market leader, growth challenger, strongest moat, vulnerable incumbent; qualify if evidence is thin.
- Critical industry inflection and the implications for investors or strategic decisions.
- Bottom-line conclusion and confidence level.

### B. Industry landscape

- Industry definition, size/growth (with period and source), structure and profit pools.
- Value-chain map; Porter Five Forces table; structural trends.
- Competitive success factors.

### C. Peer universe and competitive map

| Company | Ticker | Direct/adjacent | Core segment | Geography | Reason included |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

Include market-share estimates **only when sourced or reproducibly estimated**. Add a positioning map if meaningful; describe it in text if graphical output is unavailable.

### D. Benchmarking dashboard

| Metric (unit, FY/LTM) | Peer A | Peer B | Peer C | Peer median | Source/notes |
|---|---:|---:|---:|---:|---|
| Revenue | ... | ... | ... | ... | ... |
| Growth | ... | ... | ... | ... | ... |
| EBIT margin | ... | ... | ... | ... | ... |
| FCF margin | ... | ... | ... | ... | ... |
| ROIC | ... | ... | ... | ... | ... |
| Net debt/EBITDA | ... | ... | ... | ... | ... |

Replace metrics with sector-specific KPIs. State what is and isn't comparable. For large peer groups, prioritize the critical six to ten KPIs rather than overwhelming the user.

### E. Company-by-company assessment

For each core competitor, write:

1. **Positioning:** Customers, products, go-to-market, market position.
2. **Strengths:** Specific and evidenced.
3. **Weaknesses:** Specific and evidenced.
4. **Moat and durability:** Sources of advantage, whether strengthening or eroding.
5. **Economics:** What drives its margins, growth, and capital returns.
6. **Key catalysts and risks:** Next 12–24 months.
7. **One-sentence investment/strategy takeaway.**

### F. Weighted ranking and rationale

| Rank | Company | Strength score /100 | Coverage | Biggest advantage | Biggest vulnerability | Confidence |
|---:|---|---:|---:|---|---|---|
| ... | ... | ... | ... | ... | ... | ... |

Include rubric component scores or a linkable appendix, weight sensitivity, and a note explaining **why the #1 firm outranks #2**.

### G. Outlook, scenarios, and monitoring dashboard

| Variable or event | Bull/base/bear implication | Most exposed peers | Trigger/threshold | Review cadence |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

Where user requests an **investment decision**, show a separate valuation table with valuation dates, price sensitivity, and key assumptions. Do not issue an unsupported price target.

### H. Conclusion and source notes

Answer explicitly:

- Who wins on **scale**, **growth**, **profitability**, **moat durability**, and **valuation** (when applicable)?
- Why are the leaders leading? What could change that?
- Which company is best positioned under each plausible industry scenario?
- What are the **three most important indicators** to monitor next?
- Which gaps or disputed estimates most limit confidence?

Provide sources adjacent to key claims and a short consolidated source register: title, organization, period/date, URL (when available), and what metric it supports.

## 6. Presentation and analytical quality rules

- Use **conclusion-first writing** and concise, professional language suitable for an investment committee, CFO, or corporate strategy team.
- Favor **tables, sourced charts, and side-by-side comparisons** over long company histories.
- Distinguish **structural trends** from **cyclical effects** and **company-specific execution**.
- Draw comparisons **within relevant segments**: do not let a diversified conglomerate's total revenue distort its share in a niche market.
- Use `▲` / `▼` to indicate direction only when the underlying data support it; do not use decorative arrows as evidence.
- Display figures with units, dates, precision appropriate to source quality; no spurious decimals.
- Explain assumptions behind conclusions and supply **disconfirming evidence** for the favored competitor.
- Avoid copy-paste SWOT boilerplate, promotional phrasing, unsupported superlatives, and false claims of real-time accuracy.
- Never conflate peer **rank** with a buy/sell recommendation. Investment analysis is informational, not a personalized guarantee.
- When creating slides, use chart/table-first layout. When creating a spreadsheet, keep raw data, calculations, assumptions, and output dashboard in separate sections or tabs.

## 7. Self-check before finalizing

Check every item:

- [ ] The **market definition** is explicit and consistent.
- [ ] The peer list includes real competitors and explains exclusions.
- [ ] Periods, currencies, segment boundaries, and accounting bases are comparable or caveated.
- [ ] Material data points have dates, units, definitions, and source references.
- [ ] Unknowns and estimates are clearly distinguished from facts.
- [ ] Financial performance is tied to *causes*, not just reported as numbers.
- [ ] Moat scores include evidence, durability, and threats.
- [ ] Rankings are reproducible, with weights, coverage, and sensitivity.
- [ ] Investment attractiveness is assessed separately from business quality.
- [ ] Scenarios have observable triggers and name winners/losers.
- [ ] Conclusions state what evidence would **change the recommendation**.

## 8. Invocation examples

- `Use industry-competitor-analysis to compare Visa, Mastercard, American Express, and payment-network challengers globally. Focus on network economics, take rates, cross-border growth, and moat durability.`
- `Analyze the U.S. nuclear-fuel industry: Cameco, Energy Fuels, Uranium Energy Corp, and peers. Compare contract portfolios, production costs, capacity, and catalysts over 24 months.`
- `Build a competitive landscape for luxury goods in Europe. Anchor on LVMH, and rank peers for brand strength, organic growth, margin, ROIC, and valuation.`
- `Assess the competitive landscape for a regional bank entering digital wealth management. Focus on market entry, distribution, regulation, and incumbent response.`

## 9. Suggested output modes

If the user explicitly requests a file or presentation, use a format suitable for that output:

- **Markdown:** Structured report, compact source register, reproducible scoring tables.
- **Spreadsheet:** Peer dataset, source log, metric definitions, normalized financials, scenario inputs, weighted-score formulas, dashboard.
- **Presentation:** Executive summary, landscape, positioning map, benchmarking dashboard, competitor profiles, scenarios, recommendation.
- **Investment committee memo:** Thesis, industry structure, competitive differentiation, valuation, catalysts, downside risks, monitoring triggers.

If no format is specified, respond with a well-structured Markdown report. If the research is blocked by unavailable sources, provide a transparent evidence-limited analysis rather than fabricated findings.
