# 실습 Overview: VisionModel_SwinT

## 1. 실습 목적
- Swin Transformer (Shifted Window Transformer) 기반의 이미지 분류 모델 구조 이해 및 실습
- Hugging Face Transformers 라이브러리를 활용하여 계층적(Hierarchical) Vision Transformer인 SwinT 모델을 로드하고, FashionMNIST 데이터셋에 맞게 Fine-tuning(미세 조정)하는 전체 과정 습득
- Window Attention 및 Shifted Window 메커니즘을 통해 이미지의 지역적 특징을 효과적으로 학습하는 원리 이해

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 설치**
  - 모델 학습 및 평가에 필요한 핵심 라이브러리 (transformers, peft, evaluate, accelerate) 설치 및 환경 구성
- **데이터셋 준비 및 전처리 (Data Preparation)**
  - FashionMNIST 데이터셋 로드: torchvision.datasets를 통해 학습 및 테스트 데이터 다운로드
  - Efficient Learning을 위한 Subsampling: 전체 데이터 대신 학습용 1,000개, 테스트용 100개의 데이터를 클래스별로 균등하게 추출하여 Subset 데이터셋 생성 (실습 효율성 증대)
- **SwinT 모델 로드 및 이미지 변환 (Model & Transformation)**
  - Pre-trained 모델 로드: microsoft/swin-tiny-patch4-window7-224 사전 학습 모델을 불러오고, 분류할 클래스 수(10개)에 맞춰 헤드 조정
  - 이미지 차원 변환: FashionMNIST(Grayscale, 1ch)를 SwinT 입력(RGB, 3ch)에 맞추기 위해 transforms.Lambda를 사용하여 채널을 3배로 복사하고, 모델이 요구하는 해상도(224x224)로 리사이징하는 전처리 로직 구현
- **모델 학습 및 평가 (Training & Evaluation)**
  - Hugging Face Trainer 활용: TrainingArguments를 설정하여 Epoch, Batch Size, Learning Rate 등을 정의하고 학습 진행
  - 평가 지표 정의: evaluate 라이브러리의 F1 score(macro average)를 사용하여 모델 성능 평가
  - 결과 시각화: 학습된 모델로 테스트 셋을 예측(Inference)하고, Confusion Matrix를 생성하여 클래스별 예측 정확도 시각화

## 3. 결과 및 기대 효과
- Hierarchical Vision Transformer 활용 능력 배양: 기존 ViT와 달리 Window 기반의 Attention을 수행하는 Swin Transformer의 작동 방식과 파이프라인 이해
- Custom Data 적용 능력 향상: 입력 해상도(224x224)와 채널 수(3ch)가 고정된 사전 학습 모델에 맞게 데이터셋을 변환(Resize, Channel Expansion)하는 실무적인 노하우 습득
- 모델 성능 분석 능력: Confusion Matrix를 통해 모델이 어떤 의류 클래스(예: T-shirt/Top vs Shirt)를 혼동하는지 시각적으로 분석하는 능력 함양

## 4. 참고 및 확장
- 데이터셋 확장: 실습에서는 일부 데이터만 사용했으나, 전체 데이터셋을 활용하여 성능 향상 실험 가능
- Hyperparameter Tuning: Learning rate, Batch size, Epoch 등을 조절하여 최적의 성능 탐색
- 다른 모델과의 비교: ViT, CvT 등 다른 Transformer 계열 모델과 SwinT의 성능 및 학습 속도 비교 실험