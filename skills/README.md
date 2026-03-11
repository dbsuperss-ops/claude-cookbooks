# Claude Skills 쿡북 (Claude Skills Cookbook) 🚀

문서 생성, 데이터 분석 및 비즈니스 자동화를 위한 Claude의 스킬(Skills) 기능을 사용하는 종합 가이드입니다. 이 쿡북은 Excel, PowerPoint, PDF 생성을 위한 Claude의 내장 스킬을 활용하는 방법과 특수 워크플로우를 위한 커스텀 스킬을 구축하는 방법을 보여줍니다.

> **🎯 스킬 작동 모습 보기:** **[Claude Creates Files](https://www.anthropic.com/news/create-files)**를 확인하여 이러한 스킬들이 Claude.ai와 데스크톱 앱에서 직접 문서를 생성하고 편집하는 Claude의 능력을 어떻게 강화하는지 확인해 보세요!

## 스킬(Skills)이란 무엇인가요?

스킬은 Claude에게 특정 작업을 위한 전문적인 능력을 부여하는 지침, 실행 가능한 코드 및 리소스의 체계적인 패키지입니다. Claude가 동적으로 검색하고 로드할 수 있는 "전문 지식 패키지"라고 생각할 수 있습니다:

- 전문적인 문서 작성 (Excel, PowerPoint, PDF, Word)
- 복잡한 데이터 분석 및 시각화 수행
- 회사 전용 워크플로우 및 브랜딩 적용
- 도메인 전문 지식을 활용한 비즈니스 프로세스 자동화

📖 엔지니어링 블로그 포스트 읽기: [스킬을 통해 에이전트에게 실무 능력을 부여하기 (Equipping agents for the real world with Skills)](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

## 주요 특징

- ✨ **점진적 공개 아키텍처 (Progressive Disclosure Architecture)** - 필요할 때만 스킬을 로드하여 토큰 사용량을 최적화함
- 📊 **재무 중심 (Financial Focus)** - 재무 및 비즈니스 분석을 위한 실제 사례 제공
- 🔧 **커스텀 스킬 개발 (Custom Skills Development)** - 자신만의 스킬을 구축하고 배포하는 방법 학습
- 🎯 **프로덕션 준비 예시 (Production-Ready Examples)** - 즉시 활용 가능한 코드 제공

## 쿡북 구조

### 📚 [노트북 1: 스킬 입문 (Introduction to Skills)](notebooks/01_skills_introduction.ipynb)

빠른 시작 예제를 통해 Claude 스킬 기능의 기초를 배웁니다.

- 스킬 아키텍처 이해하기
- 베타 헤더를 통한 API 설정
- 첫 번째 Excel 스프레드시트 만들기
- PowerPoint 프레젠테이션 생성하기
- PDF 형식으로 내보내기

### 💼 [노트북 2: 재무 애플리케이션 (Financial Applications)](notebooks/02_skills_financial_applications.ipynb)

실제 재무 데이터를 사용하여 강력한 비즈니스 사용 사례를 탐색합니다.

- 차트와 피벗 테이블이 포함된 재무 대시보드 구축
- 포트폴리오 분석 및 투자 보고
- 다중 형식 워크플로우: CSV → Excel → PowerPoint → PDF
- 토큰 최적화 전략

### 🔧 [노트북 3: 커스텀 스킬 개발 (Custom Skills Development)](notebooks/03_skills_custom_development.ipynb)

자신만의 특화된 스킬을 만드는 기술을 마스터합니다.

- 재무 비율 계산기 구축하기
- 기업 브랜드 가이드라인 스킬 만들기
- 고급: 재무 모델링 스위트
- [최선의 관행 (Best practices)](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices) 및 보안 고려 사항

## 빠른 시작

### 사전 요구 사항

- Python 3.8 이상
- Anthropic API 키 ([여기에서 받기](https://console.anthropic.com/))
- Jupyter Notebook 또는 JupyterLab

### 설치 방법

1. **레포지토리 복제**

```bash
git clone https://github.com/anthropics/claude-cookbooks.git
cd claude-cookbooks/skills
```

2. **가상 환경 생성** (권장)

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

3. **의존성 설치**

```bash
pip install -r requirements.txt
```

4. **API 키 구성**

```bash
cp .env.example .env
# .env 파일을 편집하고 ANTHROPIC_API_KEY를 추가하세요.
```

5. **Jupyter 실행**

```bash
jupyter notebook
```

6. **노트북 1부터 시작하기**
   `notebooks/01_skills_introduction.ipynb`를 열고 따라해 보세요!

## 샘플 데이터

쿡북은 `sample_data/` 디렉토리에 실제와 유사한 재무 데이터셋을 포함하고 있습니다:

- 📊 **financial_statements.csv** - 분기별 손익계산서, 대차대조표 및 현금흐름표 데이터
- 💰 **portfolio_holdings.json** - 성과 지표가 포함된 투자 포트폴리오
- 📋 **budget_template.csv** - 차이 분석이 포함된 부서별 예산
- 📈 **quarterly_metrics.json** - KPI 및 운영 지표

## 프로젝트 구조

```
skills/
├── notebooks/                    # Jupyter 노트북
│   ├── 01_skills_introduction.ipynb
│   ├── 02_skills_financial_applications.ipynb
│   └── 03_skills_custom_development.ipynb
├── sample_data/                  # 재무 데이터셋
│   ├── financial_statements.csv
│   ├── portfolio_holdings.json
│   ├── budget_template.csv
│   └── quarterly_metrics.json
├── custom_skills/                # 커스텀 스킬
│   ├── financial_analyzer/
│   ├── brand_guidelines/
│   └── report_generator/
├── outputs/                      # 생성된 파일
├── docs/                         # 문서
├── requirements.txt             # Python 의존성
├── .env.example                 # 환경 변수 템플릿
└── README.md                    # 본 파일
```

## API 구성

스킬을 사용하려면 특정 베타 헤더가 필요합니다. 노트북에서 자동으로 처리하지만, 내부적으로는 다음과 같이 작동합니다:

```python
from anthropic import Anthropic

client = Anthropic(
    api_key="your-api-key",
    default_headers={
        "anthropic-beta": "code-execution-2025-08-25,files-api-2025-04-14,skills-2025-10-02"
    }
)
```

**필수 베타 헤더:**

- `code-execution-2025-08-25` - 스킬을 위한 코드 실행 활성화
- `files-api-2025-04-14` - 생성된 파일 다운로드에 필요
- `skills-2025-10-02` - 스킬 기능 활성화

## 생성된 파일 다루기

스킬이 문서(Excel, PowerPoint, PDF 등)를 생성하면 응답에 `file_id` 속성을 반환합니다. 이 파일을 다운로드하려면 **Files API**를 사용해야 합니다.

### 작동 방식

1. **스킬이 코드 실행 중 파일을 생성**합니다.
2. **응답에 생성된 각 파일의 file_id가 포함**됩니다.
3. **Files API를 사용하여** 실제 파일 내용을 다운로드합니다.
4. **로컬에 저장**하거나 필요한 처리를 수행합니다.

### 예시: Excel 파일 생성 및 다운로드

```python
from anthropic import Anthropic

client = Anthropic(api_key="your-api-key")

# 1단계: 스킬을 사용하여 파일 생성
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=4096,
    container={
        "skills": [
            {"type": "anthropic", "skill_id": "xlsx", "version": "latest"}
        ]
    },
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[{
        "role": "user",
        "content": "간단한 예산 스프레드시트가 포함된 Excel 파일을 만들어줘"
    }]
)

# 2단계: 응답에서 file_id 추출
file_id = None
for block in response.content:
    if block.type == "tool_result" and hasattr(block, 'output'):
        # 도구 출력에서 file_id 찾기
        if 'file_id' in str(block.output):
            file_id = extract_file_id(block.output)  # file_id 파싱
            break

# 3단계: Files API를 사용하여 파일 다운로드
if file_id:
    file_content = client.beta.files.download(file_id=file_id)

    # 4단계: 디스크에 저장
    with open("outputs/budget.xlsx", "wb") as f:
        f.write(file_content.read())

    print(f"✅ 파일 다운로드 완료: budget.xlsx")
```

### Files API 메서드

```python
# 파일 내용 다운로드 (바이너리)
content = client.beta.files.download(file_id="file_abc123...")
with open("output.xlsx", "wb") as f:
    f.write(content.read())  # .content가 아닌 .read()를 사용하세요.

# 파일 메타데이터 가져오기
info = client.beta.files.retrieve_metadata(file_id="file_abc123...")
print(f"파일명: {info.filename}, 크기: {info.size_bytes} 바이트")  # size가 아닌 size_bytes를 사용하세요.

# 모든 파일 목록 보기
files = client.beta.files.list()
for file in files.data:
    print(f"{file.filename} - {file.created_at}")

# 파일 삭제하기
client.beta.files.delete(file_id="file_abc123...")
```

**중요 참고 사항:**

- 파일은 Anthropic 서버에 일시적으로 저장됩니다.
- 다운로드한 파일은 로컬 `outputs/` 디렉토리에 저장해야 합니다.
- Files API는 Messages API와 동일한 API 키를 사용합니다.
- 모든 노트북에는 파일 다운로드를 위한 헬퍼 함수가 포함되어 있습니다.
- **파일은 기본적으로 덮어씌워집니다** - 셀을 다시 실행하면 기존 파일이 교체됩니다 (출력에 `[overwritten]` 표시가 나타납니다).

자세한 내용은 [Files API 문서](https://docs.claude.com/en/api/files-content)를 참조하세요.

## 내장 스킬 참조

Claude는 다음과 같은 사전 구축된 스킬을 제공합니다:

| 스킬       | ID     | 설명                                                                 |
| ---------- | ------ | --------------------------------------------------------------------------- |
| Excel      | `xlsx` | 수식, 차트, 서식이 포함된 Excel 워크북 생성 및 조작                    |
| PowerPoint | `pptx` | 슬라이드, 차트, 전환 효과가 포함된 전문적인 프레젠테이션 생성           |
| PDF        | `pdf`  | 텍스트, 표, 이미지가 포함된 서식 있는 PDF 문서 생성                  |
| Word       | `docx` | 풍부한 서식과 구조를 갖춘 Word 문서 생성                             |

## 커스텀 스킬 만들기

커스텀 스킬은 다음과 같은 구조를 따릅니다:

```
my_skill/
├── SKILL.md           # 필수: Claude를 위한 지침
├── scripts/           # 선택: Python/JS 코드
│   └── processor.py
└── resources/         # 선택: 템플릿, 데이터
    └── template.xlsx
```

자세한 내용은 [노트북 3](notebooks/03_skills_custom_development.ipynb)에서 확인하세요.

## 일반적인 사용 사례

### 재무 보고
- 분기별 자동 보고서 생성
- 예산 차이 분석
- 투자 성과 대시보드

### 데이터 분석
- 복잡한 수식을 활용한 Excel 기반 분석
- 피벗 테이블 생성
- 통계 분석 및 시각화

### 문서 자동화
- 브랜드 가이드라인이 적용된 프레젠테이션 생성
- 여러 소스로부터 보고서 취합
- 다중 형식 간 문서 변환

## 성능 팁

1. **점진적 공개 사용**: 토큰 사용량을 최소화하기 위해 스킬을 단계별로 로드합니다.
2. **배치 작업**: 단일 대화에서 여러 파일을 처리합니다.
3. **스킬 조합**: 복잡한 워크플로우를 위해 여러 스킬을 결합합니다.
4. **캐시 재사용**: 로드된 스킬을 재사용하기 위해 컨테이너 ID를 사용합니다.

## 문제 해결

### 일반적인 문제

**API 키를 찾을 수 없음**
`ValueError: ANTHROPIC_API_KEY not found`
→ `.env.example`을 `.env`로 복사하고 키를 추가했는지 확인하세요.

**Skills 베타 헤더 누락**
`Error: Skills feature requires beta header`
→ 노트북에 표시된 대로 올바른 베타 헤더를 사용하고 있는지 확인하세요.

**토큰 한도 초과**
`Error: Request exceeds token limit`
→ 큰 작업을 작은 단위로 나누거나 점진적 공개를 사용하세요.

## 리소스

### 문서
- 📖 [Claude API 문서](https://docs.anthropic.com/en/api/messages)
- 🔧 [Skills 문서](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)

### 지원 기사
- 📚 [스킬을 사용하여 Claude에게 당신의 업무 방식을 가르치기](https://support.claude.com/en/articles/12580051-teach-claude-your-way-of-working-using-skills) - 스킬 활용 가이드
- 🛠️ [대화를 통해 Claude로 스킬을 만드는 방법](https://support.claude.com/en/articles/12599426-how-to-create-a-skill-with-claude-through-conversation) - 대화형 스킬 생성 가이드

---

**준비되셨나요?** [노트북 1](notebooks/01_skills_introduction.ipynb)을 열고 멋진 것을 만들어 봅시다! 🎉
    
