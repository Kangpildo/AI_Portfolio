# 실습 Overview: VisionModel_CvT(Convolutional Vision Transformer)

## 1. 실습 목적
- Convolutional Vision Transformer (CvT) 기반의 이미지 분류 모델 구조 이해 및 실습
- Hugging Face Transformers 라이브러리를 활용하여 Pre-trained 모델을 로드하고, FashionMNIST 데이터셋에 맞게 Fine-tuning(미세 조정)하는 전체 과정 습득
- 흑백 이미지(1채널)를 컬러 모델(3채널) 입력에 맞게 변환하는 전처리 과정 학습

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 설치**
  - 모델 학습 및 평가에 필요한 핵심 라이브러리 (transformers, peft, evaluate, accelerate) 설치 및 환경 구성
- **데이터셋 준비 및 전처리 (Data Preparation)**
  - FashionMNIST 데이터셋 로드: torchvision.datasets를 통해 학습 및 테스트 데이터 다운로드
  - Efficient Learning을 위한 Subsampling: 전체 데이터 대신 학습용 1,000개, 테스트용 100개의 데이터를 클래스별로 균등하게 추출하여 Subset 데이터셋 생성 (실습 효율성 증대)
- **CvT 모델 로드 및 이미지 변환 (Model & Transformation)**
  - Pre-trained 모델 로드: microsoft/cvt-21 사전 학습 모델을 불러오고, 분류할 클래스 수(10개)에 맞춰 헤드 조정
  - 이미지 차원 변환: FashionMNIST(Grayscale, 1ch)를 CvT 입력(RGB, 3ch)에 맞추기 위해 transforms.Lambda를 사용하여 채널을 3배로 복사하는 전처리 로직 구현
- **모델 학습 및 평가 (Training & Evaluation)**
  - Hugging Face Trainer 활용: TrainingArguments를 설정하여 Epoch, Batch Size, Learning Rate 등을 정의하고 학습 진행
  - 평가 지표 정의: evaluate 라이브러리의 F1 score(macro average)를 사용하여 모델 성능 평가
  - 결과 시각화: 학습된 모델로 테스트 셋을 예측(Inference)하고, Confusion Matrix를 생성하여 클래스별 예측 정확도 시각화 


## 3. 결과 및 기대 효과
- Transformer 기반 Vision 모델의 활용 능력 배양: CNN과 Transformer가 결합된 CvT 모델의 작동 방식 이해
- Custom Data 적용 능력 향상: 입력 채널이 다른 데이터셋을 사전 학습된 모델에 맞게 전처리하는 실무적인 노하우 습득
- 모델 성능 분석 능력: Confusion Matrix를 통해 모델이 어떤 클래스를 혼동하는지 시각적으로 분석하는 능력 함양

## 4. 참고 및 확장
- 데이터셋 확장: 실습에서는 일부 데이터만 사용했으나, 전체 데이터셋을 활용하여 성능 향상 실험 가능
- Hyperparameter Tuning: Learning rate, Batch size, Epoch 등을 조절하여 최적의 성능 탐색
- 다른 모델과의 비교: ViT, ResNet 등 다른 아키텍처와 성능 및 학습 속도 비교 실험

