# 연구 2단계: 기준점(Baseline) 모델 수립

## 1. 연구 개요 및 목적
비교 실험을 위한 기준(Baseline) 성능을 수립합니다. 가장 범용적인 `YOLOv8n (Nano)` 모델을 사용하여 데이터셋의 학습 난이도를 파악합니다.

## 2. 주요 설정
- **Model**: `yolov8n.pt` (가볍고 빠름, 초기 실험용 최적)
- **Epochs**: 30 (수렴 패턴 확인용)
- **Optimizer**: Adam (빠른 초기 수렴)

## 3. 예상 결과
- `saveModels/baseline_yolov8n` 폴더에 학습된 가중치(`best.pt`)가 저장됩니다.
- 콘솔에 초기 mAP 수치가 출력됩니다.