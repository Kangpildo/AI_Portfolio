# 실습 Overview: VisionModel_Faster_R-CNN

## 1. 실습 목적
- Faster R-CNN (Region-based Convolutional Neural Network) 기반의 객체 탐지(Object Detection) 모델 구조 이해 및 실습
- PyTorch TorchVision 라이브러리를 활용하여 Pre-trained Faster R-CNN 모델을 로드하고, COCO 포맷의 사용자 데이터셋(Custom Dataset)에 맞게 Fine-tuning(미세 조정)하는 전체 과정 습득
- Object Detection 파이프라인 구축: 데이터 로딩, 모델 학습, 추론(Inference), 평가(mAP)까지의 전 과정 경험

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 로드**
  - torch, torchvision, pycocotools 등 객체 탐지에 필수적인 라이브러리 로드 및 Google Drive 마운트 
- **데이터셋 준비 (Custom COCO Dataset)**
  - COCODataset 클래스 구현: torch.utils.data.Dataset을 상속받아 COCO 포맷의 어노테이션 파일을 파싱하고 이미지와 바운딩 박스(Bbox) 정보를 로드하는 커스텀 데이터셋 클래스 정의 
  - 데이터 로더 설정: 학습(Train) 및 검증(Test) 데이터셋을 위한 DataLoader 생성 및 배치 처리용 collate_fn 구현 
- **Faster R-CNN 모델 구성 (Model Configuration)**
  - Backbone 네트워크 설정: VGG16 (VGG16_Weights.IMAGENET1K_V1)을 백본으로 사용하고, Feature Map 추출을 위해 레이어 수정 
  - Anchor Generator 정의: 다양한 크기(32~512)와 비율(0.5, 1.0, 2.0)을 가진 앵커 박스 생성기 설정 
  - RoI Pooler 설정: MultiScaleRoIAlign을 사용하여 Feature Map에서 관심 영역(RoI)을 고정된 크기(7x7)로 추출 
  - 모델 조립: 위 구성 요소들을 FasterRCNN 클래스에 결합하여 최종 탐지 모델 생성 
- **모델 학습 (Training)*8
  - Optimizer & Scheduler: SGD Optimizer (Momentum, Weight Decay 적용) 및 StepLR 스케줄러 설정 
  - 학습 루프 구현: 5 Epoch 동안 학습을 진행하며, 매 배치마다 Loss를 계산하고 역전파(Backpropagation) 수행. 학습 진행 상황(Cost) 출력 
- **추론 및 시각화 (Inference & Visualization)**
  - 시각화 함수 정의: 이미지 위에 예측된 바운딩 박스, 클래스 이름, 신뢰도 점수(Score)를 그리는 draw_bbox 함수 구현 
  - 결과 비교: 모델의 예측 결과(Red Box)와 정답 데이터(Ground Truth, Blue Box)를 함께 시각화하여 성능을 직관적으로 확인 
- **성능 평가 (Evaluation)**
  - COCO Evaluator 활용: pycocotools를 사용하여 전체 테스트 데이터셋에 대한 모델의 예측 결과를 COCO 포맷으로 변환하고, 표준 평가지표인 mAP(mean Average Precision) 등을 계산하여 정량적 성능 평가 수행

## 3. 결과 및 기대 효과
- Object Detection 원리 체득: Region Proposal Network(RPN)와 Fast R-CNN Detector가 결합된 2-Stage 탐지 모델의 작동 방식 이해
- Custom Dataset 활용 능력: COCO 포맷의 어노테이션을 파싱하고 PyTorch 모델 학습에 적합한 텐서 형태로 변환하는 데이터 처리 역량 강화
- 정량적/정성적 평가 능력: 시각화를 통한 직관적 분석과 mAP 지표를 통한 객관적 성능 평가 방법을 모두 습득하여 모델 개선 방향 도출 가능

## 4. 참고 및 확장
- Backbone 교체: VGG16 대신 ResNet-50, MobileNet 등 더 강력하거나 경량화된 백본 네트워크 적용 실험 
- Hyperparameter Tuning: Anchor Size/Ratio, Learning Rate, Batch Size 등을 조절하여 탐지 성능 최적화
- Data Augmentation: 학습 데이터에 다양한 변환(Flip, Rotate, Color Jitter 등)을 적용하여 모델의 일반화 성능 향상 시도