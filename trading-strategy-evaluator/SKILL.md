---
name: trading-strategy-evaluator
description: Evaluates any algorithmic trading strategy using a 6-dimension scoring framework (performance, backtest integrity, edge rationale, risk, opportunity cost, weak points). Produces a weighted score out of 5 and a clear trade/do-not-trade verdict. Use when asked to evaluate, score, or review a backtest, live strategy, or before promoting a strategy to live capital.
---

# Strategy Evaluator

## Overview

Evaluate any algorithmic trading strategy using a standardized 6-dimension scoring framework. Produces a complete written report with per-dimension scores, a weighted final score (1–5), and a clear verdict.

## When to Use

- User says "evaluate this strategy", "score this backtest", "run the strategy evaluator", or "/trading-strategy-evaluator"
- A backtest has just been completed and needs a rigorous assessment
- Comparing two strategies to decide which to run live
- Before promoting a strategy from paper trading to live capital

## Workflow

### Step 1 — Load references

Before writing anything, read both reference files into context:

```
references/scoring_guide.md   — thresholds and criteria for all 6 dimensions
references/legends.md         — legendary investor benchmarks for calibration
```

### Step 2 — Gather strategy data

Collect the following. Run scripts if available; read docs if not.

**Required inputs:**
- Strategy name and logic (entry/exit rules, indicators, timeframe)
- Backtest period and data source
- Performance metrics: annual return, Sharpe, profit factor, max drawdown, win rate, trade count
- Cost model: fee assumptions, slippage modeling
- IS/OOS split details (if any)
- Year-by-year or regime breakdown (if available)

**How to get them:**
- Run any backtest scripts available in the project
- Read backtest result files, docs, or output CSVs
- Ask the user to paste the metrics if no automated source exists

### Step 3 — Score all 6 dimensions

Use `references/scoring_guide.md` for exact thresholds. Score 1 (worst) → 5 (best).

| # | Dimension | Weight | What it measures |
|---|-----------|--------|-----------------|
| 1 | Performance | 25% | Risk-adjusted returns: Sharpe, Ann%, PF, Calmar |
| 2 | Backtest Integrity | 25% | OOS trades, IS/OOS degradation, period, cost model |
| 3 | Edge Rationale | 20% | Why the strategy makes money — durability of the edge |
| 4 | Risk & Drawdown | 15% | Max DD, recovery time, consecutive losses, monthly win% |
| 5 | Opportunity Cost | 10% | Return vs passive alternatives (SPY, BTC hold, T-bills) |
| 6 | Weak Points | 5% | Structural vulnerabilities (score 5=minor, 1=fatal flaws) |

### Step 4 — Write the report

Structure the report exactly as follows:

```
# <Strategy Name> — Full Evaluation Report
**Date:** | **Data:** | **Symbols/Pairs:**

## 0. What the Strategy Does
[2–4 sentences: entry logic, exit logic, timeframe, cost assumptions]

## 1. Performance — Score: X/5 (weight 25%)
[Table of key metrics by symbol/scenario. Written analysis.]

## 2. Backtest Integrity — Score: X/5 (weight 25%)
[Table of integrity factors. Flag any disqualifying issues in bold.]

## 3. Edge Rationale — Score: X/5 (weight 20%)
[Explain the "why it works" story. Compare to scoring guide categories.]

## 4. Risk & Drawdown — Score: X/5 (weight 15%)
[Table: Max DD, recovery, consecutive losses, monthly win%. Written analysis.]

## 5. Opportunity Cost — Score: X/5 (weight 10%)
[Compare to SPY, T-bills, BTC hold, or relevant passive benchmark.]

## 6. Weak Points — Score: X/5 (weight 5%)
[Table of vulnerabilities with severity. 5=minor, 1=fatal.]

## Final Score Table
| Dimension | Weight | Score | Weighted |
|-----------|--------|-------|----------|
...
| TOTAL     | 100%   |       | X.XX / 5 |

## Verdict: <Trade / Do Not Trade / Forward Test First> — X.XX/5
[The single disqualifying flaw (if any)]
[What's genuinely good]
[What needs to change before any capital commitment]
```

### Step 5 — Save the report

Save the report as a markdown file. Suggested path: `<STRATEGY_NAME>_EVALUATION_<YYYY-MM-DD>.md`. Place it wherever the project keeps its documentation.

## Scoring Calibration (quick reference)

Use `references/legends.md` to calibrate. Key anchors:
- Sharpe 5.91 from a simple BB+RSI on 2 years = **almost certainly inflated** (bar-level computation)
- Medallion Fund: Sharpe ~2.0 over 30 years — any single strategy claiming > 2.0 needs scrutiny
- Two Sigma / D.E. Shaw: 15–20% net annually — the institutional bar
- "Worth trading over index funds": Sharpe > 0.5, Ann > 7% after all costs

## Critical Checks (always apply)

1. **Cost sensitivity test** — What happens at 2× and 5× the modeled fee? If the strategy dies, flag it.
2. **Year-by-year consistency** — One outlier year masking 4 losing years is a red flag, not success.
3. **Regime coverage** — 2 years on one regime is not robust. Minimum 3 years including a bear market.
4. **Trade count on OOS data** — < 30 OOS trades = statistically unreliable, regardless of PF.
5. **Venue/cost mismatch** — Check if backtest data source matches the live execution venue (e.g., ECN data vs CFD execution).

## Resources

- `references/scoring_guide.md` — Detailed score thresholds for all 6 dimensions
- `references/legends.md` — Legendary investor benchmarks (Simons, Soros, Buffett, etc.)
