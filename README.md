---
title: README (English)
nav_exclude: true
search_exclude: true
---

# InvestIQ Medium Series — An Investing Non-Specialist Builds an Algorithmic Trading System with AI

[English (default)](./README.md) | [한국어](./README_kokr.md)

> **Series title:** *Building an Algorithmic Trading System as an Investing Novice, with an AI Team*
>
> A 5-part technical blog series. Target readers: **data analysts** and **business decision-makers**.
> The throughline: a non-specialist builds an end-to-end algorithmic trading system with the help of
> LLM-based AI agents, runs it on a minimal budget in a paper account, and **analyzes the result
> honestly** — including what to watch for when working with AI.
>
> **Important distinction:** Trading decisions are made by **code-defined algorithms** (technical
> analysis + portfolio optimization + risk rules). The AI agents were the **development, research,
> and review harness** for that program — not the entity that decides trades in real time.

---

## Series structure

| # | Title | One-line summary | Key visuals |
|---|---|---|---|
| **1** | [Background — Why, Who, With What](./en-us/part1_background_and_setup.md) | Non-specialist + AI team (Squad) + 14-microservice paper-trading MVP | Architecture / safety-floor flowcharts |
| **2.1** | [Data — Ingestion Pipeline & Source of Truth](./en-us/part2_1_data_pipeline.md) | Multi-source ingestion · single Alpaca price source · the broker's filled-order record | Coverage and sentiment-distribution charts |
| **2.2** | [Universe Selection — How InvestIQ Picks What to Trade](./en-us/part2_2_universe_selection.md) | watchlist-intel authority · capped discovery → promotion → auto-approve → rotation · regime gate | Selection-pipeline flowchart |
| **2.3** | [Control-Group Comparison & Strategic Direction](./en-us/part2_3_control_comparison.md) | Backtest decomposition · treated vs control · placebo (pre-trading) window · difference-in-differences · selection rode momentum, not skill | Equity-by-horizon, pre/post by group, DiD |
| **3.1** | [Strategy — Scoring Symbols (Spec-070)](./en-us/part3_1_scoring.md) | The composite score: momentum/technical + news sentiment × pullback multiplier | Composite-score flowchart |
| **3.2** | [Post-Market Pipeline & Portfolio Optimization](./en-us/part3_2_postmarket_pipeline.md) | Nightly post-market batch · Markowitz / Risk Parity · quality gate · concentration cap | Pipeline + optimization flowcharts |
| **3.3** | [A Real Allocation, Read Line by Line](./en-us/part3_3_real_allocation_example.md) | The actual 2026-06-12 rebalancing plan · 31 held names · whole-share trades · 3 risk-gate blocks | Real target-weight bar, 14-day weight heatmap |
| **3.4** | [From Plan to Order — Approval-Gated Execution](./en-us/part3_4_approval_gated_execution.md) | Propose → review → execute · HMAC token · fail-closed veto | Approval-gated sequence diagram |
| **4** | [What the Loss Actually Was — A Causal Reading](./en-us/part4_loss_attribution.md) | Realized −$369.85 over 927 round-trips · single-name tail (ASTH) · indistinguishable from break-even · news signal underpowered | H1–H6 attribution charts, IC term structure |
| **5** | [Lessons — Working with AI](./en-us/part5_lessons_for_working_with_ai.md) | Pre-registration · authoritative records · universe separation · hard caps · veto structure | AI-collaboration loop flowchart |

---

## Key facts (single source of truth)

- **Window:** 2026-04-13 to 2026-06-13 (42 trading days), Alpaca paper account.
- **Loss attribution (`loss_attribution_v2`):** realized −$369.85 across 927 long round-trips in 133
  names; win rate 41.7%, payoff 1.31; ASTH −$2,712 (ex-ASTH +$2,343); bootstrap 95% CI
  [−$3,156, +$2,149] — indistinguishable from break-even.
- **News causality (`news_causality_v3`):** IC positive and rising with horizon (1d +0.028 → 10d
  +0.061) but not significant; a directionally consistent, underpowered signal. Prices from Alpaca
  Market Data; sentiment from InvestIQ news-intel.

## Publishing guide

- **Figures:** PNGs live in `research/loss_attribution_v2/figures/` (H1–H6) and
  `research/news_causality_v3/figures/` (01/02/03 series). Attach directly when uploading to Medium.
- **Mermaid:** Medium does not render mermaid natively; export each diagram to PNG/SVG at
  [mermaid.live](https://mermaid.live) and embed it.
- **Scope banner:** Every figure is realized PnL from a paper account over a single window. Keep the
  scope-and-limits note at the top of each part.
- **Tags:** `#AlgorithmicTrading #LLM #QuantResearch #AIAgents #DataScience`.


