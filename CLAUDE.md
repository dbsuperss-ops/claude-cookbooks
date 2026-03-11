# Claude 쿡북 (Claude Cookbooks)

Claude API를 사용하여 빌드하기 위한 Jupyter 노트북 및 Python 예제 모음입니다.

## 빠른 시작

```bash
# 의존성 설치
uv sync --all-extras

# pre-commit 훅 설치
uv run pre-commit install

# API 키 설정
cp .env.example .env
# .env 파일을 수정하고 ANTHROPIC_API_KEY를 추가하세요.
```

## 개발 기능/명령어

```bash
make format        # ruff를 사용하여 코드 포맷팅
make lint          # 린팅 실행
make check         # 포맷 체크 + 린트 실행
make fix           # 이슈 자동 수정 + 포맷팅
make test          # pytest 실행
```

또는 uv를 직접 사용하는 경우:

```bash
uv run ruff format .           # 포맷팅
uv run ruff check .            # 린팅
uv run ruff check --fix .      # 자동 수정
uv run pre-commit run --all-files
```

## 코드 스타일

- **한 줄 길이:** 100자
- **따옴표:** 큰따옴표 (Double quotes)
- **포맷터:** Ruff

노트북의 경우 파일 중간의 임포트(E402), 재정의(F811), 그리고 변수 명명(N803, N806)에 대해 완화된 규칙을 적용합니다.

## Git 워크플로우

**브랜치 명명:** `<사용자명>/<기능-설명>`

**커밋 형식 (Conventional Commits):**

```
feat(scope): 새로운 기능 추가
fix(scope): 버그 수정
docs(scope): 문서 업데이트
style: 린트/포맷팅
```

## 주요 규칙

1. **API 키:** `.env` 파일을 절대 커밋하지 마세요. 항상 `os.environ.get("ANTHROPIC_API_KEY")`를 사용하세요.
2. **의존성:** `uv add <패키지>` 또는 `uv add --dev <패키지>`를 사용하세요. `pyproject.toml`을 직접 수정하지 마세요.
3. **모델:** 최신 Claude 모델을 사용하세요. 최신 버전은 docs.anthropic.com에서 확인하세요.

   - Sonnet: `claude-sonnet-4-6`
   - Haiku: `claude-haiku-4-5`
   - Opus: `claude-opus-4-6`
   - **날짜가 포함된 모델 ID는 사용하지 마세요** (예: `claude-sonnet-4-6-20250514`). 항상 날짜가 없는 에일리어스(Alias)를 사용하세요.
   - **Bedrock 모델 ID**는 형식이 다릅니다. 문서에 명시된 기본 Bedrock 모델 ID를 사용하세요:
     - Opus 4.6: `anthropic.claude-opus-4-6-v1`
     - Sonnet 4.5: `anthropic.claude-sonnet-4-5-20250929-v1:0`
     - Haiku 4.5: `anthropic.claude-haiku-4-5-20251001-v1:0`
     - 글로벌 엔드포인트에는 `global.`을 앞에 붙이는 것을 권장합니다: `global.anthropic.claude-opus-4-6-v1`
     - 참고: Opus 4.6 이전의 Bedrock 모델은 Bedrock 모델 ID에 날짜가 포함된 ID가 필요합니다.
4. **노트북:**

   - 노트북의 출력 결과를 유지하세요 (시연 목적으로 의도됨).
   - 노트북 하나당 하나의 개념만 다룹니다.
   - 노트북이 처음부터 끝까지 오류 없이 실행되는지 테스트하세요.
5. **품질 체크:** 커밋하기 전에 `make check`를 실행하세요. Pre-commit 훅이 포맷팅과 노트북 구조를 검증합니다.

## 슬래시 명령어

다음 명령어들은 Claude Code와 CI에서 사용할 수 있습니다:

- `/notebook-review` - 노트북 품질 리뷰
- `/model-check` - Claude 모델 참조 유효성 검사
- `/link-review` - 변경된 파일의 링크 확인

## 프로젝트 구조

```
capabilities/      # 핵심 Claude 기능 (RAG, 분류 등)
skills/            # 고급 스킬 기반 노트북
tool_use/          # 도구 사용 및 통합 패턴
multimodal/        # 비전 및 이미지 처리
misc/              # 배치 프로세싱, 캐싱, 유틸리티
third_party/       # Pinecone, Voyage, Wikipedia 통합
extended_thinking/ # 확장된 사고(Thinking) 패턴
scripts/           # 검증 스크립트
.claude/           # Claude Code 명령어 및 스킬
```

## 새로운 쿡북 추가하기

1. 적절한 디렉토리에 노트북을 생성합니다.
2. 제목, 설명, 경로, 작성자, 카테고리를 포함하여 `registry.yaml`에 항목을 추가합니다.
3. 새로운 기여자라면 `authors.yaml`에 작성자 정보를 추가합니다.
4. 품질 체크를 실행하고 PR을 제출합니다.
