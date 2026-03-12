# Claude 쿡북 기여 가이드 (Contributing to Claude Cookbooks)

Claude 쿡북에 관심을 가져주셔서 감사합니다! 이 가이드는 개발 시작을 돕고 여러분의 기여가 품질 기준을 충족하는지 확인하는 데 도움이 될 것입니다.

## 개발 설정 (Development Setup)

### 사전 요구 사항

- Python 3.11 이상
- [uv](https://docs.astral.sh/uv/) 패키지 매니저 (권장) 또는 pip

### 빠른 시작

1. **uv 설치** (권장 패키지 매니저):
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   
   또는 Homebrew 사용 시:
   ```bash
   brew install uv
   ```

2. **레포지토리 클론**:
   ```bash
   git clone https://github.com/anthropics/anthropic-cookbook.git
   cd anthropic-cookbook
   ```

3. **개발 환경 설정**:
   ```bash
   # 가상 환경 생성 및 의존성 설치
   uv sync --all-extras
   
   # 또는 pip 사용 시:
   pip install -e ".[dev]"
   ```

4. **pre-commit 훅 설치**:
   ```bash
   uv run pre-commit install
   # 또는: pre-commit install
   ```

5. **API 키 설정**:
   ```bash
   cp .env.example .env
   # .env 파일을 수정하여 Claude API 키를 추가하십시오.
   ```

## 품질 기준 (Quality Standards)

이 레포지토리는 코드 품질을 유지하기 위해 자동화된 도구들을 사용합니다:

### 노트북 검증 스택 (The Notebook Validation Stack)

- **[nbconvert](https://nbconvert.readthedocs.io/)**: 테스트를 위한 노트북 실행
- **[ruff](https://docs.astral.sh/ruff/)**: 기본 Jupyter 지원 기능이 포함된 빠른 Python 린터 및 포매터
- **Claude AI 리뷰**: Claude를 사용한 지능형 코드 리뷰

**참고**: 노트북 출력물은 사용자가 예상 결과를 확인할 수 있도록 의도적으로 레포지토리에 유지됩니다.

### Claude Code 슬래시 커멘드

이 레포지토리에는 로컬 개발(Claude Code) 및 GitHub Actions CI에서 작동하는 슬래시 커맨드가 포함되어 있습니다. Claude Code로 이 레포지토리에서 작업할 때 다음 커맨드들을 자동으로 사용할 수 있습니다.

**사용 가능한 커맨드**:
- `/link-review` - 마크다운 및 노트북의 링크 유효성 검사
- `/model-check` - Claude 모델 사용이 최신인지 확인
- `/notebook-review` - 종합적인 노트북 품질 체크

**Claude Code에서의 사용 예시**:
```bash
# CI에서 실행될 것과 동일한 검증 실행
/notebook-review skills/my-notebook.ipynb
/model-check
/link-review README.md
```

이 커맨드들은 CI 파이프라인과 동일한 검증 로직을 사용하여, 푸시 전에 문제를 발견할 수 있게 돕습니다. 커맨드 정의는 로컬 및 CI 공용으로 `.claude/commands/`에 저장되어 있습니다.

### 커밋 전 확인 사항

1. **품질 체크 실행**:
   ```bash
   uv run ruff check skills/ --fix
   uv run ruff format skills/
   
   uv run python scripts/validate_notebooks.py
   ```

2. **노트북 실행 테스트** (선택 사항, API 키 필요):
   ```bash
   uv run jupyter nbconvert --to notebook \
     --execute skills/classification/guide.ipynb \
     --ExecutePreprocessor.kernel_name=python3 \
     --output test_output.ipynb
   ```

### Pre-commit 훅 (Hooks)

Pre-commit 훅은 코드 품질을 보장하기 위해 각 커밋 전에 자동으로 실행됩니다:

- ruff를 이용한 코드 포맷팅
- 노트북 구조 검증

훅이 실패하면 문제를 수정한 후 다시 커밋을 시도하십시오.

## 기여 가이드라인 (Contribution Guidelines)

### 노트북 최선 관행 (Best Practices)

1. **API 키에 환경 변수 사용**:
   ```python
   import os
   api_key = os.environ.get("ANTHROPIC_API_KEY")
   ```

2. **최신 Claude 모델 사용**:
   - 유지보수성을 위해 가능한 경우 모델 별칭(Alias)을 사용하십시오.
   - 최신 Haiku 모델: `claude-haiku-4-5` (Haiku 4.5)
   - 현재 모델 확인: https://docs.claude.com/en/docs/about-claude/models/overview
   - Claude가 PR 리뷰 시 모델 사용의 적절성을 자동으로 검증합니다.

3. **노트북 집중도 유지**:
   - 하나의 노트북에는 하나의 개념만 담으십시오.
   - 명확한 설명과 주석을 포함하십시오.
   - 예상 출력값을 마크다운 셀로 포함하십시오.

4. **노트북 테스트**:
   - 처음부터 끝까지 에러 없이 실행되는지 확인하십시오.
   - 예시 API 호출 시 최소한의 토큰을 사용하십시오.
   - 에러 처리 로직을 포함하십시오.

### Git 워크플로우 (Git Workflow)

1. **기능 브랜치 생성**:
   ```bash
   git checkout -b <본인-이름>/<기능-설명>
   # 예시: git checkout -b alice/add-rag-example
   ```

2. **Conventional Commits 형식 사용**:
   ```bash
   # 형식: <타입>(<범위>): <제목>
   
   # 타입 예시:
   feat     # 새로운 기능
   fix      # 버그 수정
   docs     # 문서 작업
   style    # 포맷팅
   refactor # 코드 구조 재조정
   test     # 테스트 추가
   chore    # 유지보수
   ci       # CI/CD 변경
   
   # 예시:
   git commit -m "feat(skills): add text-to-sql notebook"
   git commit -m "fix(api): use environment variable for API key"
   git commit -m "docs(readme): update installation instructions"
   ```

3. **원자적 커밋 유지**:
   - 하나의 커밋에는 하나의 논리적 변경 사항만 담으십시오.
   - 명확하고 서술적인 메시지를 작성하십시오.
   - 관련 이슈가 있는 경우 참조하십시오.

4. **푸시 및 PR 생성**:
   ```bash
   git push -u origin your-branch-name
   gh pr create  # 또는 GitHub 웹 인터페이스 사용
   ```

### 풀 리퀘스트(PR) 가이드라인

1. **PR 제목**: Conventional Commit 형식을 따르십시오.
2. **설명**: 다음 내용을 포함하십시오:
   - 변경한 내용
   - 변경 이유
   - 테스트 방법
   - 관련 이슈 번호
3. **PR 집중도 유지**: 하나의 PR에는 하나의 기능/수정만 담으십시오.
4. **피드백 대응**: 리뷰 의견에 신속하게 대응하십시오.

## 테스트 (Testing)

### 로컬 테스트

검증 스위트를 실행하십시오:

```bash
# 모든 노트북 확인
uv run python scripts/validate_notebooks.py

# 모든 파일에 대해 pre-commit 실행
uv run pre-commit run --all-files
```

### CI/CD

GitHub Actions 워크플로우를 통해 다음 작업이 자동으로 수행됩니다:

- 노트북 구조 검증
- ruff를 이용한 코드 린트
- 노트북 실행 테스트 (메인테이너용)
- 링크 유효성 체크
- Claude의 코드 및 모델 사용 리뷰

외부 기여자의 경우 리소스 절약을 위해 API 테스트가 제한될 수 있습니다.

## 도움 받기 (Getting Help)

- **이슈**: [GitHub Issues](https://github.com/anthropics/claude-cookbooks/issues)
- **Discord**: [Anthropic Discord](https://www.anthropic.com/discord)

## 보안 (Security)

- API 키나 비밀 정보를 절대 커밋하지 마십시오.
- 민감한 데이터에는 환경 변수를 사용하십시오.
- 보안 이슈는 security@anthropic.com으로 비공개로 보고해 주십시오.

## 라이선스 (License)

기여함으로써 여러분의 기여물이 프로젝트와 동일한 라이선스(MIT License) 하에 제공됨에 동의하게 됩니다.