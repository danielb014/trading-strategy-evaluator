# Legendary Investor Benchmarks

Reference these when benchmarking a strategy or discussing edge durability.
Use these as the gold standard — strategies should be compared to what the best have achieved.

---

## Table of Contents
1. [Quantitative / Systematic](#quantitative--systematic)
2. [Macro / Discretionary](#macro--discretionary)
3. [Long-Term Value](#long-term--value)
4. [Technical / Trend](#technical--trend)
5. [Key Takeaways for Strategy Evaluation](#key-takeaways-for-strategy-evaluation)

---

## Quantitative / Systematic

### Jim Simons — Renaissance Technologies (Medallion Fund)
- **Period:** 1988–2018
- **Ann. return (gross):** ~66% | **Net of fees:** ~39%
- **Sharpe ratio:** ~2.0+ (exceptionally rare)
- **Max drawdown:** ~15% (managed tightly)
- **Win rate:** ~50–55% (very high frequency, tiny edge per trade, massive compounding)
- **Edge source:** Statistical arbitrage, pattern recognition across thousands of instruments
- **Key lesson:** The edge was in *execution* and *signal diversification* — no single signal dominated. Thousands of weak signals combined beat one strong signal.
- **Strategy evaluation use:** If someone claims Sharpe > 1.5 on a simple 2-signal strategy, that is extraordinary and requires extraordinary evidence.

### Two Sigma / D.E. Shaw (industry benchmark)
- **Ann. return (net):** ~15–20%
- **Sharpe:** ~1.0–1.5
- **What they do:** High-frequency to medium-frequency stat arb, ML-driven signals
- **Key lesson:** Even the best quant shops with unlimited resources target 15–20% net. A retail strategy claiming 30%+ annualized net should be viewed skeptically unless sample is very large.

### AQR Capital (Cliff Asness)
- **Strategy:** Factor investing (value, momentum, carry, defensive)
- **Ann. return:** ~10–15% net
- **Sharpe:** ~0.7–1.0
- **Key lesson:** Well-documented, academically validated factors still only generate moderate Sharpe. True edge is rare.

---

## Macro / Discretionary

### George Soros — Quantum Fund
- **Period:** 1969–2000
- **Ann. return:** ~32% net
- **Famous trade:** Short GBP 1992 — $1B profit in one day
- **Max drawdown:** ~26% (1981)
- **Edge source:** Global macro — reflexivity theory, identifying self-reinforcing feedback loops in markets
- **Key lesson:** Exceptional returns came from *concentrated bets* with asymmetric payoffs, not diversified systematic trading. Very few people can replicate this.

### Stanley Druckenmiller
- **Period:** 1986–2010
- **Ann. return:** ~30%
- **Consecutive profitable years:** 30 (no losing year in 30 years)
- **Edge source:** Macro, concentrated positions, "when you're right, be very right"
- **Key lesson for evaluation:** A strategy with no losing *years* over 10+ years is extraordinarily rare — virtually no strategy achieves this. Be very suspicious of backtests with no losing years.

### Ray Dalio — Bridgewater (Pure Alpha)
- **Ann. return:** ~12–15% net
- **Sharpe:** ~0.8–1.0
- **Strategy:** Risk parity — diversify across uncorrelated risk premiums
- **Key lesson:** The world's largest hedge fund targets modest Sharpe. True diversification is hard.

---

## Long-Term / Value

### Warren Buffett — Berkshire Hathaway
- **Period:** 1965–2023
- **Ann. return:** ~19.8% (vs S&P 11.4%)
- **Total gain:** ~3,787,464% vs S&P 31,223%
- **Sharpe:** ~0.7–0.8 (not exceptional risk-adjusted, but extraordinary compounding)
- **Max drawdown:** ~-51% (2008–2009) — endured deep DDs by holding long
- **Edge source:** Buying great businesses at fair prices, holding forever, compound interest
- **Key lesson for evaluation:**
  - Buffett's edge is *patience* and *business quality judgment*, not market timing
  - His 20% ann. return over 60 years is the best long-term track record in history
  - Any active strategy must justify itself vs simply buying BRK.B or SPY
  - He famously stated: "Most investors would be better off in index funds"

### Peter Lynch — Magellan Fund
- **Period:** 1977–1990 (13 years)
- **Ann. return:** ~29.2%
- **Beat S&P every year of his tenure**
- **Edge source:** "Invest in what you know" — retail consumer observation, growth at reasonable price
- **Key lesson:** Even Lynch, the best mutual fund manager in history, retired at 46 saying the stress wasn't worth it. Consistent outperformance is exhausting and rare.

### Joel Greenblatt — Gotham Capital
- **Period:** 1985–1994
- **Ann. return:** ~50%
- **Strategy:** Special situations, spin-offs, value in complexity
- **Key lesson:** High returns in early years are common for small funds — capacity constraints are real. A $50K strategy and a $50M strategy perform very differently.

---

## Technical / Trend Following

### Richard Dennis — Turtle Traders
- **Ann. return:** ~80% (peak years, early 1980s)
- **Strategy:** Trend following — buy 20-day breakouts, hold with trailing stops
- **Win rate:** ~35–40% (most trades were losers; winners were very large)
- **Key lesson:** The spot_flow breakout strategy in this codebase is essentially a version of the Turtle system. Dennis proved breakout works — but win rates of 30–40% are *normal and expected* for trend following. Don't over-optimize for higher win rates.
- **Caveat:** Dennis's strategy later failed due to *strategy crowding* — too many traders following the same breakout signals. This is a real risk for any published or widely-known strategy.

### Ed Seykota
- **Ann. return:** ~60%+ (1970s–1980s)
- **Strategy:** Trend following, position sizing, cutting losses ruthlessly
- **Famous quote:** "Cut losses, ride winners, manage risk, stick to your system"
- **Key lesson:** Seykota's returns came from *regime* — the 1970s–80s commodity trends were exceptional. The same strategy underperformed in ranging markets. **Regime dependency is the #1 silent killer of trend strategies.**

### Paul Tudor Jones
- **Ann. return:** ~25%+
- **Strategy:** Macro trend following, never averaged down losers
- **Key lesson:** "Losers average losers." A strategy that adds to losing positions (martingale) will eventually blow up. Every evaluation should check if position sizing compounds losses.

---

## Key Takeaways for Strategy Evaluation

### What "outperforming" actually means

| Category | Achievable by | Realistic expectation |
|----------|--------------|----------------------|
| Exceptional (Simons-level) | Institutions with massive R&D | Sharpe > 1.5, Ann > 30% net |
| Great (Lynch/Druckenmiller) | Rare individuals + ideal conditions | Sharpe 0.8–1.2, Ann 20–30% |
| Good (professional quant) | Systematic + disciplined | Sharpe 0.6–1.0, Ann 12–20% |
| Viable (retail algo) | Well-designed retail strategy | Sharpe 0.4–0.7, Ann 8–15% |
| Marginal | Most retail strategies | Sharpe 0.2–0.4, Ann 5–10% |
| Not worth it | Worse than S&P passive | Sharpe < 0.2, Ann < 7% |

### The S&P 500 reality check
- S&P 500 total return (1993–2023): ~10.5% annualized
- Any strategy must beat this *risk-adjusted* to justify the complexity and time
- Warren Buffett himself recommends index funds to most investors
- A strategy with 12% annualized and -40% max DD is **worse** than S&P (10.5% with -50% max DD, but zero work)

### The Sharpe threshold that matters
- Simons: ~2.0 — never reproduced by anyone at scale
- Institutional minimum to raise capital: ~0.8
- "Worth trading over index funds": ~0.5+
- "Might as well buy SPY": < 0.3

### Why most backtests look better than live trading
- **Optimism bias:** Tested on best period
- **Lookahead bias:** Using future data accidentally
- **Overfitting:** Parameters fitted to noise
- **No slippage:** 0.1–0.2% per trade missing
- **Survivorship bias:** Only winning assets tested
- **Regime mismatch:** 2020–2021 bull is not representative

**Industry rule of thumb:** Live trading typically achieves 40–60% of backtested returns.
Apply this haircut when projecting forward from any backtest.
