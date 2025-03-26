# Day3. Evaluation, Function Call & Agent, MultiModal / Productivity

## 5. Evaluation

### MMLU (Massive Multitask Language Understanding)
- MMLU의 경우 데이터가 공개되어 있음
- 어떤 부분에 강점 또는 약점이 있는지 확인 가능
- 표준적인 평가 방식
- 내용이 방대해서 모델 발표 시 MMLU 결과가 없다면 어뷰징 및 성능에 의심할만함

### ROUGE (Recall-Oriented Understudy Gisting Evaluation)
- 텍스트 요약의 품질 평가 방법
- 기계 생성 요약과 사람의 요약을 비교하여 얼마나 유사한지 측정
- 정량 지표로 많이 쓰이긴 하나, 메인 지표로 삼기에는 적절하지 않음 (어뷰징 가능성)

### BLEU (Bilingual Evaluation Understudy)
- 기계 번역의 품질을 평가하는 방법
- 사람의 번역과 비교하여 측정
- 어뷰징 가능성이 높아 많이 쓰이진 않음
  - 가장 많은 단어만 번역해도 100점이 나옴
  - brevity penalty: 어뷰징 방지 목적으로 너무 짧을 경우 페널티

### Evaluation 문제점
- benchmark가 너무 다양하고, 점수가 높다고 해도 성능이 좋다는 보장이 없음
- 어뷰징이 심하고 모델 발전에 따라 인플레이션 발생
- 프롬프트 엔지니어링(결과가 좋지 않을 떄 재질문 등)이 반영되지 않음
- 사람이 일일이 모든 태스크에 대해 평가하는 건 불가능
- 결국 사람이 평가를 하는데, AI가 사람보다 더 뛰어나지고 있음

### LLM as a judge
- 평가를 LLM에게 맡기는 것
- 보통 작은 모델의 평가를 큰 모델에게 맡김

### FLASK
- LLM의 언어 능력을 역량별로 나눠서 평가
- 최근에 많이 쓰이는 중

### LMSYS Chatbot Arena
- 유저가 질문 시 익명의 랜덤 LLM이 답변하고, 유저에게 만족도를 받음 (대신 유저는 무료로 질문)
- 결과를 통해 리더보드를 만들어 제공
- 어뷰징이 적고 가장 신뢰하고 있는 평가지만, 사용자의 전문성이 떨어지므로 사용자들의 인기투표와 비슷

### Humanity's Last Exam
- 현재 가장 어려운 문제 중 하나
- 최고 정확도가 8.93%

### Self-Route
- Long Context와 RAG를 질문에 따라 나누는 작은 모델을 이용
- LC나 RAG만 썼을 때에 비해 비용도 적고 성능도 좋게 나옴

## 6. Function Call & Agent

### Function Call
- LLM이 외부 시스템을 이용하는 것
- LLM이 잘 배우지 못하는 것(계산 코딩 및 결과 확인 등)을 잘하게 하기 위함
- 기본 앱 또는 웹 LLM에는 여러 가지 function call을 탑재하고 있음
- code interpreter, file search 등 여러 기능이 있음
  - file search의 경우 RAG와 유사하나 범용적인 기능이므로, RAG 성능이 file search에 비해 성능 개선 여지가 있음
- LLM은 텍스트만 in, out하고, function call의 사용도 텍스트를 통해 진행
- LangChain 등과 같이 사용 가능

### AI Agent
- 유저의 요청 -> 플래닝 -> 메모리(롱텀, 숏텀), 툴(function call 등) -> agent 코어 답변
- 디지털 환경의 모든 인지적 행동은 모두 가능함
- assistant(일반적인 도움) -> agent(자기주도성)

## 7. MultiModal / Productivity
