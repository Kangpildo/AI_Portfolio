# 연구 4단계: 데이터 증강(Augmentation) 효과 검증

## 1. 연구 개요 및 목적
YOLO의 강력한 데이터 증강 기법이 본 표정 데이터셋에서 실제로 성능 향상에 기여하는지 확인하는 **제거 실험(Ablation Study)**입니다.

## 2. 실험 설계
- **조건 A**: Augmentation = False (원본 이미지만 사용)
- **조건 B**: Augmentation = True (Mosaic, Flip 등 적용 - Baseline)

## 3. 결과 해석
- 일반적으로 `True`일 때 mAP가 더 높아야 합니다.
- 만약 `False`가 더 높다면, 데이터 증강이 표정의 미세한 특징을 왜곡하고 있을 가능성이 있으므로 증강 파라미터(회전 각도 등)를 조절해야 합니다.