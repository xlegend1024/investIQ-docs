---
title: Home
nav_order: 1
description: "InvestIQ — Building an Algorithmic Trading System as an Investing Novice, with an AI Team."
permalink: /
---

# InvestIQ — An Investing Novice Builds an Algorithmic Trading System with AI
{: .fs-8 }

A 5-part technical series on building an end-to-end algorithmic trading system as a
non-specialist, with the help of an LLM-based AI team — run on a minimal budget in a
paper account, and analyzed **honestly**.
{: .fs-5 .fw-300 }

[English series](en-us/index.md){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[한국어 시리즈](ko-kr/index.md){: .btn .fs-5 .mb-4 .mb-md-0 }

---

> **Important distinction.** Trading decisions are made by **code-defined algorithms**
> (technical analysis + portfolio optimization + risk rules). The AI agents were the
> **development, research, and review harness** for that program — not the entity that
> decides trades in real time.

## Read the series

| # | English | 한국어 |
|---|---|---|
| 1 | [Background](en-us/part1_background_and_setup.md) | [배경](ko-kr/part1_background_and_setup.md) |
| 2.1 | [Data Pipeline](en-us/part2_1_data_pipeline.md) | [데이터 파이프라인](ko-kr/part2_1_data_pipeline.md) |
| 2.2 | [Universe Selection](en-us/part2_2_universe_selection.md) | [유니버스 선택](ko-kr/part2_2_universe_selection.md) |
| 2.3 | [Control-Group Comparison](en-us/part2_3_control_comparison.md) | [대조군 비교](ko-kr/part2_3_control_comparison.md) |
| 3.1 | [Scoring (Spec-070)](en-us/part3_1_scoring.md) | [종목 점수 (Spec-070)](ko-kr/part3_1_scoring.md) |
| 3.2 | [Post-Market Pipeline](en-us/part3_2_postmarket_pipeline.md) | [Post-Market 파이프라인](ko-kr/part3_2_postmarket_pipeline.md) |
| 3.3 | [A Real Allocation](en-us/part3_3_real_allocation_example.md) | [실제 할당](ko-kr/part3_3_real_allocation_example.md) |
| 3.4 | [Approval-Gated Execution](en-us/part3_4_approval_gated_execution.md) | [승인 게이트 실행](ko-kr/part3_4_approval_gated_execution.md) |
| 4 | [What the Loss Actually Was](en-us/part4_loss_attribution.md) | [손실의 실체](ko-kr/part4_loss_attribution.md) |
| 5 | [Lessons — Working with AI](en-us/part5_lessons_for_working_with_ai.md) | [교훈 — AI와 함께 일하기](ko-kr/part5_lessons_for_working_with_ai.md) |

## Key facts (single source of truth)

- **Window:** 2026-04-13 to 2026-06-13 (42 trading days), Alpaca paper account.
- **Loss attribution:** realized −$369.85 across 927 long round-trips in 133 names;
  win rate 41.7%, payoff 1.31; ASTH −$2,712 (ex-ASTH +$2,343); bootstrap 95% CI
  [−$3,156, +$2,149] — indistinguishable from break-even.
- **News causality:** IC positive and rising with horizon (1d +0.028 → 10d +0.061)
  but not significant; a directionally consistent, underpowered signal.
