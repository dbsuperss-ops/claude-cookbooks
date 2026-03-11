# Promptfoo를 이용한 평가 (Evaluations with Promptfoo)

### 이 평가 스위트에 대한 참고 사항

1) 아래 지침을 반드시 따르십시오. 특히 필요한 패키지에 대한 사전 요구 사항을 확인하세요.

2) 전체 평가 스위트를 실행하려면 평소보다 높은 요율 제한(rate limit)이 필요할 수 있습니다. Promptfoo에서 일부 테스트만 실행하는 것을 고려해 보세요.

3) 모든 테스트가 즉시 통과하지는 않을 것입니다. 우리는 평가를 어느 정도 도전적으로 설계했습니다.

### 사전 요구 사항
Promptfoo를 사용하려면 시스템에 node.js와 npm이 설치되어 있어야 합니다. 자세한 내용은 [이 가이드](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)를 참조하십시오.

npm을 사용하여 promptfoo를 설치하거나 npx를 사용하여 직접 실행할 수 있습니다. 이 가이드에서는 npx를 사용합니다.

*참고: 이 예제에서는 `npx promptfoo@latest init`를 실행할 필요가 없습니다. 이 디렉토리에 이미 초기화된 `promptfooconfig.yaml` 파일이 있습니다.*

공식 문서는 [여기](https://www.promptfoo.dev/docs/getting-started)에서 확인하세요.

#### 참고 - 추가 의존성
이 예제에서는 커스텀 평가(custom_evals)가 제대로 작동하도록 다음 의존성을 설치해야 합니다.

`pip install nltk rouge-score`

### 시작하기

시작하려면 ANTHROPIC_API_KEY 환경 변수 또는 선택한 프로바이더에 필요한 다른 키를 설정하십시오. `export ANTHROPIC_API_KEY=YOUR_API_KEY`와 같이 설정할 수 있습니다.

그런 다음 `evaluation` 디렉토리로 `cd` 이동하여 `npx promptfoo@latest eval -c promptfooconfig.yaml --output ../data/results.csv`를 입력하십시오.

그 후 `npx promptfoo@latest view`를 실행하여 결과를 확인할 수 있습니다.

### 작동 방식

`promptfooconfig.yaml` 파일은 우리 평가 설정의 핵심입니다. 여기에는 다음과 같은 중요한 섹션들이 정의되어 있습니다.

**프롬프트 (Prompts):**
- 프롬프트는 `prompts.py` 파일에서 가져옵니다.
- 이 프롬프트들은 언어 모델 성능의 다양한 측면을 테스트하도록 설계되었습니다.

**프로바이더 (Providers):**
- 여기에서 다양한 Claude 버전과 설정을 구성합니다.
- 이를 통해 여러 모델을 테스트하거나 다양한 파라미터(예: 다른 온도 설정)로 테스트할 수 있습니다.

**테스트 (Tests):**
- 테스트 케이스는 이 파일에 직접 정의하거나, 이 예제처럼 `tests.yaml`에서 가져옵니다.
- 이 테스트들은 평가를 위한 입력값과 예상 출력값을 지정합니다.
- Promptfoo는 다양한 내장 테스트 유형을 제공하며(문서 참조), 직접 정의할 수도 있습니다. 우리는 3개의 커스텀 평가와 1개의 기본 평가(contains 메서드)를 사용합니다.
    - `bleu_eval.py`: 기계가 생성한 텍스트와 참조 텍스트 간의 유사도를 측정하는 BLEU(Bilingual Evaluation Understudy) 점수를 구현합니다.
    - `rouge_eval.py`: 참조 요약본과 비교하여 요약의 품질을 평가하는 ROUGE(Recall-Oriented Understudy for Gisting Evaluation) 점수를 구현합니다.
    - `llm_eval.py`: 일관성, 관련성 또는 사실적 정확성과 같은 생성된 텍스트의 다양한 측면을 평가하기 위해 언어 모델을 활용하는 커스텀 평가 지표를 포함합니다.

**출력 (Output):**
- 평가 결과의 형식과 위치를 지정합니다.
- Promptfoo는 다양한 출력 형식도 지원합니다!

### Python 바이너리 재정의

기본적으로 Promptfoo는 셸에서 `python`을 실행합니다. `python`이 적절한 실행 파일을 가리키고 있는지 확인하십시오.

Python 바이너리가 없으면 "python: command not found" 오류가 표시됩니다.

Python 바이너리를 재정의하려면 `PROMPTFOO_PYTHON` 환경 변수를 설정하십시오. 경로(예: `/path/to/python3.11`) 또는 PATH에 있는 실행 파일 이름(예: `python3.11`)으로 설정할 수 있습니다.
    