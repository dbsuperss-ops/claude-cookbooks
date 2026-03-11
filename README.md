# Claude 쿡북 (Claude Cookbooks)

Claude 쿡북은 개발자가 Claude를 사용하여 제품을 개발하는 데 도움이 되도록 설계된 코드와 가이드를 제공하며, 자신의 프로젝트에 쉽게 통합할 수 있는 복사 가능한 코드 스니펫을 제공합니다.

## 사전 요구 사항

이 쿡북의 예제를 최대한 활용하려면 Claude API 키가 필요합니다 ([여기](https://www.anthropic.com)에서 무료로 가입하세요).

코드 예제는 주로 Python으로 작성되었지만, 개념은 Claude API와의 상호 작용을 지원하는 모든 프로그래밍 언어에 적용할 수 있습니다.

Claude API를 처음 사용하신다면, [Claude API 기본 과정](https://github.com/anthropics/courses/tree/master/anthropic_api_fundamentals)에서 시작하여 탄탄한 기초를 다지는 것을 추천합니다.

## 더 알아보기

Claude 및 AI 비서에 대한 경험을 향상시키기 위한 더 많은 리소스를 찾고 계신가요? 다음 유용한 링크들을 확인해 보세요:

- [Anthropic 개발자 문서](https://docs.claude.com/claude/docs/guide-to-anthropics-prompt-engineering-resources)
- [Anthropic 지원 문서](https://support.anthropic.com)
- [Anthropic Discord 커뮤니티](https://www.anthropic.com/discord)

## 기여하기

Claude 쿡북은 개발자 커뮤니티의 기여로 번창합니다. 아이디어 제출, 오타 수정, 새로운 가이드 추가 또는 기존 가이드 개선 등 여러분의 의견을 소중하게 생각합니다. 기여를 통해 이 리소스가 모두에게 더욱 가치 있게 만들어질 수 있습니다.

노력의 중복을 피하기 위해 기여하기 전에 기존 Issue와 Pull Request를 검토해 주세요.

새로운 예제나 가이드에 대한 아이디어가 있다면 [이슈 페이지](https://github.com/anthropics/anthropic-cookbook/issues)에서 공유해 주세요.

## 레시피 목록

### 주요 기능 (Capabilities)
- [분류 (Classification)](https://github.com/anthropics/anthropic-cookbook/tree/main/capabilities/classification): Claude를 사용한 텍스트 및 데이터 분류 기술을 탐구합니다.
- [검색 증강 생성 (Retrieval Augmented Generation)](https://github.com/anthropics/anthropic-cookbook/tree/main/capabilities/retrieval_augmented_generation): 외부 지식을 사용하여 Claude의 응답을 향상시키는 방법을 배웁니다.
- [요약 (Summarization)](https://github.com/anthropics/anthropic-cookbook/tree/main/capabilities/summarization): Claude를 사용한 효과적인 텍스트 요약 기술을 알아봅니다.

### 도구 사용 및 통합 (Tool Use and Integration)
- [도구 사용 (Tool use)](https://github.com/anthropics/anthropic-cookbook/tree/main/tool_use): Claude를 외부 도구 및 기능과 통합하여 기능을 확장하는 방법을 배웁니다.
  - [고객 서비스 에이전트](https://github.com/anthropics/anthropic-cookbook/blob/main/tool_use/customer_service_agent.ipynb)
  - [계산기 통합](https://github.com/anthropics/anthropic-cookbook/blob/main/tool_use/calculator_tool.ipynb)
  - [SQL 쿼리](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/how_to_make_sql_queries.ipynb)

### 제3자 통합 (Third-Party Integrations)
- [검색 증강 생성 (Retrieval augmented generation)](https://github.com/anthropics/anthropic-cookbook/tree/main/third_party): 외부 데이터 소스로 Claude의 지식을 보완합니다.
  - [벡터 데이터베이스 (Pinecone)](https://github.com/anthropics/anthropic-cookbook/blob/main/third_party/Pinecone/rag_using_pinecone.ipynb)
  - [Wikipedia](https://github.com/anthropics/anthropic-cookbook/blob/main/third_party/Wikipedia/wikipedia-search-cookbook.ipynb/)
  - [웹 페이지](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/read_web_pages_with_haiku.ipynb)
- [Voyage AI를 이용한 임베딩](https://github.com/anthropics/anthropic-cookbook/blob/main/third_party/VoyageAI/how_to_create_embeddings.md)

### 멀티모달 기능 (Multimodal Capabilities)
- [Claude의 비전 기능 (Vision with Claude)](https://github.com/anthropics/anthropic-cookbook/tree/main/multimodal): 
  - [이미지 시작하기](https://github.com/anthropics/anthropic-cookbook/blob/main/multimodal/getting_started_with_vision.ipynb)
  - [비전 기능 모범 사례](https://github.com/anthropics/anthropic-cookbook/blob/main/multimodal/best_practices_for_vision.ipynb)
  - [차트 및 그래프 해석](https://github.com/anthropics/anthropic-cookbook/blob/main/multimodal/reading_charts_graphs_powerpoints.ipynb)
  - [양식에서 내용 추출](https://github.com/anthropics/anthropic-cookbook/blob/main/multimodal/how_to_transcribe_text.ipynb)
- [Claude로 이미지 생성](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/illustrated_responses.ipynb): 이미지 생성을 위해 Claude를 Stable Diffusion과 함께 사용합니다.

### 고급 기술 (Advanced Techniques)
- [서브 에이전트 (Sub-agents)](https://github.com/anthropics/anthropic-cookbook/blob/main/multimodal/using_sub_agents.ipynb): Haiku를 Opus와 결합하여 서브 에이전트로 사용하는 방법을 배웁니다.
- [Claude에 PDF 업로드](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/pdf_upload_summarization.ipynb): PDF를 파싱하여 텍스트로 Claude에게 전달합니다.
- [자동 평가 (Automated evaluations)](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/building_evals.ipynb): Claude를 사용하여 프롬프트 평가 프로세스를 자동화합니다.
- [JSON 모드 활성화](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/how_to_enable_json_mode.ipynb): Claude로부터 일관된 JSON 출력을 보장합니다.
- [중재 필터 만들기 (Create a moderation filter)](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/building_moderation_filter.ipynb): Claude를 사용하여 애플리케이션의 콘텐츠 중재 필터를 만듭니다.
- [프롬프트 캐싱 (Prompt caching)](https://github.com/anthropics/anthropic-cookbook/blob/main/misc/prompt_caching.ipynb): Claude의 효율적인 프롬프트 캐싱 기술을 배웁니다.

## 추가 리소스

- [AWS상의 Anthropic](https://github.com/aws-samples/anthropic-on-aws): AWS 인프라에서 Claude를 사용하는 예제와 솔루션을 탐색합니다.
- [AWS 샘플](https://github.com/aws-samples/): Claude와 함께 사용하기 위해 조정할 수 있는 AWS의 코드 샘플 모음입니다. 일부 샘플은 Claude에서 최적으로 작동하려면 수정이 필요할 수 있습니다.
