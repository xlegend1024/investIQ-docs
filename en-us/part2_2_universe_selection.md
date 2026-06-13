---
title: "2.2 Universe Selection"
parent: English
nav_order: 3
---

# Part 2.2 — Universe Selection: Where the Performance Actually Lives

[Series Home (English)](../README.md) | [한국어 README](../README_kokr.md) | [이 문서 한국어](../ko-kr/part2_2_universe_selection.md)

> *Series: Building an Algorithmic Trading System as an Investing Novice, with an AI Team (Part 2.2 of 5)*
>
> **Scope and limits.** Realized and backtested figures from an Alpaca paper account, single window.
> This sub-part shows that most of the apparent edge sits in **which symbols entered the universe**,
> not in the daily sentiment ranking. Part 2.3 then tests whether that selection has real skill.

---

## Summary

- The analysis universe is the **133 symbols the system actually traded** — a small,
  sentiment-correlated subset of NASDAQ, not a random sample.
- A cost-aware backtest of "rank by sentiment → hold N days → liquidate" beats SPY in-sample, and
  looks better the longer it holds — but once decomposed, **most of that outperformance is the
  universe's own drift, not the day-to-day signal.**
- This relocates the question: the interesting effect is in the **selection stage** (which symbols
  are in the universe), which Part 2.3 examines directly.

---

## 1. The universe is a selection, not a sample

A novice trap is conflating the **analysis population** with the **trading set**. News mentions
thousands of strings; most never resolve to a tradable US ticker. We scoped the studies to the
**133 symbols the system actually traded** (two out-of-scope names excluded).

This trades breadth for relevance — the operating question is "did the approach help on the names we
acted on," not "does sentiment work across all of NASDAQ." But it carries a hidden risk: those 133
names were not drawn at random. They are the survivors of a **sentiment-correlated selection**
(news coverage → watchlist promotion → actually traded). That selection, not the signal, turns out
to carry most of the measured performance.

---

## 2. The "hold N days" strategy, tested with costs

To make the question concrete, we ran the literal strategy a reader might imagine: each formation
day, rank the universe by lagged news sentiment, buy the top tercile, hold N days, liquidate,
re-form — with round-trip transaction costs.

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
strategy. The decomposition is where it unravels.

---

## 3. Decomposition: the signal is the small part

Add an **equal-weight whole-universe** benchmark (hold all 133 names equally) and a **market-neutral
long-short** (long top tercile, short bottom). These separate the sentiment signal from the
universe's own drift and from market beta.

| Hold | Long-only | Equal-weight universe | **Selection alpha** | Long-short (signal-only) |
|---|---:|---:|---:|---:|
| 1d | +8.1% | +3.6% | +4.5% | −0.1% |
| 3d | +6.9% | +7.0% | **−0.1%** | −0.0% |
| 5d | +21.7% | +16.7% | +5.0% | +8.4% |
| 10d | +26.9% | +16.8% | +10.1% | +15.7% |

Two facts stand out:

1. **The 133-name universe itself beat SPY** — +16.8% vs +8.0% at the 10-day cadence. A large part
   of "beating the market" is simply that this small/mid-cap universe rose more than the index,
   with no sentiment selection involved.
2. **The day-to-day signal contributes little and inconsistently.** Selection alpha (long-only minus
   the equal-weight universe) is **zero at the pre-registered 3-day horizon**, and the clean
   market-neutral long-short is weak everywhere and **negative at 10 days** (−3.8% per trade).

The breakdown of the headline 10-day long-only return:

```
Long-only total  =  market (SPY)  +  universe selection  +  day-to-day signal
   +27%          ≈    +8%         +      +17% (largest)   +    ~0%
```

So the result is not mainly about ranking by sentiment each day. It is about **which symbols are in
the universe at all** — the selection stage.

---

## 4. Why this reframes everything

If most of the performance lives in selection, the right object of study is **the universe choice**,
not the daily signal. And that immediately raises a harder question: when our traded universe beats
NASDAQ, is that **skill** (we picked names that would go up) or **momentum we rode** (we picked names
that were already going up)? In-sample, on the traded names alone, the two are indistinguishable.

Answering it requires a **control group** — the symbols the pipeline saw but did **not** trade — and
a **before/after** comparison. That is exactly what Part 2.3 does.

> **Next:** Part 2.3 builds a control group of non-traded names (including a deliberately
> negative-sentiment set) and uses the 44 days **before** trading as a placebo, to separate genuine
> selection skill from pre-existing momentum.


