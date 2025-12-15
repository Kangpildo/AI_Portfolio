# 실습 Overview: VGG16 Model Quantization

## 1. 실습 목적
- 모델 경량화: 사전 학습된 VGG16 모델(FP32)에 정적 양자화(Post-Training Static Quantization, PTSQ)를 적용하여 모델의 파일 크기를 줄임.
- 성능 비교 및 검증: 양자화 전후의 모델 크기, 추론 속도, 그리고 예측 결과값의 차이를 비교하여 양자화의 효율성을 검증함.

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 설치**
  - 모델 양자화 및 추론에 필요한 핵심 라이브러리 (torch, torchvision, torch.ao.quantization) 설치 및 환경 구성.
- **데이터셋 준비 및 전처리 (Data Preparation)**
  - Pet 데이터셋 로드: 모델의 캘리브레이션(Calibration)을 위해 Pet 데이터셋을 사용.
  - 데이터 전처리: 이미지를 256으로 리사이즈하고 중앙을 224로 크롭한 뒤 텐서 변환 및 정규화(Normalize) 수행.
- **양자화 수행 (Quantization Process)**
  - 모델 정의: QuantStub과 DeQuantStub을 포함하는 QuantizedVGG16 래퍼 클래스를 정의하여 양자화 및 역양자화 노드 삽입.
  - 설정 및 캘리브레이션: fbgemm 백엔드를 설정하고, quantization.prepare를 통해 모델에 관찰자(Observer)를 부착한 후 데이터를 통과시켜 활성화 값의 범위를 측정 (Calibration).
  - 변환 및 저장: quantization.convert를 통해 FP32 연산을 INT8 연산으로 변환하고, TorchScript 형식으로 모델 저장.
- **성능 평가 (Evaluation)**
  - 단일 이미지(cat.jpg)를 사용하여 원본 FP32 모델과 양자화된 INT8 모델의 추론 결과(Logits)를 비교하고, 파일 크기 및 추론 속도 측정.

## 3. 결과 및 기대 효과
- 모델 용량 감소: 양자화 적용 결과, 모델 파일 크기가 약 537MB에서 134MB로 약 4배 감소하여 메모리 효율성 증대.
- 추론 속도 확인: GPU 기반 원본 모델(0.0451s) 대비 CPU 기반 양자화 모델(0.2675s)의 속도 차이를 확인함으로써, 하드웨어 가속의 중요성 및 CPU 환경에서의 INT8 연산 특성 이해.
- 정확도 유지: 양자화 후에도 예측 결과값(Logits)의 차이가 미미함을 확인하여, 모델의 성능 저하 없이 경량화가 가능함을 검증.

## 4. 참고 및 확장
- QAT 적용: 정적 양자화 외에 학습 도중 양자화를 고려하는 QAT(Quantization Aware Training) 기법 적용 및 비교 실험.
- 백엔드 최적화: qnnpack 등 다양한 양자화 백엔드를 적용하여 모바일 등 다른 배포 환경에서의 성능 테스트.
