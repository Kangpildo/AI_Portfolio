# 실습 Overview: Image Emotion Classification using YOLOv5/8/10(Nano, Small)

## 1. 실습 목적
- YOLO 기반 분류 모델 학습: 객체 탐지(Detection)에 주로 사용되는 YOLO 아키텍처를 이미지 분류(Classification) 태스크에 적용하여 감정 인식 모델을 구현함.
- 모델 크기별 성능 비교: 동일한 데이터셋과 학습 조건에서 모델 크기가 다른 Nano(n) 모델과 Small(s) 모델을 각각 학습시켜 성능과 효율성을 비교 분석함.

## 2. 주요 실습 내용
- **환경 설정 및 데이터셋 준비**
  - 라이브러리 설치: ultralytics를 설치하여 YOLOv11 기반의 분류 모델 학습 환경을 구축함.
  - 데이터셋 구성: 9가지 얼굴 표정 클래스('angry', 'contempt', 'disgust', 'fear', 'happy', 'neutral', 'sad', 'sleepy', 'surprised')로 구성된 이미지 데이터를 학습에 활용함.
- **모델 학습 (Training)**
  - 모델 선정: ImageNet으로 사전 학습된 YOLOv5/8/10(Nano, Small) 모델을 로드하여 전이 학습(Transfer Learning)을 수행함.
  - 학습 파이프라인: Epoch 30, Batch Size 32, Image Size 224로 설정하고, Optimizer는 AdamW, Learning Rate는 0.001로 지정하여 학습을 진행함.
  - 경량화 전략: Nano 모델 학습을 통해 엣지 디바이스 탑재를 고려한 초경량 모델 생성 과정을 실습함.
- **성능 평가 및 시각화 (Evaluation)**
  - 학습 지표 확인: 학습 과정에서의 Loss 감소와 Accuracy 상승 추이를 시각화하여 모델의 수렴 과정을 확인함.
  - 혼동 행렬(Confusion Matrix): 테스트 데이터를 통해 클래스별 예측 정확도를 분석하고, 모델이 혼동하는 감정 클래스를 식별함.

## 3. 결과 및 기대 효과
- 모델 스케일링 비교: Nano 모델과 Small 모델의 학습 결과 비교를 통해, 서비스 환경(속도 중요 vs 정확도 중요)에 따른 최적의 모델 선택 기준을 마련함.
- YOLO의 범용성 검증: YOLO 아키텍처가 단순 객체 탐지를 넘어 이미지 분류 작업에서도 높은 성능과 효율성을 보여줌을 확인함.

## 4. 참고 및 확장
- 하이퍼파라미터 튜닝: Epoch 수를 늘리거나(Early Stopping 적용), Learning Rate Scheduler를 변경하여 분류 정확도를 추가로 개선하는 실험 가능.
- 데이터 증강(Augmentation): Albumentations 등을 적용하여 표정 이미지의 조명, 각도 변화에 강건한 모델로 고도화 가능.
- 배포 최적화: 학습된 모델을 ONNX, TensorRT 포맷으로 변환하여 실시간 영상 처리 시스템에서의 추론 속도를 극대화하는 후속 연구 가능.