# CLAUDE.md - 비서실장(Chief of Staff) 컨텍스트

## 회사 개요
- **회사명**: TechStart Inc
- **단계**: 시리즈 A (2024년 1월 1,000만 달러 유치 완료)
- **산업**: B2B SaaS - AI 기반 개발자 도구
- **설립**: 2022년
- **본사**: 미국 캘리포니아주 샌프란시스코

## 재무 현황
- **월간 비용 소모율 (Monthly Burn Rate)**: 약 $500,000
- **현재 가용 기간 (Runway)**: 20개월 (2025년 9월까지)
- **ARR (연간 반복 매출)**: $2.4M (전월 대비 15% 성장 중)
- **은행 잔고**: $10M
- **직원당 매출**: $48K

## 팀 구조
- **총 인원**: 50명
- **엔지니어링**: 25명 (50%)
  - 백엔드: 12명
  - 프론트엔드: 8명
  - DevOps/SRE: 5명
- **영업 및 마케팅**: 12명 (24%)
- **제품 (Product)**: 5명 (10%)
- **운영 (Operations)**: 5명 (10%)
- **임원진 (Executive)**: 3명 (6%)

## 핵심 지표
- **고객 수**: 120개 기업 고객
- **NPS 점수**: 72
- **월간 이탈률 (Monthly Churn)**: 2.5%
- **CAC (고객 획득 비용)**: $15,000
- **LTV (고객 생애 가치)**: $85,000
- **CAC 회수 기간**: 10개월

## 현재 우선순위 (2024년 2분기)
1. **채용**: 제품 개발 가속화를 위해 엔지니어 10명 추가 채용
2. **제품**: 2분기 말까지 AI 코드 리뷰 기능 출시
3. **영업**: 유럽 시장으로 확장
4. **투자 유치**: 시리즈 B 대화 시작 (목표: $30M)

## 보상 벤치마크
- **시니어 엔지니어**: $180K - $220K + 0.1-0.3% 지분
- **주니어 엔지니어**: $100K - $130K + 0.05-0.1% 지분
- **엔지니어링 매니저**: $200K - $250K + 0.3-0.5% 지분
- **엔지니어링 VP**: $250K - $300K + 0.5-1% 지분

## 이사회 구성
- **CEO**: Sarah Chen (창업자)
- **투자자 1**: Mark Williams (Sequoia Capital)
- **투자자 2**: Jennifer Park (Andreessen Horowitz)
- **사외이사**: Michael Torres (전 GitHub CTO)

## 경쟁 환경
- **주요 경쟁사**: DevTools AI, CodeAssist Pro, SmartDev Inc
- **차별점**: 우수한 AI 정확도, 10배 빠른 처리 속도
- **시장 규모**: $5B (연간 25% 성장 중)

## 최근 결정 사항
- 시니어 백엔드 엔지니어 3명 채용 승인 (2024년 3월)
- 프리미엄(Freemium) 등급 출시 (2024년 2월)
- 유럽 법인 설립 (2024년 1월)
- 시리즈 A 투자 유치 완료 (2024년 1월)

## 예정된 결정 사항
- 경쟁사 SmartDev Inc 인수 여부 (제시가 $8M)
- 3분기 채용 계획 (엔지니어링 vs. 영업 집중도)
- 사무실 확장 vs. 원격 우선(Remote-first) 전략
- 초기 직원을 위한 스톡옵션 추가 부여(Refresh)

## 위험 요소
- AWS에 대한 높은 의존도 (매출원가의 70%)
- 핵심 엔지니어 이탈 방지 (3명의 핵심 팀원)
- 빅테크 기업과의 경쟁 심화
- 기업 영업에 대한 잠재적인 경제 불황의 영향

## 사용 가능한 스크립트

### simple_calculation.py
런웨이 및 비용 소모율 분석을 위한 빠른 재무 지표 계산기입니다.
스크립트 위치: `./scripts/simple_calculation.py`

**사용법:**
```bash
python scripts/simple_calculation.py <total_runway> <monthly_burn>
```

**예시:**
```bash
python scripts/simple_calculation.py 10000000 500000
```

**출력:** monthly_burn, runway_months, total_runway_dollars, quarterly_burn, burn_rate_daily를 포함한 JSON 형식

기억하세요: 비서실장으로서 당신은 financial_data/ 디렉토리의 재무 데이터에 접근할 수 있으며, 전문적인 분석이 필요한 경우 서브 에이전트(financial-analyst 및 recruiter)에게 업무를 위임할 수 있습니다.
    