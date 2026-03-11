# Claude 기능 (Claude Capabilities)

Claude 쿡북의 기능(Capabilities) 섹션에 오신 것을 환영합니다! 이 디렉토리에는 Claude가 뛰어난 성능을 발휘하는 특정 기능들을 보여주는 가이드 모음이 포함되어 있습니다. 각 가이드는 특정 기능에 대한 심층적인 탐구를 제공하며, 잠재적인 사용 사례, 결과를 최적화하기 위한 프롬프트 엔지니어링 기술, 그리고 Claude의 성능을 평가하기 위한 접근 방식에 대해 논의합니다.

## 가이드 목록

- **[Claude를 이용한 분류 (Classification with Claude)](./classification/guide.ipynb)**: 특히 복잡한 비즈니스 규칙과 제한된 학습 데이터가 있는 시나리오에서 Claude가 어떻게 분류 작업을 혁신할 수 있는지 알아보세요. 이 가이드는 데이터 준비, 검색 증강 생성(RAG)을 활용한 프롬프트 엔지니어링, 테스트 및 평가 과정을 안내합니다.

- **[Claude를 이용한 검색 증강 생성 (Retrieval Augmented Generation with Claude)](./retrieval_augmented_generation/guide.ipynb)**: RAG를 사용하여 도메인 특화 지식으로 Claude의 기능을 향상시키는 방법을 배웁니다. 이 가이드는 RAG 시스템을 기초부터 구축하고 성능을 최적화하며 평가 스위트를 만드는 방법을 보여줍니다. 요약 인덱싱 및 재순위화(re-ranking)와 같은 기술이 질문 답변 작업에서 어떻게 정밀도, 재현율 및 전반적인 정확도를 크게 향상시킬 수 있는지 배우게 됩니다.

- **[Contextual Embeddings를 이용한 검색 증강 생성](./contextual-embeddings/guide.ipynb)**: RAG 시스템의 성능을 향상시키기 위한 새로운 기술을 사용하는 방법을 배웁니다. 기존 RAG에서는 효율적인 검색을 위해 문서를 일반적으로 작은 청크(chunk)로 나눕니다. 이 방식은 많은 애플리케이션에서 잘 작동하지만, 개별 청크에 충분한 문맥이 부족할 때 문제가 발생할 수 있습니다. Contextual Embeddings는 임베딩 전에 각 청크에 관련 문맥을 추가하여 이 문제를 해결합니다. 시맨틱 검색, BM25 검색 및 재순위화와 함께 Contextual Embeddings를 사용하여 성능을 높이는 방법을 배우게 됩니다.

- **[Claude를 이용한 요약 (Summarization with Claude)](./summarization/guide.ipynb)**: 여러 소스에서 정보를 요약하고 합성하는 Claude의 능력을 탐구합니다. 이 가이드는 멀티샷(multi-shot), 도메인 기반 및 청킹 방법을 포함한 다양한 요약 기술과 긴 콘텐츠 및 여러 문서를 처리하기 위한 전략을 다룹니다. 또한 기술, 주관성, 그리고 올바른 접근 방식 사이의 균형이 필요한 요약 평가 방법도 살펴봅니다.

- **[Claude를 이용한 Text-to-SQL (Text-to-SQL with Claude)](./text_to_sql/guide.ipynb)**: 이 가이드는 프롬프트 기술, 자기 개선(self-improvement) 및 RAG를 사용하여 자연어로부터 복잡한 SQL 쿼리를 생성하는 방법을 다룹니다. 또한 구문, 데이터 정확성, 행 수 등을 확인하는 에발(evals)을 통해 생성된 SQL 쿼리의 정확도를 평가하고 향상시키는 방법도 탐구합니다.

## 시작하기

이 가이드들을 시작하려면 원하는 가이드의 디렉토리로 이동하여 `guide.ipynb` 파일에 제공된 지침을 따르십시오. 각 가이드는 독립적으로 구성되어 있으며 예제와 실험을 재현하는 데 필요한 모든 코드, 데이터 및 평가 스크립트를 포함하고 있습니다.