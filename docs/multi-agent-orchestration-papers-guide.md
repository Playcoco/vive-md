# 멀티에이전트 오케스트레이션 논문 가이드

> 2023~2026년 멀티에이전트 소프트웨어 개발 관련 핵심 논문 분석 및 적용 가이드

---

## 📚 문서 개요

이 문서는 Octo Orchestra 및 바이브코딩 환경에서 멀티에이전트 시스템을 설계할 때 참고할 수 있는 주요 연구 논문들을 정리한 것입니다.

**원본 문서**: `../multi-agent-orchestration-papers.md`

---

## 🎯 핵심 논문 분류

### 1. 역할 기반 에이전트 시스템

#### ChatDev (ACL 2024)
- **핵심**: 대화 기반 가상 소프트웨어 회사 시뮬레이션
- **메커니즘**: Chat Chain - 원자적 채팅 세션으로 작업 분해
- **적용 포인트**: 에이전트별 명확한 역할 시스템 프롬프트 설계

#### MetaGPT (ICLR 2024)
- **핵심**: SOP 기반 문서 소통
- **ChatDev와의 차이**: 대화 대신 **구조화된 문서**로 소통
- **적용 포인트**: PRD → System Design → Task List 계층 구조

#### HyperAgent (2024)
- **4역할 시스템**: Planner → Navigator → Code Editor → Executor
- **적용 포인트**: 계획 → 탐색 → 편집 → 검증의 명확한 4단계

---

### 2. 오케스트레이션 아키텍처

#### Evolving Orchestration (NeurIPS 2025)
- **Puppeteer 패러다임**: RL 기반 동적 오케스트레이터
- **핵심**: 작업 상태에 따라 에이전트를 동적으로 활성화/비활성화
- **적용 포인트**: 에이전트 완료 순서에 따른 동적 작업 조정

#### Cross-Team Orchestration (Croto)
- **패턴**: 독립 팀 병렬 → 교차 협업
- **핵심**: 여러 팀이 동시에 다른 솔루션 경로 탐색
- **적용 포인트**: git worktree 기반 병렬 에이전트 패턴

#### AgentOrchestra (TEA Protocol)
- **TEA**: Tool, Environment, Agent를 일급 자원으로 모델링
- **성과**: GAIA 벤치마크 89.04% (SOTA)
- **적용 포인트**: 라이프사이클 관리, 버전 관리, 롤백

#### TDAG (Neural Networks 2024)
- **동적 작업 분해**: 미리 정해진 분해가 아닌 점진적 발견
- **에이전트 자동 생성**: 각 하위 작업에 맞춤형 에이전트 생성

---

### 3. 코드 생성 특화 멀티에이전트

#### MapCoder (ACL 2024)
- **4단계 파이프라인**: Retrieval → Planning → Coding → Debugging
- **성과**: HumanEval 93.9%, MBPP 83.1%
- **적용 포인트**: 계획 수립 시 코드베이스 탐색을 필수 1단계로

#### AgentCoder (2023)
- **3역할 반복 루프**: Programmer ↔ Test Designer ↔ Test Executor
- **성과**: HumanEval 96.3%, 토큰 사용량 59% 절감
- **적용 포인트**: Maker-Checker 패턴, 테스트 루프 강화

---

### 4. 실전 소프트웨어 엔지니어링 에이전트

#### SWE-agent (2024)
- **핵심**: Agent-Computer Interface (ACI) 설계
- **통찰**: LLM 에이전트는 전용 인터페이스가 필요한 새로운 종류의 사용자

#### Live-SWE-agent (2025)
- **혁신**: 런타임 자기 진화 (별도 학습 없이 문제 풀면서 개선)
- **성과**: SWE-bench Verified 77.4% (최고)
- **적용 포인트**: 오케스트레이션 결과 로그 누적 → 학습

---

### 5. 실패 분석 & 도전 과제

#### MAST (2025) - 멀티에이전트 시스템 실패 분류
- **데이터**: 7개 프레임워크, 1,600+ 트레이스
- **3대 실패 카테고리**:
  1. 시스템 설계 문제 (작업 분배, 역할 중복)
  2. 에이전트 간 불일치 (소통 실패, 컨텍스트 손실)
  3. 작업 검증 문제 (검증 부재, 완료 조건 모호)

#### MAS Challenges (2024)
- **4대 도전 과제**:
  1. 작업 할당 최적화
  2. 추론 강화
  3. 컨텍스트 관리
  4. 메모리 시스템

---

## 🚀 Octo Orchestra 적용 로드맵

### 즉시 적용 가능 (Short-term)

| 아이디어 | 출처 | 적용 방법 |
|----------|------|-----------|
| 역할 시스템 강화 | ChatDev, MetaGPT | 프롬프트 시작에 `[ROLE]` 섹션 추가 |
| 구조화된 계획 산출물 | MetaGPT | PRD → Design → Task List 계층 |
| 테스트 루프 강화 | AgentCoder | `[VERIFY]`에 구체적 테스트 절차 |
| 방어적 프롬프트 | MAST | `[WARNINGS]` 섹션으로 실패 방어 |
| 결과 보고서 | MetaGPT | 완료 시 `/tmp/octo-report-{nickname}.md` 생성 |

### 중기 로드맵 (Medium-term)

- **교차 검증**: 에이전트 간 코드 리뷰
- **동적 재할당**: 비서의 진행 상황 모니터링 및 조정
- **Maker-Checker 분리**: 개발 에이전트와 QA 에이전트 분리

### 장기 비전 (Long-term)

- **자기 진화 비서**: 결과 로그 기반 학습
- **모델별 최적 역할 할당**: 작업 복잡도에 따른 모델 선택

---

## 📖 참고 문헌

### 역할 기반 시스템
- [ChatDev: Communicative Agents for Software Development](https://arxiv.org/abs/2307.07924) — ACL 2024
- [MetaGPT: Meta Programming for A Multi-Agent Collaborative Framework](https://arxiv.org/abs/2308.00352) — ICLR 2024
- [HyperAgent: Generalist Software Engineering Agents](https://openreview.net/forum?id=PZf4RsPMBG) — 2024

### 오케스트레이션 아키텍처
- [Multi-Agent Collaboration via Evolving Orchestration](https://arxiv.org/abs/2505.19591) — NeurIPS 2025
- [Multi-Agent Collaboration via Cross-Team Orchestration](https://arxiv.org/abs/2406.08979) — 2024
- [AgentOrchestra: TEA Protocol](https://arxiv.org/abs/2506.12508) — 2025
- [TDAG: Dynamic Task Decomposition and Agent Generation](https://arxiv.org/abs/2402.10178) — Neural Networks 2024

### 코드 생성
- [MapCoder: Multi-Agent Code Generation](https://arxiv.org/abs/2405.11403) — ACL 2024
- [AgentCoder: Multi-Agent Code Generation with Iterative Testing](https://arxiv.org/abs/2312.13010) — 2023

### 소프트웨어 엔지니어링 에이전트
- [SWE-agent: Agent-Computer Interfaces](https://arxiv.org/abs/2405.15793) — 2024
- [Live-SWE-agent: Self-Evolve on the Fly](https://arxiv.org/abs/2511.13646) — 2025

### 서베이 & 분석
- [LLM-Based Multi-Agent Systems for SE: Literature Review](https://arxiv.org/abs/2404.04834) — ACM TOSEM
- [Why Do Multi-Agent LLM Systems Fail?](https://arxiv.org/abs/2503.13657) — 2025
- [LLM Multi-Agent Systems: Challenges and Open Problems](https://arxiv.org/abs/2402.03578) — 2024
