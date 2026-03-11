# Promptfoo를 이용한 평가 (Evaluations with Promptfoo)

### 사전 요구 사항
Promptfoo를 사용하려면 시스템에 node.js와 npm이 설치되어 있어야 합니다. 자세한 내용은 [이 가이드](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)를 참조하십시오.

npm을 사용하여 promptfoo를 설치하거나 npx를 사용하여 직접 실행할 수 있습니다. 이 가이드에서는 npx를 사용합니다.

*참고: 이 예제에서는 `npx promptfoo@latest init`를 실행할 필요가 없습니다. 이 디렉토리에 이미 초기화된 `promptfooconfig.yaml` 파일이 있습니다.*

공식 문서는 [여기](https://www.promptfoo.dev/docs/getting-started)에서 확인하세요.

### 시작하기
평가는 `promptfooconfig.yaml` 파일에 의해 오케스트레이션됩니다. 이 파일에서 정의하는 섹션은 다음과 같습니다.

- **프롬프트 (Prompts)**
    - Promptfoo를 사용하면 다양한 형식으로 프롬프트를 가져올 수 있습니다. 자세한 내용은 [여기](https://www.promptfoo.dev/docs/configuration/parameters)를 참조하십시오.
    - 이 예제에서는 `guide.ipynb`와 동일한 `prompts.py` 파일에서 3개의 프롬프트를 로드합니다.
        - 함수들은 Claude API를 호출하는 대신 프롬프트를 반환한다는 점을 제외하고는 `guide.ipynb`에서 사용된 것과 동일합니다. Promptfoo가 API 호출 및 결과 저장을 처리합니다.
        - 프롬프트 함수에 대한 자세한 내용은 [여기](https://www.promptfoo.dev/docs/configuration/parameters#prompt-functions)를 참조하십시오. Python을 사용하면 RAG에 필요한 VectorDB 클래스를 재사용할 수 있으며, 이는 `vectordb.py`에 정의되어 있습니다.
- **프로바이더 (Providers)**
    - Promptfoo를 사용하면 다양한 플랫폼의 여러 LLM에 연결할 수 있습니다. 자세한 내용은 [여기](https://www.promptfoo.dev/docs/providers)를 참조하십시오. `guide.ipynb`에서는 기본 온도(temperature) 0.0의 Haiku를 사용했습니다. Promptfoo를 사용하여 다양한 온도 설정을 실험하고 우리 사용 사례에 최적인 선택을 찾을 수 있습니다.
- **테스트 (Tests)**
    - [`dataset.csv`](./dataset.csv)에 있는 `guide.ipynb`와 동일한 데이터를 사용합니다.
    - Promptfoo에는 다양한 내장 테스트가 있으며 [여기](https://www.promptfoo.dev/docs/configuration/expected-outputs/deterministic)에서 찾을 수 있습니다.
    - 이 예제에서는 각 행마다 평가 조건이 달라지는 경우 `dataset.csv`에 테스트를 정의하고, 모든 테스트 케이스에 일정한 조건인 경우 `promptfooconfig.yaml`에 테스트를 정의합니다. 자세한 내용은 [여기](https://www.promptfoo.dev/docs/configuration/parameters/#import-from-csv)를 참조하십시오.
- **변환 (Transform)**
    - `defaultTest` 섹션에서 변환 함수를 정의합니다. 이는 LLM 응답에서 테스트하고자 하는 특정 출력을 추출하는 Python 함수입니다.
- **출력 (Output)**
    - 출력 파일의 경로를 정의합니다. Promptfoo는 다양한 형식으로 결과를 출력할 수 있습니다. [여기](https://www.promptfoo.dev/docs/configuration/parameters/#output-file)를 참조하십시오. 또는 Promptfoo의 웹 UI를 사용할 수도 있습니다. [여기](https://www.promptfoo.dev/docs/usage/web-ui)를 참조하십시오.

### 평가 실행

Promptfoo를 시작하려면 터미널을 열고 이 디렉토리(`./evaluation`)로 이동하십시오.

평가를 실행하기 전에 다음과 같은 환경 변수를 정의해야 합니다.

`export ANTHROPIC_API_KEY=YOUR_API_KEY`  
`export VOYAGE_API_KEY=YOUR_API_KEY`

`evaluation` 디렉토리에서 다음 명령어를 실행하십시오.

`npx promptfoo@latest eval`

요청의 동시성(concurrency)을 높이려면(기본값 = 4) 다음 명령어를 실행하십시오.

`npx promptfoo@latest eval -j 25`

평가가 완료되면 터미널에 데이터셋의 각 행에 대한 결과가 출력됩니다.

이제 `guide.ipynb`로 돌아가 결과를 분석할 수 있습니다!
