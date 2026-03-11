# Claude 쿡북 기여 가이드 (Contributing to Claude Cookbooks)

Claude 쿡북에 관심을 가져주셔서 감사합니다! 이 가이드는 여러분이 개발을 시작하고 기여 내용이 품질 표준을 충족하도록 돕기 위해 작성되었습니다.

## 개발 환경 설정

### 사전 요구 사항

- Python 3.11 이상
- [uv](https://docs.astral.sh/uv/) 패키지 관리자 (권장) 또는 pip

### 빠른 시작

1. **uv 설치** (권장 패키지 관리자):
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
   # .env 파일을 수정하여 Claude API 키를 추가하세요.
   ```

## 품질 표준

이 레포지토리는 코드 품질을 유지하기 위해 다음과 같은 자동화 도구를 사용합니다.

### 노트북 검증 스택 (Notebook Validation Stack)

- **[nbconvert](https://nbconvert.readthedocs.io/)**: 테스트를 위한 노트북 실행
- **[ruff](https://docs.astral.sh/ruff/)**: 네이티브 Jupyter 지원 기능을 갖춘 빠른 Python 린터 및 포맷터
- **Claude AI 리뷰**: Claude를 사용한 지능형 코드 리뷰

**참고**: 노트북 출력 결과물은 사용자에게 예상 결과를 보여주기 위해 의도적으로 이 레포지토리에 유지됩니다.

### Claude Code 슬래시 명령어

이 레포지토리에는 Claude Code(로컬 개발용)와 GitHub Actions CI 모두에서 작동하는 슬래시 명령어가 포함되어 있습니다. Claude Code로 이 레포지토리에서 작업할 때 이러한 명령어를 자동으로 사용할 수 있습니다.

**사용 가능한 명령어**:
- `/link-review` - 마크다운 및 노트북의 링크 유효성 검사
- `/model-check` - Claude 모델 사용이 최신인지 확인
- `/notebook-review` - 종합적인 노트북 품질 체크

**Claude Code에서의 사용법**:
```bash
# CI가 실행할 것과 동일한 검증을 실행합니다.
/notebook-review skills/my-notebook.ipynb
/model-check
/link-review README.md
```

이 명령어들은 CI 파이프라인과 정확히 동일한 검증 로직을 사용하므로, 코드를 푸시하기 전에 문제를 파악하는 데 도움이 됩니다. 명령어 정의는 로컬 및 CI 용도 모두를 위해 `.claude/commands/`에 저장되어 있습니다.

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

### Pre-commit 훅

코드 품질을 보장하기 위해 각 커밋 전에 Pre-commit 훅이 자동으로 실행됩니다.

- ruff를 사용하여 코드 포맷팅
- 노트북 구조 검증

훅 실행에 실패하면 문제를 수정한 후 다시 커밋을 시도하세요.

## 기여 가이드라인

### 노트북 작성 모범 사례

1. **API 키에 환경 변수 사용**:
   ```python
   import os
   api_key = os.environ.get("ANTHROPIC_API_KEY")
   ```

2. **최신 Claude 모델 사용**:
   - 가용할 경우 유지보수가 용이하도록 모델 에일리어스(Alias)를 사용하세요.
   - 최신 Haiku 모델: `claude-haiku-4-5` (Haiku 4.5)
   - 현재 모델 목록 확인: https://docs.claude.com/en/docs/about-claude/models/overview
   - Claude가 PR 리뷰 시 모델 사용의 적절성을 자동으로 검증합니다.

3. **노트북의 집중도 유지**:
   - 노트북 하나당 하나의 개념만 다룹니다.
   - 명확한 설명과 주석을 포함하세요.
   - 예상 출력 결과를 마크다운 셀로 포함하세요.

4. **노트북 테스트**:
   - 처음부터 끝까지 오류 없이 실행되는지 확인하세요.
   - 예제 API 호출 시 최소한의 토큰을 사용하세요.
   - 에러 처리를 포함하세요.

### Git 워크플로우

1. **기능 브랜치 생성**:
   ```bash
   git checkout -b <이름>/<기능-설명>
   # 예: git checkout -b alice/add-rag-example
   ```

2. **Conventional Commits 사용**:
   ```bash
   # 형식: <type>(<scope>): <subject>
   
   # 유형(Type):
   feat     # 새로운 기능
   fix      # 버그 수정
   docs     # 문서 수정
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

3. **원자적(Atomic) 커밋 유지**:
   - 커밋 하나당 하나의 논리적 변경 사항을 담으세요.
   - 명확하고 구체적인 메시지를 작성하세요.
   - 해당되는 경우 이슈 번호를 참조하세요.

4. **푸시 및 PR 생성**:
   ```bash
   git push -u origin your-branch-name
   gh pr create  # 또는 GitHub 웹 인터페이스 사용
   ```

### 풀 리퀘스트(PR) 가이드라인

1. **PR 제목**: Conventional Commit 형식을 사용하세요.
2. **설명**: 다음 내용을 포함하세요:
   - 변경한 내용
   - 변경한 이유
   - 테스트 방법
   - 관련 이슈 번호
3. **PR의 집중도 유지**: PR 하나당 하나의 기능/수정만 다룹니다.
4. **피드백 대응**: 리뷰 의견에 신속하게 대응하세요.

## 테스트

### 로컬 테스트

검증 스위트를 실행합니다.

```bash
# 모든 노트북 체크
uv run python scripts/validate_notebooks.py

# 모든 파일에 대해 pre-commit 실행
uv run pre-commit run --all-files
```

### CI/CD

GitHub Actions 워크플로우가 자동으로 다음을 수행합니다.

- 노트북 구조 검증
- ruff를 이용한 코드 린팅
- 노트북 실행 테스트 (메인테이너용)
- 링크 확인
- Claude의 코드 및 모델 사용 리뷰

외부 기여자의 경우 리소스 절약을 위해 API 테스트가 제한적으로 수행될 수 있습니다.

## 도움 받기

- **이슈**: [GitHub Issues](https://github.com/anthropics/anthropic-cookbook/issues)
- **토론**: [GitHub Discussions](https://github.com/anthropics/anthropic-cookbook/discussions)
- **Discord**: [Anthropic Discord](https://www.anthropic.com/discord)

## 보안

- API 키나 시크릿을 절대 커밋하지 마세요.
- 민감한 데이터에는 환경 변수를 사용하세요.
- 보안 문제는 security@anthropic.com으로 비공개로 보고해 주세요.

## 라이선스

기여함으로써 귀하의 기여 내용이 프로젝트와 동일한 라이선스(MIT License)에 따라 라이선스가 부여됨에 동의하게 됩니다.