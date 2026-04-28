# The Right Way to Hedge — Commodity Risk Management Framework

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cgorricho/the-right-way-to-hedge/blob/main/GDR_40.ipynb)
[![Author](https://img.shields.io/badge/Author-Carlos_Gorricho-blue)](https://github.com/cgorricho)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-carlos--gorricho-blue?logo=linkedin)](https://linkedin.com/in/carlos-gorricho-data-driven-c-level)

> *A Python implementation of McKinsey's strategic commodity hedging framework, grounded in 25+ years of C-suite financial leadership including design and execution of a $300M commodity risk management program.*

---

## What This Is

This notebook implements the analytical framework from McKinsey's article **"The Right Way to Hedge"** — a structured, strategy-first approach to commodity risk management that contrasts sharply with the reactive, siloed hedging programs most companies actually run.

The article's central thesis: most companies hedge the wrong things, in the wrong amounts, for the wrong reasons. They hedge under pressure from capital markets rather than from a clear-eyed analysis of which exposures actually threaten the company's financial health or strategic plans. The result: hedging programs that destroy more value than the risks they were designed to contain.

This notebook translates the McKinsey framework into executable Python code — making the concepts quantifiable, testable, and auditable.

---

## The McKinsey Framework: Core Principles

### 1. Hedge Only Material Exposures

Companies should hedge only exposures that pose a material risk to their financial health or threaten their strategic plans. The framework begins by separating exposures that genuinely threaten the company from those that create noise but not risk.

**Implementation in this notebook:** Materiality thresholds are computed as a function of EBITDA, cash reserves, and debt service obligations — not as arbitrary percentage targets.

### 2. Understand True Risk Capacity

Before deciding *what* to hedge, a company must understand *how much* risk it can actually absorb. This requires:

- Mapping cash flow requirements: interest, principal, dividends, sustaining CAPEX, growth CAPEX
- Identifying the probability distribution of commodity price outcomes
- Quantifying the gap between worst-case scenarios and available cash buffers

**The two failure modes:**
- **Over-insured companies** (high free cash flow, excess hedging) — destroying shareholder value by paying for protection they don't need
- **Over-extended companies** (recent distress, large capital programs) — failing to hedge exposures that could trigger financial distress

### 3. Aggregate Risk Across the Enterprise

Too many hedging programs target the nominal risks of "siloed" businesses rather than a company's net economic exposure — aggregated risk across the broad enterprise that also includes the indirect risks.

Classic failure case: one business unit hedges a $700M FX exposure while a second business unit is simultaneously sourcing $500M from the same market. The net exposure is $200M — but the siloed hedge creates a $500M gross overhedge.

**Implementation:** Net exposure calculation aggregates long and short commodity positions across all business units before any hedging decisions are made.

### 4. Explore Non-Financial Alternatives First

An effective risk management program often includes **non-financial levers** that can reduce risk more effectively and cheaply than derivatives:

- **Contracting:** Pass risk through to counterparties via pricing clauses
- **Vertical integration:** Acquire upstream or downstream assets that naturally offset exposure
- **Operational flexibility:** Adjust activity levels, product specifications, or facility scheduling when input costs peak
- **Capital structure:** Hold additional cash reserves as a buffer against price volatility

Financial hedges should be the *last resort*, not the default tool.

### 5. Evaluate Cost vs. Benefit Rigorously

Companies should test the effectiveness of different risk mitigation strategies by quantitatively comparing the total cost of each approach with the benefits.

This cost depends on the organization's fundamental view of commodity price floors and ceilings — not on what the futures market implies. A company that believes gas prices will stay between $5.00–$8.00/MMBtu should evaluate a hedge at $5.50 differently than one with no directional view.

---

## Why This Matters: The Author's Context

This notebook was built by a CFO who has lived this problem — not as an academic exercise.

**Carlos Gorricho** served as CFO & VP Business Development at **Riopaila Castilla S.A.**, Colombia's largest integrated agribusiness conglomerate, managing 35,000+ hectares across the full agricultural value chain. In that role he:

- **Designed and executed a $300M commodity risk management program** using derivative instruments for sugar price and foreign exchange hedging
- Managed the full spectrum of agricultural commodity exposures: spot price risk, basis risk, FX translation risk, and production volume uncertainty
- Built the internal analytical capability to evaluate hedge effectiveness and optimize hedge ratios
- Presented hedging strategy and risk positions to board-level stakeholders and lenders

The McKinsey framework described in the article is not theoretical from this perspective — it describes exactly the discipline required to run a commodity risk program at scale without destroying shareholder value in the process.

---

## Notebook: GDR_40.ipynb

### What GDR_40 Stands For

**GDR** refers to the **Gross Delta Risk** analytical framework — a structured approach to measuring and managing net commodity exposure at the enterprise level. The **40** denotes the model iteration.

### What the Notebook Covers

The notebook implements the following analytical sequence:

```
1. Exposure Identification
   └── Map all commodity exposures across business units
   └── Separate direct exposures (purchase/sale commitments) from indirect exposures

2. Net Exposure Aggregation
   └── Aggregate long and short positions across the enterprise
   └── Calculate natural hedges (internal offsets)
   └── Quantify residual net exposure

3. Materiality Assessment
   └── Compute exposure as % of EBITDA, cash, and debt service
   └── Apply materiality thresholds to identify hedgeable exposures
   └── Separate material from immaterial risks

4. Risk Capacity Analysis
   └── Model cash flow waterfall: interest → principal → dividends → CAPEX
   └── Stress test against commodity price scenarios
   └── Identify the "distress threshold" — the price level at which liquidity fails

5. Hedge Strategy Evaluation
   └── Model financial hedging alternatives (futures, swaps, options, collars)
   └── Model non-financial alternatives (contracting, operational flexibility)
   └── Compare total cost and effectiveness of each approach

6. Optimal Hedge Ratio
   └── Compute the hedge ratio that minimizes the probability of financial distress
   └── Distinguish from the ratio that minimizes earnings volatility (not the same)

7. Backtesting & Validation
   └── Apply strategy to historical price data
   └── Evaluate hedge effectiveness using standard metrics (R², hedge ratio stability)
   └── Assess basis risk and liquidity constraints
```

### Key Outputs

| Output | Description |
|---|---|
| Net exposure by commodity | Aggregated long/short positions across the enterprise |
| Materiality matrix | Exposures ranked by financial impact severity |
| Risk capacity curve | Cash available vs. price scenario probability |
| Hedge cost/benefit comparison | Financial vs. non-financial alternatives |
| Optimal hedge ratio | Distress-minimizing hedge quantity |
| Backtest results | Historical effectiveness of the strategy |

### Tech Stack

```python
# Core analytics
pandas          # Data manipulation and time series
numpy           # Numerical computation
scipy           # Statistical distributions and optimization
matplotlib      # Visualization
seaborn         # Statistical plotting

# Financial modeling
yfinance        # Market price data retrieval
datetime        # Date handling for forward curves

# Notebook environment
Google Colab    # Cloud execution, no local setup required
```

---

## How to Run

### Option 1 — Google Colab (Recommended)

Click the badge at the top of this README:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cgorricho/the-right-way-to-hedge/blob/main/GDR_40.ipynb)

No installation required. The notebook installs its own dependencies.

### Option 2 — Local Jupyter

```bash
git clone https://github.com/cgorricho/the-right-way-to-hedge.git
cd the-right-way-to-hedge
pip install pandas numpy scipy matplotlib seaborn yfinance jupyter
jupyter notebook GDR_40.ipynb
```

---

## Source Article

**"The Right Way to Hedge"**
McKinsey & Company | Strategy & Corporate Finance Practice
Authors: Martin Pergler and Andrew Freeman

The article argues that the complexity of day-to-day commodity hedging often overwhelms its underlying logic — and that the solution is to begin with a broad strategic perspective rather than a tactical derivatives program. The full article is available at [mckinsey.com](https://www.mckinsey.com/capabilities/strategy-and-corporate-finance/our-insights/the-right-way-to-hedge).

---

## Related Projects

This notebook is part of a broader portfolio of financial engineering and AI projects:

| Project | Description |
|---|---|
| [portfolio](https://github.com/cgorricho/portfolio) | Full project portfolio — all 45 repositories |
| [token-light-code-intensive](https://github.com/cgorricho/token-light-code-intensive) | AI cost governance framework (TLCI) |
| [OFAC](https://github.com/cgorricho/OFAC) | Sanctions screening tool for humanitarian NGOs |
| [agentic-RAG-Oben-Pinecone](https://github.com/cgorricho/agentic-RAG-Oben-Pinecone) | Production RAG chatbot with fine-tuned embeddings |
| [bmad-sdlc](https://github.com/cgorricho/bmad-sdlc) | Automated SDLC using Claude Code |

---

## Author

**Carlos Gorricho** — CFO · AI Practitioner · Management Consultant

- Former CFO at Riopaila Castilla S.A. (Colombia's largest agribusiness conglomerate)
- Designed $300M commodity risk management program using derivatives
- Currently CFO at Aid to the Church in Need USA
- Founder & CEO, CGAI Management Consulting LLC

📧 cgorricho@carlosgorrichoai.one
🔗 [linkedin.com/in/carlos-gorricho-data-driven-c-level](https://linkedin.com/in/carlos-gorricho-data-driven-c-level)
💻 [github.com/cgorricho](https://github.com/cgorricho)

---

*April 2026 · CGAI Management Consulting LLC*
