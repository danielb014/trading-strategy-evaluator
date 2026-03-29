# Dimension Scoring Guide

Detailed thresholds and examples for scoring each of the 6 evaluation dimensions.
Score 1 (worst) → 5 (best) per dimension.

---

## Dimension 1: Performance (Weight 25%)

Measures risk-adjusted returns. Raw return alone is meaningless without context.

### Key metrics to assess
- **Annualized return** — after all costs
- **Sharpe ratio** — (Ann.Return - RiskFree) / Ann.Volatility
- **Sortino ratio** — like Sharpe but only penalizes downside volatility
- **Calmar ratio** — Ann.Return / |Max Drawdown|
- **Profit Factor** — Σ(wins) / Σ(losses)
- **Expectancy** — average return per trade (after fees)

### Score thresholds

| Score | Sharpe | Ann% | PF | Calmar | Expectancy/trade |
|-------|--------|------|----|--------|-----------------|
| 5 | > 1.5 | > 20% | > 2.0 | > 2.0 | > 0.5% |
| 4 | 0.8–1.5 | 12–20% | 1.4–2.0 | 1.0–2.0 | 0.2–0.5% |
| 3 | 0.5–0.8 | 8–12% | 1.2–1.4 | 0.5–1.0 | 0.1–0.2% |
| 2 | 0.2–0.5 | 3–8% | 1.05–1.2 | 0.2–0.5 | 0–0.1% |
| 1 | < 0.2 | < 3% | < 1.05 | < 0.2 | < 0% |

**Practical note:** Most performance data comes from backtests. Apply a 40–60% haircut
to backtested returns when projecting live performance (industry standard).

---

## Dimension 2: Backtest Integrity (Weight 25%)

The most important dimension for algo strategies. Excellent performance on a bad backtest = zero.

### What to check

**Sample size**
- OOS trades < 30: Score cap = 2 (statistically meaningless)
- OOS trades 30–50: Marginal, interpret with caution
- OOS trades 50–100: Acceptable
- OOS trades > 100: Good
- OOS trades > 200: Strong

**IS/OOS degradation**
- PF(IS) / PF(OOS) ratio reveals overfitting:
  - < 1.3× degradation: Good (model generalizes)
  - 1.3–1.8×: Acceptable
  - 1.8–2.5×: Warning — likely some overfitting
  - > 2.5×: Red flag — heavy overfitting

**Backtest period coverage**
- Covers multiple regimes (bull + bear + ranging): +1
- Only covers bull market: -1
- Tested on 5+ years: Good
- Tested on < 1 year: Score cap = 2

**Cost model realism**
- Includes fee + slippage: Good
- Includes fee only: Apply 2× haircut mentally
- No costs modeled: Score cap = 2

**Other checks**
- Walk-forward validation: +1 to score
- No lookahead bias verified: Required
- Monte Carlo simulation run: +0.5

### Score thresholds

| Score | OOS Trades | IS/OOS PF ratio | Period | Costs |
|-------|-----------|-----------------|--------|-------|
| 5 | > 200 | < 1.3× | 5+ yrs, multi-regime | Fee + slippage |
| 4 | 100–200 | 1.3–1.8× | 3–5 yrs | Fee + slippage |
| 3 | 50–100 | 1.8–2.0× | 2–3 yrs | Fee only |
| 2 | 30–50 | 2.0–2.5× | 1–2 yrs | Fee only |
| 1 | < 30 | > 2.5× | < 1 yr | No costs |

---

## Dimension 3: Edge Rationale (Weight 20%)

What is the actual reason this strategy makes money? Can you articulate it clearly?
If you can't explain the edge in one sentence, it probably doesn't have one.

### Categories of edge (from most to least durable)

**Structural / Market microstructure edge**
- Examples: Bid-ask spread capture, liquidity provision, order flow imbalance
- Durability: High — based on market mechanics
- Detection: Taker flow ratio, CVD, order book signals

**Regime-based edge**
- Examples: Trending in high-ATR regimes, mean-reversion in low-vol regimes
- Durability: Medium — requires correct regime identification
- Risk: Regime change can make strategy stop working overnight

**Statistical pattern edge**
- Examples: Seasonality, day-of-week effects, earnings drift
- Durability: Medium-low — patterns can be traded away once known
- Risk: Crowding (too many algos exploit same pattern)

**Parameter-fitted edge**
- "Optimized" parameters with no fundamental rationale
- Durability: Very low — almost certainly overfitted
- Signature: Strategy stops working 6–12 months after optimization date

### Score thresholds

| Score | Edge Description |
|-------|-----------------|
| 5 | Clear microstructure or behavioral explanation. Academically documented. Robust across multiple assets and timeframes without retuning. |
| 4 | Solid regime-based rationale. Edge exists but depends on market conditions. Clear "why it works" story. |
| 3 | Plausible logic. Pattern-based with some reasoning. Moderate confidence edge will persist. |
| 2 | Vague or thin rationale. "It worked in backtest." No clear reason it should continue. |
| 1 | No edge rationale. Pure curve-fitting. Contradicts market microstructure logic. |

---

## Dimension 4: Risk & Drawdown (Weight 15%)

Measures survivability. A strategy that blows up once is a failed strategy regardless
of prior returns. Real money cannot tolerate some drawdowns psychologically even if
mathematically recoverable.

### Key metrics

**Max drawdown:** Peak-to-trough equity decline
**Recovery time:** Days/months to recover from max DD
**Max consecutive losses:** Tests psychological durability
**Tail risk:** Worst single-trade loss as % of portfolio
**Monthly win rate:** % of months in profit

### Score thresholds

| Score | Max DD | Recovery | Consec. Losses | Monthly Win% |
|-------|--------|----------|----------------|-------------|
| 5 | < 10% | < 30 days | ≤ 3 | > 65% |
| 4 | 10–20% | 30–90 days | 4–5 | 55–65% |
| 3 | 20–30% | 3–6 months | 6–8 | 45–55% |
| 2 | 30–45% | 6–18 months | 9–12 | 35–45% |
| 1 | > 45% | > 18 months / ongoing | > 12 | < 35% |

**Psychological reality check:** Most traders abandon strategies after 3–5 consecutive losses
regardless of expected value. A strategy with 12 consecutive losses (even if profitable
long-term) will not be executed correctly by a human operator.

---

## Dimension 5: Opportunity Cost (Weight 10%)

The question is not "does this strategy make money?" but "does it make MORE money
than the alternative of doing nothing?" Time, cognitive load, and capital have value.

### Comparison framework

Always compare on **same time period** and **risk-adjusted basis**:

1. **Absolute return:** Did it beat buy-and-hold?
2. **Risk-adjusted:** Did it beat passive with less drawdown?
3. **Sharpe comparison:** Is Sharpe > index Sharpe?
4. **Effort-adjusted:** Is the alpha worth the time to manage?

### Passive benchmarks (use same backtest period)

| Benchmark | Typical Ann% | Typical Sharpe | Effort |
|-----------|-------------|----------------|--------|
| SPY (S&P 500) | ~10–11% | ~0.6 | Zero |
| QQQ (Nasdaq) | ~14–15% | ~0.7 | Zero |
| BTC hold | Variable (bull: +200%, bear: -80%) | ~0.8–1.2 bull | Zero |
| 60/40 | ~7–8% | ~0.8 | Near-zero |
| T-Bills | ~4–5% | N/A | Zero |

### Score thresholds

| Score | vs Passive |
|-------|-----------|
| 5 | Beats best passive alternative by > 5% annualized AND better Sharpe |
| 4 | Beats passive by 2–5% annualized OR significantly better risk-adjusted |
| 3 | Roughly matches passive with similar or better risk profile |
| 2 | Underperforms passive return but with lower drawdown |
| 1 | Underperforms passive on both return and risk-adjusted basis |

---

## Dimension 6: Weak Points (Weight 5%)

Every strategy has structural vulnerabilities. Identifying them honestly is what separates
a professional evaluation from a promotional pitch. Score reflects how severe the weak points are
(5 = minor/manageable, 1 = fatal flaws).

### Common weak points to check

**Regime dependency**
- Does the strategy only work in trending or only in ranging markets?
- What happens when regime changes? (e.g., spot_flow in parabolic 2021 bull)

**Crowding risk**
- Are many other algos running similar logic?
- The Turtle strategy stopped working when too many traders copied it
- Any strategy based on published academic factors is already crowded

**Capacity constraints**
- What's the maximum capital this strategy can absorb?
- A strategy that works on $10K may not work on $1M (market impact)
- 15m crypto futures at $50K starts moving against you

**Execution sensitivity**
- How much does slippage affect the strategy?
- If 10bps slippage turns profitable → unprofitable, the edge is too thin

**Strategy decay**
- How long has this worked? Is the edge shrinking over time?
- Look at year-by-year performance trend — is it improving, flat, or declining?

**Parameter fragility**
- What happens if you change the key parameters by ±10%?
- Robust strategies survive small parameter changes; overfit ones collapse

**Psychological durability**
- Can a human actually follow this strategy through its worst drawdown?
- A strategy requiring 12 consecutive losses before recovery will be abandoned

### Score thresholds

| Score | Weak Point Profile |
|-------|-------------------|
| 5 | Minor, manageable vulnerabilities. Strategy is regime-robust. Works across parameters. |
| 4 | 1–2 known weak points that can be monitored and managed with circuit breakers. |
| 3 | Clear regime dependency or thin edge after slippage. Requires active monitoring. |
| 2 | Multiple significant vulnerabilities. Requires major redesign to be robust. |
| 1 | Fatal structural flaws (overfitting, no slippage, cherry-picked period, no edge rationale). |
