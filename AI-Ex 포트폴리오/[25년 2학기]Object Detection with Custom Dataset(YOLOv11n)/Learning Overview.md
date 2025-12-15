# 실습 Overview: Object Detection with Custom Dataset (YOLOv11n)

## 1. 실습 목적
- 커스텀 데이터셋 활용: 준비한 커스텀 데이터셋(Person Detection)을 활용하여 객체 탐지 모델을 학습시키는 과정을 습득함.
- YOLO 모델 학습: 최신 객체 탐지 모델인 YOLO(v11n)을 사용하여 모델을 로드하고, 주어진 데이터에 맞게 Fine-tuning하는 방법을 익힘.

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 설치**
  - Google Drive 마운트 및 ultralytics 라이브러리 설치를 통해 YOLO 모델 학습 환경을 구축함.
- **데이터셋 준비 및 전처리**
  - 데이터 경로 설정: Google Drive에 저장된 Person Detection 데이터셋(data.yaml) 경로를 지정하여 모델 학습에 활용함.
  - 캐시 생성: 학습 및 검증 데이터의 라벨 정보를 스캔하고 캐시 파일을 생성하여 데이터 로딩 속도를 최적화함.
- **모델 학습 (Training)**
  - 모델 로드: yolov8n.pt 가중치를 기반으로 YOLO 모델을 초기화함 (실습 로그에서는 yolo11n.pt가 다운로드 및 사용됨).
  - 학습 파라미터 설정: Epoch 100, 이미지 크기 640으로 설정하여 학습을 진행함. Optimizer는 AdamW, Learning Rate는 자동으로 조정됨.
  - 학습 진행: 총 100 Epoch 동안 학습이 진행되었으며, Box Loss, Class Loss, mAP 등의 지표가 지속적으로 개선됨을 확인함.
- **성능 평가 및 추론 (Validation & Inference)**
  - 검증(Validation): 학습된 모델(best.pt)을 사용하여 검증 데이터셋에 대한 mAP50-95 성능을 평가함 (mAP50-95: 0.505 달성).
  - 테스트 및 시각화: 테스트 이미지를 대상으로 추론을 수행하고, 객체 탐지 결과(Bounding Box)가 그려진 이미지를 저장하여 시각적으로 확인함.

## 3. 결과 및 기대 효과
- 모델 성능 확보: 100 Epoch 학습 후 mAP50은 0.707, mAP50-95는 0.501을 기록하여 준수한 탐지 성능을 달성함.
- 실무 적용 가능성: 커스텀 데이터셋을 활용한 End-to-End 학습 파이프라인을 경험함으로써, 다양한 도메인의 객체 탐지 문제에 YOLO 모델을 적용할 수 있는 능력을 배양함.
- 최신 모델 활용: Ultralytics 라이브러리를 통해 최신 YOLO 아키텍처(v11)를 손쉽게 활용하고, 학습 및 추론 과정을 효율적으로 관리하는 방법을 익힘.

## 4. 참고 및 확장
- 하이퍼파라미터 튜닝: imgsz, batch, lr0 등의 파라미터를 조절하여 모델 성능을 추가적으로 최적화하는 실험 가능.
- 데이터 증강(Augmentation): Albumentations 등을 활용하여 학습 데이터를 다양화함으로써 모델의 일반화 성능을 향상시킬 수 있음.
- 배포 및 경량화: 학습된 모델을 ONNX, TensorRT 등으로 변환하여 실제 서비스 환경에 배포하거나, Quantization을 통해 경량화하는 후속 실습 가능.