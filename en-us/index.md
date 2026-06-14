---
title: English
nav_order: 2
has_children: true
permalink: /en-us/
---

# English Series

<div class="iq-hero" markdown="0">
  <img class="iq-logo" src="images/investIQ_logo.png" alt="InvestIQ" />
  <span class="iq-eyebrow">English · 5 parts</span>
  <h1 class="iq-title">Building a Trading System with an AI Team</h1>
  <p class="iq-sub">A non-specialist's end-to-end algorithmic trading system, built with an LLM-based AI team and analyzed <strong>honestly</strong>. Use the sidebar to navigate, or pick a part below.</p>
  <div class="iq-cta">
    <a class="iq-btn iq-btn-ghost" href="../ko-kr/">한국어로 보기 →</a>
  </div>
</div>

| # | Title | One-line summary |
|---|---|---|
| 1 | [Background — Why, Who, With What](part1_background_and_setup.md) | Non-specialist + AI team + 14-microservice paper MVP |
| 2.1 | [Data — Ingestion Pipeline & Source of Truth](part2_1_data_pipeline.md) | Multi-source ingestion · single Alpaca price source |
| 2.2 | [Universe Selection — How InvestIQ Picks What to Trade](part2_2_universe_selection.md) | watchlist-intel: capped discovery → promotion → rotation pipeline |
| 2.3 | [Control-Group Comparison](part2_3_control_comparison.md) | Backtest decomposition · treated vs control · placebo window · DiD |
| 3.1 | [Strategy — Scoring Symbols (Spec-070)](part3_1_scoring.md) | Composite score: momentum/technical + news sentiment |
| 3.2 | [Post-Market Pipeline & Portfolio Optimization](part3_2_postmarket_pipeline.md) | Markowitz / Risk Parity · quality gate · concentration cap |
| 3.3 | [A Real Allocation, Read Line by Line](part3_3_real_allocation_example.md) | The actual 2026-06-12 rebalancing plan |
| 3.4 | [From Plan to Order — Automated Execution](part3_4_approval_gated_execution.md) | Auto-propose → auto-execute · risk-engine HMAC · fail-closed veto |
| 4 | [What the Loss Actually Was](part4_loss_attribution.md) | Realized −$369.85 · single-name tail (ASTH) |
| 5 | [Lessons — Working with AI](part5_lessons_for_working_with_ai.md) | Pre-registration · authoritative records · hard caps |
