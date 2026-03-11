# 임베딩 (Embeddings)
텍스트 임베딩은 텍스트 문자열의 수치적 표현으로, 부동 소수점 숫자의 벡터로 나타납니다. 두 텍스트 임베딩 사이의 거리(주로 코사인 유사도 사용)를 사용하여 두 텍스트 조각이 서로 얼마나 관련되어 있는지 측정할 수 있으며, 거리가 작을수록 관련성이 높음을 예측할 수 있습니다.

문자열의 유사성을 비교하거나 상호 거리별로 문자열을 클러스터링하는 것은 **검색**(RAG 아키텍처에서 널리 사용), **추천**, **이상 탐지**를 포함한 광범위한 애플리케이션을 가능하게 합니다.

## Anthropic에서 임베딩을 얻는 방법
Anthropic은 자체 임베딩 모델을 제공하지 않지만, 텍스트 임베딩의 우선 공급자로 [Voyage AI](https://www.voyageai.com/?ref=anthropic)와 파트너십을 맺었습니다. Voyage는 [최신 기술 수준(state of the art)](https://blog.voyageai.com/2023/10/29/voyage-embeddings/?ref=anthropic)의 임베딩 모델을 제작하며, 금융 및 의료와 같은 특정 산업 분야에 맞춤화된 모델과 귀사에 맞게 미세 조정(Fine-tuning)할 수 있는 모델도 제공합니다.

Voyage 임베딩을 사용하려면 먼저 [Voyage AI 웹사이트](https://dash.voyageai.com/?ref=anthropic)에서 가입하여 API 키를 발급받은 후, 편의를 위해 API 키를 환경 변수로 설정하십시오:

```bash
export VOYAGE_API_KEY="<your secret key>"
```

아래 설명된 대로 공식 [`voyageai` Python 패키지](https://github.com/voyage-ai/voyageai-python) 또는 HTTP 요청을 사용하여 임베딩을 얻을 수 있습니다.

### Voyage Python 패키지

다음 명령어를 사용하여 `voyageai` 패키지를 설치할 수 있습니다:

```bash
pip install -U voyageai
```

그 후, 클라이언트 객체를 생성하고 이를 사용하여 텍스트를 임베딩할 수 있습니다:

```python
import voyageai

vo = voyageai.Client()
# 이 코드는 자동으로 환경 변수 VOYAGE_API_KEY를 사용합니다.
# 대신 vo = voyageai.Client(api_key="<your secret key>") 형식을 사용할 수도 있습니다.

texts = ["샘플 텍스트 1", "샘플 텍스트 2"]

result = vo.embed(texts, model="voyage-2", input_type="document")
print(result.embeddings[0])
print(result.embeddings[1])
```

`result.embeddings`는 각각 1024개의 부동 소수점 숫자를 포함하는 두 개의 임베딩 벡터 목록이 됩니다. 위 코드를 실행하면 화면에 두 개의 임베딩이 출력됩니다:

```
[0.02012746, 0.01957859, ...]  # "샘플 텍스트 1"에 대한 임베딩
[0.01429677, 0.03077182, ...]  # "샘플 텍스트 2"에 대한 임베딩
```

임베딩을 생성할 때 `embed()` 함수에 몇 가지 다른 인수를 지정할 수 있습니다. 사양은 다음과 같습니다:

> `voyageai.Client.embed(texts : List[str], model : str = "voyage-2", input_type : Optional[str] = None, truncation : Optional[bool] = None)`

- **texts** (List[str]) - `["고양이를 좋아합니다", "개도 좋아합니다"]`와 같은 문자열 목록입니다. 현재 목록의 최대 길이는 128이며, 목록에 포함된 총 토큰 수는 `voyage-2`의 경우 최대 320K, `voyage-code-2`의 경우 120K입니다.
- **model** (str) - 모델의 이름입니다. 권장 옵션: `voyage-2` (기본값), `voyage-code-2`.
- **input_type** (str, 선택 사항, 기본값 `None`) - 입력 텍스트의 유형입니다. 기본값은 `None`입니다. 다른 옵션으로는 `query`, `document`가 있습니다.
    - input_type이 `None`으로 설정되면 입력 텍스트는 임베딩 모델에 의해 직접 인코딩됩니다. 반면 입력이 문서(document)이거나 쿼리(query)인 경우 사용자는 input_type을 각각 `document` 또는 `query`로 지정할 수 있습니다. 이 경우 Voyage는 입력 텍스트 앞에 특수한 프롬프트를 추가하여 임베딩 모델로 전냅니다.
    - 검색(retrieval/search) 사용 사례의 경우, 검색 품질을 높이기 위해 쿼리나 문서를 인코딩할 때 이 인수를 지정하는 것을 권장합니다. input_type 인수 유무에 관계없이 생성된 임베딩은 서로 호환됩니다.

- **truncation** (bool, 선택 사항, 기본값 `None`) - 입력 텍스트를 컨텍스트 길이에 맞게 자를지 여부입니다.
    - `True`인 경우, 너무 긴 입력 텍스트는 임베딩 모델에 의해 벡터화되기 전에 컨텍스트 길이에 맞게 잘립니다.
    - `False`인 경우, 텍스트가 컨텍스트 길이를 초과하면 에러가 발생합니다.
    - 지정되지 않은 경우(기본값 `None`), 텍스트가 컨텍스트 윈도우 길이를 약간 초과하면 모델에 보내기 전에 자릅니다. 상당히 초과하면 에러가 발생합니다.

### Voyage HTTP API

Voyage HTTP API를 요청하여 임베딩을 얻을 수도 있습니다. 예를 들어, 터미널에서 `curl` 명령어를 통해 HTTP 요청을 보낼 수 있습니다:

```bash
curl https://api.voyageai.com/v1/embeddings \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $VOYAGE_API_KEY" \
  -d '{
    "input": ["샘플 텍스트 1", "샘플 텍스트 2"],
    "model": "voyage-2"
  }'
```

받게 될 응답은 임베딩과 토큰 사용량이 포함된 JSON 객체입니다:

```bash
{
  "object": "list",
  "data": [
    {
      "embedding": [0.02012746, 0.01957859, ...],
      "index": 0
    },
    {
      "embedding": [0.01429677, 0.03077182, ...],
      "index": 1
    }
  ],
  "model": "voyage-2",
  "usage": {
    "total_tokens": 10
  }
}
```

Voyage AI의 임베딩 엔드포인트는 `https://api.voyageai.com/v1/embeddings` (POST)입니다. 요청 헤더에는 API 키가 포함되어야 합니다. 요청 본문은 다음 인수를 포함하는 JSON 객체입니다:

- **input** (str, List[str]) - 단일 텍스트 문자열 또는 문자열 목록입니다.
- **model** (str) - 모델의 이름입니다.
- **input_type** (str, 선택 사항) - 입력 텍스트의 유형입니다 (`query`, `document`).
- **truncation** (bool, 선택 사항) - 텍스트 절단 여부입니다.
- **encoding_format** (str, 선택 사항) - 임베딩이 인코딩되는 형식입니다.
    - 지정되지 않은 경우(기본값 `None`): 부동 소수점 숫자 목록으로 표현됩니다.
    - `"base64"`: [Base64](https://docs.python.org/3/library/base64.html) 인코딩으로 압축됩니다.

### AWS Marketplace
Voyage 임베딩은 [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=seller-snt4gb6fd7ljg)에서도 사용할 수 있습니다.

## 사용 가능한 모델

Voyage는 다음 임베딩 모델 사용을 권장합니다:

| 모델 | 컨텍스트 길이 | 임베딩 차원 | 설명 |
| --- | --- | --- | --- |
| `voyage-2` | 4000 | 1024 | 최상의 검색 품질을 갖춘 최신 범용 임베딩 모델입니다. |
| `voyage-code-2` | 16000 | 1536 | 코드 검색에 최적화되어 있으며(타 모델 대비 17% 우수), 일반 용도의 말뭉치에서도 세계 최고 수준(SoTA)입니다. |

`voyage-2`는 여러 도메인에서 최첨단 성능을 달성하면서도 높은 효율성을 유지하며, `voyage-code-2`는 코드 애플리케이션에 최적화되어 긴 컨텍스트 길이를 제공합니다.

Voyage는 더 발전되고 특화된 모델을 개발 중이며, 귀사를 위해 임베딩을 미세 조정할 수도 있습니다. 개별 데이터에 대한 미세 조정이나 시험 사용을 원하시면 [contact@voyageai.com](mailto:contact@voyageai.com)으로 문의하십시오!

## 예제
임베딩을 얻는 방법을 알았으니, 간단한 예제를 살펴보겠습니다. 하위 6개의 문서로 구성된 작은 말뭉치가 있다고 가정해 봅시다.

```python
documents = [
    "지중해 식단은 생선, 올리브 오일, 채소를 강조하며 만성 질환을 줄이는 것으로 여겨집니다.",
    "식물의 광합성은 빛 에너지를 포도당으로 전환하고 필수적인 산소를 생산합니다.",
    "라디오에서 스마트폰에 이르는 20세기 혁신은 전자 기술의 발전에 집중되었습니다.",
    "강은 물, 관개 및 수생 생물의 서식지를 제공하며 생태계에 필수적입니다.",
    "Apple의 4분기 실적 및 사업 업데이트를 논의하기 위한 컨퍼런스 콜은 2023년 11월 2일 목요일 오후 2시(PT) / 오후 5시(ET)로 예정되어 있습니다.",
    "햄릿과 한여름 밤의 꿈과 같은 셰익스피어의 작품은 문학계에서 영원히 남을 것입니다."
]
```

먼저 Voyage를 사용하여 각 문서를 임베딩 벡터로 변환합니다.

```python
import voyageai

vo = voyageai.Client()

# 문서 임베딩
doc_embds = vo.embed(
    documents, model="voyage-2", input_type="document"
).embeddings
```

임베딩을 통해 벡터 공간에서 시맨틱 검색/조회를 수행할 수 있습니다. 다음 쿼리가 주어졌을 때,

```python
query = "Apple의 컨퍼런스 콜은 언제인가요?"
```

이를 임베딩으로 변환하고, 임베딩 공간에서의 거리를 기반으로 가장 관련성 높은 문서를 찾기 위해 최근접 이웃(Nearest Neighbor) 검색을 실시합니다.

```python
import numpy as np

# 쿼리 임베딩
query_embd = vo.embed(
    [query], model="voyage-2", input_type="query"
).embeddings[0]

# 유사도 계산
# Voyage 임베딩은 길이가 1로 정규화되므로 내적(dot-product)과 코사인 유사도가 동일합니다.
similarities = np.dot(doc_embds, query_embd)

retrieved_id = np.argmax(similarities)
print(documents[retrieved_id])
```

결과는 쿼리와 가장 관련이 있는 5번째 문서가 될 것입니다.

벡터 데이터베이스를 포함하여 임베딩으로 RAG를 수행하는 방법에 대한 자세한 가이드는 [RAG 쿡북](https://github.com/anthropics/anthropic-cookbook/blob/main/third_party/Pinecone/rag_using_pinecone.ipynb)을 확인하십시오.

## 자주 묻는 질문 (FAQ)
### 두 임베딩 벡터 사이의 거리는 어떻게 계산하나요?
코사인 유사도가 널리 쓰이지만 대부분의 거리 함수도 잘 작동합니다. Voyage 임베딩은 길이가 1로 정규화되어 있으므로 코사인 유사도는 두 벡터 사이의 내적과 본질적으로 동일합니다.

### 임베딩 하기 전에 문자열의 토큰 수를 셀 수 있나요?
네! 다음 코드로 가능합니다.

```python
import voyageai

vo = voyageai.Client()
total_tokens = vo.count_tokens(["샘플 텍스트"])
```

## 가격
가격 정보는 Voyage 웹사이트의 [가격 페이지](https://docs.voyageai.com/pricing/?ref=anthropic)에서 확인하실 수 있습니다.
    
