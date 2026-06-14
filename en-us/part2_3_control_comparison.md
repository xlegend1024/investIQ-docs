---
title: "2.3 Control-Group Comparison"
parent: English
nav_order: 4
---

# Part 2.3 — Comparing Universe Candidates with Excluded Names

[Series Home (English)](../README.md) | [한국어 README](../README_kokr.md) | [이 문서 한국어](../ko-kr/part2_3_control_comparison.md)

> *Series: Building an Algorithmic Trading System as an Investing Novice, with an AI Team (Part 2.3 of 5)*
>
> **Scope and limits.** A quasi-experiment on Alpaca paper-account data, over a single window. This
> part first decomposes a backtest to show that most of the apparent performance comes from the
> universe selection stage described in Part 2.2. It then tests whether that selection has genuine
> forward predictive power, using a control group of non-traded symbols and a placebo window, and
> draws the strategic direction that follows.

---

## Summary

- Decomposing a backtest that ranks by sentiment and holds for N days shows that most of the apparent
  performance comes not from the daily signal but from the selection stage described in Part 2.2, that
  is, which symbols are included in the universe in the first place.
- To test whether the selected candidates carry meaning, we built a control group of symbols the news
  pipeline covered but the system did not trade, including a deliberately negative-sentiment subset.
  We compared these to the traded names over both the trading window and the 44 days before trading
  began.
- The traded group outperformed the control by a wide margin during the trading window (+20pp), but
  it had already been ahead by +14pp before trading began. The trend-adjusted difference-in-differences
  estimate is not statistically significant.
- In conclusion, the selected names mostly rode pre-existing momentum rather than predicting it. Even
  so, the fact that a non-specialist, using only news sentiment and a few rules, assembled a candidate
  pool filled with the momentum names the market was actually paying attention to is hard to dismiss
  as coincidence. The result sits between meaningful and meaningless.

---

## 1. The apparent performance comes from the selection stage

Part 2.2 showed that InvestIQ selects a small universe tilted toward momentum and sentiment. So how
good does that universe look if you run the strategy a reader might imagine? We simulated it with
transaction costs: each formation day, rank the universe by lagged news sentiment, buy the top
tercile, hold N days, liquidate, re-form.

| Hold | Long-only | SPY | Per-trade NW t | Hit rate |
|---|---:|---:|---:|---:|
| 1d | +8.1% | +4.2% | 0.98 | 65% |
| 3d | +6.9% | +4.5% | 1.88 | 68% |
| 5d | +21.7% | +8.0% | 1.84 | 77% |
| 10d | +26.9% | +8.0% | **2.61** | 82% |

![Equity by horizon](./images/F1_equity_by_horizon.png)
*Figure. Realizable equity (form → hold N days → liquidate) at 10 bps cost. Long-only (green) sits
above SPY (grey dashed) at every horizon — but note the orange line.*

Taken alone, the 10-day result — +27% vs SPY +8%, a per-trade t of 2.61 — looks like a working
strategy. The decomposition is where it unravels. Add an **equal-weight whole-universe** benchmark
(hold all 133 names equally) and a **market-neutral long-short** (long top tercile, short bottom) to
separate the sentiment signal from the universe's drift and market beta.

| Hold | Long-only | Equal-weight universe | **Selection alpha** | Long-short (signal-only) |
|---|---:|---:|---:|---:|
| 1d | +8.1% | +3.6% | +4.5% | −0.1% |
| 3d | +6.9% | +7.0% | **−0.1%** | −0.0% |
| 5d | +21.7% | +16.7% | +5.0% | +8.4% |
| 10d | +26.9% | +16.8% | +10.1% | +15.7% |

Two facts stand out: (1) **the 133-name universe itself beat SPY** (+16.8% vs +8.0% at 10 days) —
simply because this small/mid-cap universe rose more than the index, with no sentiment selection. (2)
**The day-to-day signal contributes little and inconsistently** — selection alpha is zero at the
pre-registered 3-day horizon, and the clean long-short is negative at 10 days (−3.8% per trade).

```
Long-only total  =  market (SPY)  +  universe selection  +  day-to-day signal
   +27%          ≈    +8%         +      +17% (largest)   +    ~0%
```

So most of the apparent edge is not in ranking by sentiment each day but in **which symbols are in
the universe at all** — the selection stage Part 2.2 described. Is that selection **skill** (picked
names that would rise) or **momentum it rode** (names already rising)? In-sample, on the traded names
alone, the two are indistinguishable — the rest of this part answers with a control group.

---

## 2. Design: treated and control groups, before and after

To ask whether selecting these names showed skill, we need to know how they would have looked
*without* the selection. So we set up a quasi-experiment:

- **Treated:** the 132 traded names.
- **Control:** non-traded but news-covered names — 2,847 broad, plus a 1,423-name
  **negative-sentiment** subset (the sharp contrast: names with clearly negative news that we did not
  trade).
- **PRE window:** the 44 trading days **before** trading began (a placebo — before the system acted).
- **POST window:** the 44-day trading window itself.

All prices come from Alpaca Market Data (no external vendor); sentiment from InvestIQ news-intel. The
design was fixed before results were inspected.

---

## 3. The naive comparison appears to favor the traded group

In the trading window, the traded names substantially outperformed the control:

| Group | n | POST return |
|---|---:|---:|
| Treated (traded) | 132 | **+24.8%** |
| Control — all non-traded | 2,847 | +4.5% |
| Control — negative sentiment | 1,423 | −3.3% |
| SPY | — | +8.1% |

A +20pp lead over all non-traded names (t = 4.4, p = 2×10⁻⁵) looks like enormous selection skill.
But the placebo window destroys that reading. **Before** any of these names were traded, the treated
group was *already* far ahead:

| Group | PRE return |
|---|---:|
| Treated (traded) | **+10.7%** |
| Control — all non-traded | −0.7% |
| Control — negative sentiment | −8.4% |
| SPY | −1.3% |

![Pre vs post by group](./images/F1_pre_post_by_group.png)
*Figure. Mean buy-and-hold return before (light) and during (solid) trading. The treated group's
lead is already large in the PRE period — the signature of selection on pre-existing momentum.*

The treated names were not comparable to the controls before selection. They were **already the
winners.**

---

## 4. Difference-in-differences shows no significant forward predictive power

The honest estimate nets out each group's fixed level and the pre-existing trend:
`DiD = (POST gap) − (PRE gap)`.

| Comparison | PRE gap | POST gap | **DiD** | Bootstrap 95% CI | p |
|---|---:|---:|---:|---:|---:|
| Treated − all non-traded | +14.0pp | +20.3pp | **+6.3pp** | [−3.3, +17.2] | 0.23 |
| Treated − negative sent. | +19.1pp | +28.1pp | **+9.0pp** | [−0.8, +19.9] | 0.094 |

![Difference-in-differences](./images/F2_difference_in_differences.png)
*Figure. The treated−control gap was already +14pp (vs all) / +19pp (vs negative) before trading; it
widened to +20pp / +28pp during. The increment (DiD) is small and not significant.*

**Both intervals include zero.** Of the +20.3pp post-period lead, **+14.0pp (≈69%) already existed
before trading.** Once the pre-existing trend is removed, the forward skill of the selection is
**statistically indistinguishable from zero.** The selection captured names that were already rising;
it did not demonstrably forecast which would rise.

A dose-response check (forward return vs in-window sentiment) shows a strong positive slope, but the
sentiment there is measured over the same window as the return — contemporaneous co-movement, not
prediction. It is consistent with the DiD verdict and cannot upgrade it.

---

## 5. What the selection means: not prediction, but not coincidence

What the statistics above knock down is exactly one thing: **prediction**. Most of the treated
group's post-period lead (~69%) already existed before any trade, and the trend-removed
difference-in-differences cannot reject zero. The claim "we knew in advance which names would rise"
is not supported by this data. Four caveats narrow it further:

1. **The slice beats the index by construction.** Selecting active, high-sentiment, high-momentum
   small/mid-caps means that in an up-tape they rise more than SPY. The +24.8% vs +8.1% is largely
   factor exposure, not skill.
2. **Most of the lead is pre-existing momentum.** ≈69% of the advantage over non-traded names existed
   before any trade — a universe-level look-ahead.
3. **The clean causal estimate is not significant.** Difference-in-differences cannot reject zero.
4. **It does not generalize to NASDAQ.** The control is still *news-covered* names, not a random
   draw; external validity is limited to "names the pipeline could see."

But the same data shows **something else clearly**. What the test rejects is *prediction*, not
*capture*. In the PRE window — before any trade — the treated group was already at +10.7%, while the
all-non-traded control sat at −0.7% and the explicitly negative-sentiment set at −8.4%. The pipeline
leaned *systematically* toward names that already had market attention and live momentum, and
*systematically* away from negative ones.

Here is the core point of this part. **"Not statistically significant" is not the same as
"meaningless."** That a non-specialist, using only news sentiment and a few rules, built a candidate
pool that filled a previously empty watchlist with **names the market actually cared about — names
with live momentum** — is hard to write off as coincidence. The selection did not *predict* which
names would rise, but something repeatable was at work in *capturing* market interest and momentum.
So the result can be called neither "significant" nor "meaningless" — it sits between the two.

---

## 6. Strategic direction

The finding is not a dead end — it is a redirection. It tells us where a real edge would have to come
from and how to test it honestly:

1. **Study selection, not the daily signal.** The performance lives in the universe choice, so that
   is the object worth improving and validating.
2. **Define the universe point-in-time.** Select names by a rule fixed *before* each window opens, so
   the test cannot ride moves that already happened. This removes the universe-level look-ahead that
   inflated the current result.
3. **Always carry a control group.** Keep the non-traded, news-covered names (and a
   negative-sentiment set) as a permanent benchmark, so every future claim is a treated-vs-control,
   before-vs-after comparison rather than an in-sample story.
4. **Replicate out-of-sample.** A single 44-day regime cannot confirm anything; the same pipeline
   must be re-run across other windows and tapes before any selection rule is trusted.
5. **Separate momentum from skill explicitly.** Since the current "edge" is mostly momentum, a useful
   next experiment is whether the selection adds anything *beyond* a simple momentum screen — if it
   does not, the news machinery is not earning its complexity.

The honest version of the project's conclusion is therefore methodological rather than financial:
the novice's news-based selection clearly had *something* when it came to **capturing** market
interest and momentum, but the measurement that asks whether that is **predictive skill** — a control
group plus a placebo window plus difference-in-differences — cannot yet answer "yes." What we learned
is how to separate those two and test them honestly, and that is a more durable result than a
single-window equity curve.


