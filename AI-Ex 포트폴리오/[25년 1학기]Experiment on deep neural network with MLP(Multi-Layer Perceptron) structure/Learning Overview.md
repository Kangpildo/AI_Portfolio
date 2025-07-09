# 실습 Overview: Experiment on deep neural network with MLP(Multi-Layer Perceptron) structure

## 1. 실습 목적
- MLP(Multi-Layer Perceptron) 구조의 심층 신경망 실험을 통해 기본 구조와 하이퍼파라미터의 영향을 이해
- 활성화 함수, 배치 정규화, 가중치 초기화 등 딥러닝 핵심 요소의 실제 효과 분석

## 2. 실습 내용 요약

### 2.1. 데이터 분할 및 준비
- **MNIST** 데이터셋을 활용
- 전체 데이터의 70%를 학습, 30%를 테스트로 구분하여 DataLoader로 구성

### 2.2. MLP 모델 구현
- **Hidden Layer 2개, 각 20개 노드**로 구성된 MLP 모델 구현 (BatchNorm 적용 가능)
- 모델 구조와 파라미터 요약 시각화

### 2.3. 활성화 함수 비교 실험
- ReLU와 Sigmoid 함수 각각을 적용
- 테스트 정확도 및 학습 성능 비교  
  - ReLU가 Sigmoid에 비해 학습 속도, 정확도에서 우수  
  - Sigmoid는 saturate 구간이 많아 gradient 소실 가능

### 2.4. Batch Normalization 적용 실험
- BatchNorm 적용/미적용 각각의 테스트 결과 비교  
  - BatchNorm 적용 시 학습 안정성, 정확도 모두 소폭 향상  
  - Sigmoid와 함께 쓸 때 효과가 더욱 뚜렷

### 2.5. 가중치 초기화 방식 실험
- **Kaiming, Xavier, Normal**(정규분포) 초기화별 실험
- 세 방식 모두 높은 정확도(0.93~0.94), 실제 차이는 미미  
  - Xavier ≥ Normal ≥ Kaiming  
  - 작은 MLP 모델에서는 초기화 방식이 성능에 큰 영향 없음

## 3. 결론 및 요약
- 활성화 함수, 배치 정규화, 초기화 방식 등 딥러닝 핵심 요소가 실제 성능에 미치는 영향 체험
- 소규모 MLP에서는 초기화 방식보다는 활성화 함수나 BatchNorm 등의 효과가 더 두드러짐
- 데이터셋이나 모델 구조에 따라 결과가 달라질 수 있음을 실험적으로 확인

## 4. 참고/확장
- 더 복잡한 모델, 다양한 데이터셋, 딥러닝 최신 기법으로 확장 가능
- 코드 및 실험 결과에 대한 추가 해설, 시각화, 보고서 작성 등 심화 과제로 연계 가능
