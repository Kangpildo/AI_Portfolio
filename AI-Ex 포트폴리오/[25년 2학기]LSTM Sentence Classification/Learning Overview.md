# 실습 Overview: LSTM Sentence Classification

## 1. 실습 목적
- LSTM 모델 구현: PyTorch를 활용하여 문장 분류를 위한 LSTM(Long Short-Term Memory) 기반의 신경망 모델을 구현함.
- 한국어 텍스트 처리: NSMC(Naver Sentiment Movie Corpus) 데이터셋을 활용하여 한국어 영화 리뷰의 감정(긍정/부정)을 분류하는 전체 파이프라인을 실습함.

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 설치**
  - 한국어 말뭉치 로드를 위한 Korpora 및 형태소 분석을 위한 konlpy 라이브러리 설치 및 환경 구성.
- **데이터셋 준비 및 전처리 (Data Preparation)**
  - 데이터 로드: Korpora를 통해 NSMC 데이터를 다운로드하고 학습 데이터(90%)와 테스트 데이터(10%)로 분할.
  - 토큰화 및 단어장 구축: Okt 형태소 분석기를 사용하여 문장을 토큰화하고, 빈도수 상위 5,000개 단어로 어휘 사전(Vocabulary) 구축 및 특수 토큰(<pad>, <unk>) 처리.
  - 패딩(Padding): 가변 길이의 문장을 처리하기 위해 최대 길이를 32로 설정하고 패딩을 적용하여 고정 길이의 텐서로 변환.
- **모델 구현 (Model Implementation)**
  - SentenceClassifier 정의: 임베딩 층(Embedding), 양방향(Bidirectional) LSTM 층(2 Layer), 드롭아웃(Dropout), 그리고 최종 분류를 위한 선형 층(Linear)으로 구성된 클래스 정의.
  - 하이퍼파라미터 설정: 임베딩 차원(128), 은닉층 차원(64), 배치 크기(16), 학습률(0.001) 등 학습에 필요한 주요 파라미터 설정.
- **학습 및 평가 (Training & Evaluation)**
  - 학습 루프: BCEWithLogitsLoss 손실 함수와 RMSprop 옵티마이저를 사용하여 5 Epoch 동안 모델 학습 진행.
  - 성능 평가: 매 Epoch마다 테스트 데이터셋을 통해 검증 손실(Val Loss)과 정확도(Val Accuracy)를 측정하고 출력.

## 3. 결과 및 기대 효과
- 분류 성능 확인: 학습이 진행됨에 따라 정확도가 상승하여, 최종적으로 약 82.46%의 검증 정확도를 달성함.
- 임베딩 벡터 확인: 학습된 모델의 임베딩 층에서 특정 단어('보고싶다')에 대한 벡터 값을 추출하여, 단어가 밀집 벡터(Dense Vector)로 표현되는 방식을 이해함.
- 시퀀스 데이터 처리: 텍스트와 같은 시퀀스 데이터를 처리하는 데 있어 순환 신경망(RNN/LSTM)의 구조와 데이터 흐름을 명확히 이해함.

## 4. 참고 및 확장
- 모델 확장: GRU(Gated Recurrent Unit)나 Transformer 기반의 모델(BERT 등)을 적용하여 LSTM과의 성능 및 학습 속도 비교 실험.
- 전처리 고도화: 불용어(Stopwords) 제거, 사전 학습된 임베딩(Pre-trained Embedding) 사용 등을 통해 모델 성능 추가 개선 도모.