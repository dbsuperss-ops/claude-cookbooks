# Skills 쿡북 - Claude Code 가이드

## 프로젝트 개요

문서 생성(Excel, PowerPoint, PDF)을 위한 Claude의 스킬(Skills) 기능을 보여주는 종합적인 Jupyter 노트북 쿡북입니다. 자신의 애플리케이션에 스킬을 통합하려는 개발자를 위해 설계되었습니다.

## 빠른 시작 명령어

### 환경 설정
```bash
# 가상 환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치 (스킬 지원을 위해 반드시 로컬 whl 사용)
pip install -r requirements.txt

# API 키 구성
cp .env.example .env
# .env 파일을 수정하고 ANTHROPIC_API_KEY를 추가하세요.
```

### 노트북 실행
```bash
# Jupyter 실행
jupyter notebook

# 또는 Jupyter 확장이 설치된 VSCode 사용
# VSCode에서 venv 커널을 선택했는지 확인하세요: Cmd+Shift+P → "Python: Select Interpreter"
```

### 테스트 및 검증
```bash
# 환경 및 SDK 버전 확인
python -c "import anthropic; print(f'SDK 버전: {anthropic.__version__}')"

# 생성된 파일이 있는지 outputs/ 디렉토리 확인
ls -lh outputs/
```

## 아키텍처 개요

### 디렉토리 구조
```
skills/
├── notebooks/              # 3단계의 Jupyter 노트북
│   ├── 01_skills_introduction.ipynb
│   ├── 02_skills_financial_applications.ipynb  # 작업 중 (WIP)
│   └── 03_skills_custom_development.ipynb      # 작업 중 (WIP)
├── sample_data/           # 예제용 재무 데이터셋
├── custom_skills/         # 커스텀 스킬 개발 영역
├── outputs/               # 생성된 파일들 (xlsx, pptx, pdf)
├── file_utils.py          # Files API 헬퍼 함수
└── docs/                  # 구현 추적 문서
```

### 핵심 기술 세부 사항

**Beta API 요구 사항:**
- 모든 스킬 기능은 `client.beta.*` 네임스페이스를 사용합니다.
- 필수 베타 헤더: `code-execution-2025-08-25`, `files-api-2025-04-14`, `skills-2025-10-02`
- `container` 파라미터와 함께 `client.beta.messages.create()`를 사용해야 합니다.
- 코드 실행 도구(`code_execution_20250825`)가 필수입니다.
- 사전 구축된 에이전트 스킬을 `skill_id`로 참조하거나, Skills API를 통해 직접 생성하여 업로드할 수 있습니다.

**Files API 통합:**
- 스킬은 파일을 생성하고 `file_id` 속성을 반환합니다.
- 파일을 다운로드하려면 `client.beta.files.download()`를 사용해야 합니다.
- 파일 정보를 얻으려면 `client.beta.files.retrieve_metadata()`를 사용해야 합니다.
- `file_utils.py`의 헬퍼 함수들이 추출 및 다운로드를 처리합니다.

**내장 스킬:**
- `xlsx` - 수식과 차트가 포함된 Excel 워크북
- `pptx` - PowerPoint 프레젠테이션
- `pdf` - PDF 문서
- `docx` - Word 문서

## 개발 시 유의사항 (Gotchas)

### 1. SDK 버전
**중요**: 스킬 기능을 지원하는 Anthropic SDK 버전 0.71.0 이상이 설치되어 있는지 확인하세요.
```bash
pip install anthropic>=0.71.0
# 업데이트 후에는 Jupyter 커널을 재시작하세요!
```

### 2. Beta 네임스페이스 필수
- **문제**: `container` 파라미터가 인식되지 않거나 Files API가 실패함
- **해결책**: `client.beta.messages.create()` 및 `client.beta.files.*`를 사용하세요.

### 3. Beta 헤더 배치
- **문제**: `default_headers`에 스킬 베타를 설정하면 모든 요청에서 코드 실행이 요구됨
- **해결책**: 대신 요청마다 `betas` 파라미터를 사용하세요.

### 4. File ID 추출
- **문제**: 응답 구조가 표준 Messages API와 다름
- **해결책**: 파일 ID는 `bash_code_execution_tool_result.content.content[0].file_id`에 있습니다. `file_utils.extract_file_ids()`를 사용하세요.

### 5. Files API 응답 객체
- **문제**: `'BinaryAPIResponse'` 객체에 `content` 속성이 없거나, `'FileMetadata'` 객체에 `size` 속성이 없음
- **해결책**: 파일 내용에는 `.read()`를, 파일 크기에는 `.size_bytes`를 사용하세요.

### 6. Jupyter 커널 선택
- **문제**: 잘못된 Python 인터프리터 선택으로 인한 의존성 문제
- **해결책**: VSCode/Jupyter에서 항상 venv 커널을 선택하세요.

### 7. 모듈 리로드 필수
- **문제**: `file_utils.py`의 변경 내용이 실행 중인 노트북에 반영되지 않음
- **해결책**: 커널을 재시작하거나 `importlib.reload(file_utils)`를 사용하여 모듈을 다시 로드하세요.

### 8. 문서 생성 시간
- **문제**: 파일 생성에 일반적인 API 호출보다 긴 시간이 걸려 사용자가 셀이 멈춘 것으로 오해할 수 있음
- **실제 관찰된 시간:**
  - Excel: ~2분
  - PowerPoint: ~1-2분 (간단한 2-3 슬라이드 기준)
  - PDF: ~1-2분
- **해결책**: 파일 생성 셀 앞에 명확한 예상 시간을 안내하세요.

## 일반적인 작업

### 새로운 노트북 섹션 추가하기
1. `01_skills_introduction.ipynb`의 기존 구조를 따르세요.
2. 임포트와 베타 헤더가 포함된 설정 셀을 포함하세요.
3. API 호출, 응답 처리, 파일 다운로드 과정을 보여주세요.
4. 에러 처리 예시를 추가하세요.

### 샘플 데이터 생성하기
1. `sample_data/`에 실제와 유사한 재무 데이터를 추가하세요.
2. 표 형식은 CSV, 구조화된 데이터는 JSON을 사용하세요.
3. 파일 크기를 적정 수준(<100KB)으로 유지하세요.

### 파일 다운로드 테스트하기
1. 노트북 셀을 실행하여 파일을 생성합니다.
2. 응답에서 `file_id`를 확인합니다.
3. `download_all_files()` 헬퍼를 사용합니다.
4. `outputs/` 디렉토리에 파일이 있는지 확인하고 실행하여 검증합니다.

## 리소스

- **API 참조**: https://docs.claude.com/en/api/messages
- **Files API**: https://docs.claude.com/en/api/files-content
- **Skills 문서**: https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview

## 환경 변수

`.env` 파일에 필수:
```bash
ANTHROPIC_API_KEY=your-api-key-here
```
    
