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