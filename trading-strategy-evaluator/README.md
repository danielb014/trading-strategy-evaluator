# trading-strategy-evaluator

A Claude Code skill that evaluates any algorithmic trading strategy using a structured 6-dimension scoring framework. Produces a scored report with a weighted final verdict and a clear trade / do-not-trade recommendation.

## What it does

Given a trading strategy's backtest data, this skill:

1. Scores the strategy across 6 dimensions (1 = worst, 5 = best)
2. Applies weighted scores to compute a final number out of 5
3. Writes a full markdown evaluation report
4. Saves the report to `docs/strategy_evaluations/`

### The 6 dimensions

| # | Dimension | Weight | What it measures |
|---|-----------|--------|-----------------|
| 1 | Performance | 25% | Sharpe, annualized return, profit factor, Calmar |
| 2 | Backtest Integrity | 25% | OOS trade count, IS/OOS degradation, period length, cost model |
| 3 | Edge Rationale | 20% | Why the strategy makes money — durability of the edge |
| 4 | Risk & Drawdown | 15% | Max DD, recovery time, consecutive losses, monthly win rate |
| 5 | Opportunity Cost | 10% | Return vs passive alternatives (SPY, BTC hold, T-bills) |
| 6 | Weak Points | 5% | Structural vulnerabilities (5 = minor, 1 = fatal flaws) |

### Score interpretation

| Score | Verdict |
|-------|---------|
| 4.0 – 5.0 | Strong — trade with appropriate sizing |
| 3.0 – 3.9 | Promising — forward test before live capital |
| 2.0 – 2.9 | Marginal — significant issues, do not allocate |
| 1.0 – 1.9 | Do Not Trade — fundamental flaws |

## Installation

```bash
git clone https://github.com/danielborda/trading-strategy-evaluator.git \
  ~/.claude/skills/trading-strategy-evaluator
```

Restart Claude Code. The skill is auto-discovered from `~/.claude/skills/`.

## Usage

```
/trading-strategy-evaluator
```

Or just ask: *"evaluate the mean_reversion strategy"* — Claude will invoke it automatically.

## Included references

- `references/scoring_guide.md` — Detailed thresholds for all 6 dimensions
- `references/legends.md` — Legendary investor benchmarks (Simons, Soros, Buffett, Druckenmiller) for calibrating what "good" actually looks like

## Example output

See the sample evaluations this skill produced:
- Mean Reversion crypto strategy: **1.85/5 — Do Not Trade**
- FX EURUSD bb_rsi_reversion: **2.45/5 — Do Not Allocate Capital**

## Requirements

- Claude Code (any version)
- A trading strategy with backtest data (the skill adapts to whatever data is available)

## License

MIT
