---
title: Home
nav_order: 1
description: "InvestIQ — Building an Algorithmic Trading System as an Investing Novice, with an AI Team."
permalink: /
---

<div class="iq-hero" markdown="0">
  <span class="iq-eyebrow">5-part technical series · English / 한국어</span>
  <h1 class="iq-title">Building an Algorithmic Trading System as an Investing Novice — with an AI Team</h1>
  <p class="iq-sub">An end-to-end trading system built by a non-specialist with the help of an LLM-based AI team. Run on a minimal budget in a paper account, then analyzed <strong>honestly</strong> — including the losses and what they actually were.</p>
  <div class="iq-cta">
    <a class="iq-btn iq-btn-primary" href="en-us/">Read in English →</a>
    <a class="iq-btn iq-btn-ghost" href="ko-kr/">한국어로 읽기 →</a>
  </div>
  <div class="iq-stats">
    <div class="iq-chip"><span class="iq-chip-value">−$369.85</span><span class="iq-chip-label">Realized PnL</span></div>
    <div class="iq-chip"><span class="iq-chip-value">927</span><span class="iq-chip-label">Round-trips</span></div>
    <div class="iq-chip"><span class="iq-chip-value">133</span><span class="iq-chip-label">Names traded</span></div>
    <div class="iq-chip"><span class="iq-chip-value">42</span><span class="iq-chip-label">Trading days</span></div>
    <div class="iq-chip"><span class="iq-chip-value">14</span><span class="iq-chip-label">Microservices</span></div>
  </div>
</div>

{: .scope }
> **Important distinction.** Trading decisions are made by **code-defined algorithms**
> (technical analysis + portfolio optimization + risk rules). The AI agents were the
> **development, research, and review harness** for that program — not the entity that
> decides trades in real time.

<p class="iq-section-label">Read the series</p>

<div class="iq-cards" markdown="0">
  <a class="iq-card" href="en-us/part1_background_and_setup.html">
    <span class="iq-card-num">Part 1</span>
    <span class="iq-card-title">Background — Why, Who, With What</span>
    <span class="iq-card-desc">Non-specialist + AI team + a 14-microservice paper-trading MVP.</span>
    <span class="iq-card-alt">한국어 · 배경 →</span>
  </a>
  <a class="iq-card" href="en-us/part2_1_data_pipeline.html">
    <span class="iq-card-num">Part 2.1</span>
    <span class="iq-card-title">Data — Ingestion & Source of Truth</span>
    <span class="iq-card-desc">Multi-source ingestion · single Alpaca price source · broker fills.</span>
    <span class="iq-card-alt">한국어 · 데이터 파이프라인 →</span>
  </a>
  <a class="iq-card" href="en-us/part2_2_universe_selection.html">
    <span class="iq-card-num">Part 2.2</span>
    <span class="iq-card-title">Universe Selection</span>
    <span class="iq-card-desc">watchlist-intel: a capped discovery → promotion → rotation pipeline.</span>
    <span class="iq-card-alt">한국어 · 유니버스 선택 →</span>
  </a>
  <a class="iq-card" href="en-us/part2_3_control_comparison.html">
    <span class="iq-card-num">Part 2.3</span>
    <span class="iq-card-title">Control-Group Comparison</span>
    <span class="iq-card-desc">Treated vs control · placebo window · difference-in-differences.</span>
    <span class="iq-card-alt">한국어 · 대조군 비교 →</span>
  </a>
  <a class="iq-card" href="en-us/part3_1_scoring.html">
    <span class="iq-card-num">Part 3.1</span>
    <span class="iq-card-title">Scoring Symbols (Spec-070)</span>
    <span class="iq-card-desc">Composite score: momentum/technical + news sentiment.</span>
    <span class="iq-card-alt">한국어 · 종목 점수 →</span>
  </a>
  <a class="iq-card" href="en-us/part3_2_postmarket_pipeline.html">
    <span class="iq-card-num">Part 3.2</span>
    <span class="iq-card-title">Post-Market Pipeline</span>
    <span class="iq-card-desc">Markowitz / Risk Parity · quality gate · concentration cap.</span>
    <span class="iq-card-alt">한국어 · Post-Market 파이프라인 →</span>
  </a>
  <a class="iq-card" href="en-us/part3_3_real_allocation_example.html">
    <span class="iq-card-num">Part 3.3</span>
    <span class="iq-card-title">A Real Allocation</span>
    <span class="iq-card-desc">The actual 2026-06-12 rebalancing plan, read line by line.</span>
    <span class="iq-card-alt">한국어 · 실제 할당 →</span>
  </a>
  <a class="iq-card" href="en-us/part3_4_approval_gated_execution.html">
    <span class="iq-card-num">Part 3.4</span>
    <span class="iq-card-title">Automated Execution</span>
    <span class="iq-card-desc">Auto-propose → auto-execute · HMAC token · fail-closed veto.</span>
    <span class="iq-card-alt">한국어 · 자동 실행과 코드 거부권 →</span>
  </a>
  <a class="iq-card" href="en-us/part4_loss_attribution.html">
    <span class="iq-card-num">Part 4</span>
    <span class="iq-card-title">What the Loss Actually Was</span>
    <span class="iq-card-desc">Single-name tail (ASTH) · indistinguishable from break-even.</span>
    <span class="iq-card-alt">한국어 · 손실의 실체 →</span>
  </a>
  <a class="iq-card" href="en-us/part5_lessons_for_working_with_ai.html">
    <span class="iq-card-num">Part 5</span>
    <span class="iq-card-title">Lessons — Working with AI</span>
    <span class="iq-card-desc">Pre-registration · authoritative records · hard caps · veto.</span>
    <span class="iq-card-alt">한국어 · 교훈 →</span>
  </a>
</div>

<p class="iq-section-label">Key facts (single source of truth)</p>

- **Window:** 2026-04-13 to 2026-06-13 (42 trading days), Alpaca paper account.
- **Loss attribution:** realized −$369.85 across 927 long round-trips in 133 names;
  win rate 41.7%, payoff 1.31; ASTH −$2,712 (ex-ASTH +$2,343); bootstrap 95% CI
  [−$3,156, +$2,149] — indistinguishable from break-even.
- **News causality:** IC positive and rising with horizon (1d +0.028 → 10d +0.061)
  but not significant; a directionally consistent, underpowered signal.

