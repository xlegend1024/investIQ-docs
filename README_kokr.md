---
title: README (한국어)
nav_exclude: true
search_exclude: true
---

# InvestIQ 미디엄 시리즈 — 투자 비전문가가 AI와 함께 알고리즘 트레이딩 시스템을 만들다

[English (기본)](./README.md) | [한국어](./README_kokr.md)

> **시리즈 제목:** *투자 비전문가가 AI 팀과 함께 알고리즘 트레이딩 시스템을 만든 기록*
>
> 5부 기술 블로그 시리즈. 대상 독자: **데이터 분석가**와 **비즈니스 의사결정권자**.
> 일관된 흐름: 비전문가가 LLM 기반 AI 에이전트의 도움으로 end-to-end 알고리즘 트레이딩 시스템을 만들고,
> 최소한의 예산으로 페이퍼 계정에서 돌리며, 그 결과를 — AI와 일할 때 주의할 점을 포함해 — **정직하게
> 분석**합니다.
>
> **중요한 구분:** 매매 의사결정은 **코드로 정의된 알고리즘**(기술적 분석 + 포트폴리오 최적화 + 리스크
> 규칙)이 내립니다. AI 에이전트는 그 프로그램의 **개발·연구·리뷰 하네스**였지, 실시간으로 거래를 결정하는
> 주체가 아닙니다.

---

## 시리즈 구성

| # | 제목 | 한 줄 요약 | 핵심 시각자료 |
|---|---|---|---|
| **1** | [배경 — 왜, 누가, 무엇으로](./ko-kr/part1_background_and_setup.md) | 비전문가 + AI 팀(Squad) + 14개 마이크로서비스 페이퍼 MVP | 아키텍처 / 안전 바닥 플로차트 |
| **2.1** | [데이터 — 수집 파이프라인과 진실의 원천](./ko-kr/part2_1_data_pipeline.md) | 멀티소스 수집 · 단일 Alpaca 가격 소스 · 브로커 체결 기록 | 커버리지·감성 분포 차트 |
| **2.2** | [유니버스 선택 — 성과는 어디에 있는가](./ko-kr/part2_2_universe_selection.md) | 비용 포함 N일 보유 백테스트 · 엣지의 대부분은 일상 신호가 아니라 유니버스 표류 | 호라이즌별 자산곡선, 분해 |
| **2.3** | [대조군 비교와 전략적 방향](./ko-kr/part2_3_control_comparison.md) | 거래군 vs 대조군 · placebo(거래 이전) 윈도우 · 이중차분 · 선택은 스킬이 아니라 모멘텀을 올라탐 | 그룹별 사전/사후, DiD, dose-response |
| **3.1** | [전략 — 종목 점수 매기기 (Spec-070)](./ko-kr/part3_1_scoring.md) | 컴포지트 점수: 모멘텀/기술 + 뉴스 감성 × 풀백 배수 | 컴포지트 점수 플로차트 |
| **3.2** | [Post-Market 파이프라인과 포트폴리오 최적화](./ko-kr/part3_2_postmarket_pipeline.md) | 야간 post-market 배치 · Markowitz / Risk Parity · 품질 게이트 · 집중도 측 | 파이프라인 + 최적화 플로차트 |
| **3.3** | [실제 할당, 한 줄씩 읽기](./ko-kr/part3_3_real_allocation_example.md) | 실제 2026-06-12 리밸런싱 플랜 · 31개 보유 종목 · 정수 주식 거래 · 리스크 게이트 3건 차단 | 실제 목표 비중 바, 14일 비중 히트맵 |
| **3.4** | [플랜에서 주문으로 — 승인 게이트 실행](./ko-kr/part3_4_approval_gated_execution.md) | 제안 → 검토 → 실행 · HMAC 토큰 · fail-closed 거부권 | 승인 게이트 시퀀스 다이어그램 |
| **4** | [손실의 실체 — 인과적 해석](./ko-kr/part4_loss_attribution.md) | 927 라운드트립 −$369.85 · 단일 종목 테일(ASTH) · 손익분기와 구별 불가 · 뉴스 신호 검정력 부족 | H1–H6 귀인 차트, IC 항기간 구조 |
| **5** | [교훈 — AI와 함께 일하기](./ko-kr/part5_lessons_for_working_with_ai.md) | 사전등록 · 권위 있는 기록 · 유니버스 분리 · 하드 캡 · 거부권 구조 | AI 협업 루프 플로차트 |

---

## 핵심 사실 (단일 진실의 원천)

- **윈도우:** 2026-04-13 ~ 2026-06-13 (42거래일), Alpaca 페이퍼 계정.
- **손실 귀인(`loss_attribution_v2`):** 133종목 927 롱 라운드트립에서 −$369.85 실현; 승률 41.7%, 페이오프
  1.31; ASTH −$2,712(ASTH 제외 +$2,343); 부트스트랩 95% CI [−$3,156, +$2,149] — 손익분기와 구별 불가.
- **뉴스 인과(`news_causality_v3`):** IC가 양수이며 호라이즌에 따라 증가(1d +0.028 → 10d +0.061)하나
  유의하지 않음; 방향성은 일관되나 검정력이 부족한 신호. 가격은 Alpaca Market Data, 감성은 InvestIQ
  news-intel.

## 발행 가이드

- **그림:** PNG는 `research/loss_attribution_v2/figures/`(H1–H6)와
  `research/news_causality_v3/figures/`(01/02/03 시리즈)에 있습니다. Medium 업로드 시 직접 첨부.
- **Mermaid:** Medium은 mermaid를 네이티브 렌더링하지 않으므로 [mermaid.live](https://mermaid.live)에서
  각 다이어그램을 PNG/SVG로 내보내 임베드.
- **범위 배너:** 모든 수치는 단일 윈도우의 페이퍼 계정 실현 손익입니다. 각 편 상단의 범위·한계 안내를 유지.
- **태그:** `#AlgorithmicTrading #LLM #QuantResearch #AIAgents #DataScience`.


