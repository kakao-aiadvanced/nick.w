# Day2. RAG, Fine Tuning, Evaluation

## 3. RAG (Retrieval Augmented Generation)
일종의 프롬프트 엔지니어링

### RAG 사용 이유
1. Enhanced Accuracy
2. Contextual Relevance
3. Scalability
4. Private Data

### Vector Store
- RAG에서 사용하는 저장소 역할
- 여러 종류의 문서(HTML, pdf 등)를 잘게 쪼개고 임베딩 후 저장
- 성능을 높이려면 파인 튜닝 시 특정 분야에서 사용하는 용어들에 대한 임베딩이 필요함

### LangChain
- 여러 종류의 파일에 맞는 로더를 제공하는 라이브러리

### Splitter
- 동일하게 여러 종류의 파일별 splitter가 있음
- 정답이 있는 건 아니지만 오답은 있음
- 태스크와 데이터의 특성을 기준으로 고려

### Chunk size
- 스플릿 후 나오는 크기
- 모든 케이스에 맞는 방법은 없지만, 서비스 허용 범위에서 좀 더 크게 일단 진행해보기

### Embedding model
- 일반적으로 OpenAI 모델 쓰는 것 추천

### Vector Store with Other Repository
- 벡터 스토어와 함께 ES, RDB 등을 같이 사용 가능
- 10 이상 50 이하 같은 명시적인 조건일 경우 벡터 유사성보다는 SQL을 통해 얻는 게 유리

### RAG Adanced

#### Query translation
- query를 retrieval하기 좋게 만드는 것

#### multi query 
- 비슷한 키워드로 약간 다르게 만들어 여러 번 쿼리를 보내고 결과를 취합 

#### RAG fusion
- 데이터의 랭크를 매기는 것
  - 보통 첫번쨰, 마지막이 정확도가 높으므로 첫번째에는 제일 관련있는 데이터를, 중간에는 제일 관련 적은 데이터가 배치되도록 랭킹

#### decomposition
- 분할 정복

#### direct routing
- 적합한 데이터 소스로 쿼리를 보내도록 하는 것 (ex. 유저 정보 = 유저 DB 보도록 지시)

#### semantic routing
- 사전에 형식화된 프롬프트를 여러 개 준비하고, 쿼리에 따라 적합한 프롬프트를 골라서 사용

#### query structuring
- 메타데이터를 기준으로 청크를 선별 (주로 비디오의 제목 등)

#### indexing
- RAPTOR(Recursive Abstractive Processing for Tree Organized Retrieval)

#### Re-rank
- Cross Encoder 사용

#### Corrective RAG
- 스스로 행동을 평가하고 수정하도록

#### Retrieval method
- 키워드 서치일 경우 주로 BM25를 사용
- hybrid search = keyword search + semantic search
- HyDE(Hypothetical Document Embeddings)
  - LLM이 가상의 답변을 만든 이후 실제 검색 및 답변

### RAG Evaluation
- Precision: 전체 시도 중 정답의 수 비율
- Recall: 전체 정답 중 찾은 정답의 수 비율
- RAGAS: RAG 평가 프레임워크

## 4. Fine Tuning
- 특정 태스크에 대해 특정 데이터셋을 추가로 학습시켜 해당 태스크에 대한 성능을 높이는 것
- 반면에 general 태스크에서는 성능이 떨어짐
- 모델의 사고 방식 자체를 바꾸는 것

### Fine Tuning vs Prompt engineering
- 파인 튜닝은 파라미터를 바꾸고, 프롬프트 엔지니어링은 바꾸지 않음
  - 프롬프트가 길어져 사용 토큰 증가
- 성능 향상의 폭이 파인 튜닝이 더 큼
- many-shot(대량의 예시) 약 8천 개까지도 성능이 올라가므로, 파인 튜닝 전 many-shot을 수행해보고 이후에 고려하기
  - many-shot에 대한 가능성의 예시가 있다면 이 쪽으로 fine tuning

### Fine Tuning vs RAG
- 성능은 둘 다 하는 게 더 좋음
- RAG는 참고해서 답, Fine Tuning은 정보의 업데이트 후 답
- 둘 중 어느 것이 더 성능 향상이 좋은지는 매번 다름

### Transfer learning
- 마지막 레이어 한 개만 튜닝
  - 내가 알고 있는 여러 지식들 중 몇개를 하나로 링크하여 새로운 지식을 쌓는 방식

### LoRA (Low Rank Adaptation)
- low rank: 행렬의 행과 열 중 작은 사이즈로 변환
- 튜닝해야 할 데이터가 작아짐
- 풀 튜닝한 것보다 성능이 더 높아질 수 있음 (대부분 fine tuning 시 사용 중)
- QLoRA (Quantized)
  - LoRA 후 양자화하여 더 작게
- 최근에는 DoRA라는 것도 나옴
  - 이외 여러가지가 나오고 있지만 매일 팔로우하지 말고, 널리 쓰이고 이미 검증된 사용하기 좋은 기술을 쓰

### Fine Tuning - Supervised / Reinforcement Learning
- 최근에는 휴먼 피드백보다 AI 피드백을 사용
- PPO(Proximal Preference Optimization): 리워드 모델을 통해 리워드를 제공하고 학습
- DPO(Direct Preference Optimization): 사람이 직접 리워드?
- GRPO(Guided Reward Policy Optimization): KL 다이버전스를 통해 사람의 산포를 모델의 산포와 비교하면서 흉내내도록 학습

### Dataset
- fine tuning의 가장 큰 비용은 좋은 데이터 준비하기
- high quality data: 더 배우기 쉬운 데이터(자세한 설명 등)

### OpenAI Fine Tuning Tool
- OpenAI에서 몇개의 예시만으로 파인 튜닝 가능
- 일단 멀티샷으로 테스트 후 좋아진다면 파인 튜닝 진행하기