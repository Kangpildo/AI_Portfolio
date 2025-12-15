# 실습 Overview: VisionModel_YOLOv8_Pose

## 1. 실습 목적
- YOLOv8 (You Only Look Once version 8) 기반의 포즈 추정(Pose Estimation) 모델 구조 이해 및 실습
- Ultralytics YOLO 라이브러리를 활용하여 Pre-trained YOLOv8-Pose 모델을 로드하고, 비디오 데이터에서 사람의 키포인트(Keypoints)를 실시간으로 탐지하는 과정 습득
- Pose Estimation 시각화: 탐지된 사람의 관절(Keypoints)과 스켈레톤(Skeleton)을 영상 위에 시각화하는 기술 구현

## 2. 주요 실습 내용
- **환경 설정 및 라이브러리 로드**
  - ultralytics, cv2, torch 등 딥러닝 및 영상 처리에 필요한 라이브러리 설치 및 로드 
  - Google Drive 마운트 및 데이터셋 경로 설정 
- **모델 로드 (Model Loading)**
  - YOLOv8-Pose 모델 로드: yolov8n-pose.pt (Nano 모델) 또는 yolov8m-pose.pt (Medium 모델) 등 사전 학습된 포즈 추정 모델을 로드 
- **비디오 처리 및 추론 (Video Processing & Inference)**
  - 비디오 캡처: cv2.VideoCapture를 사용하여 테스트용 비디오 파일(woman.mp4) 로드 
  - 프레임별 추론 함수 구현 (predict): 각 비디오 프레임을 YOLO 모델에 입력하여 포즈 추정 결과(results)를 반환하는 함수 정의. IoU 및 Confidence Threshold 설정 가능 
- **시각화 함수 구현 (Visualization)**
  - Bbox 시각화 (draw_boxes): 탐지된 객체의 바운딩 박스를 영상에 그리는 함수 구현 (옵션) 
  - Keypoints 시각화 (draw_keypoints): ultralytics.yolo.utils.plotting.Annotator를 활용하거나 OpenCV를 사용하여 탐지된 키포인트(관절)와 연결선(스켈레톤)을 그리는 함수 구현. 각 키포인트의 신뢰도(Score)가 일정 수준 이상일 때만 시각화 
- **통합 실행 루프 (Main Loop)**
  - 비디오 프레임을 순차적으로 읽어와 모델 추론을 수행하고, 결과를 시각화하여 출력하는 전체 파이프라인 실행 
  - cv2.imshow를 통해 결과 영상을 실시간으로 확인하고, 비디오 종료 시 자원 해제

## 3. 결과 및 기대 효과
- Pose Estimation 활용 능력 배양: 단일 단계(Single-Stage) 객체 탐지 모델인 YOLO를 확장하여 사람의 자세를 추정하는 원리 이해
- 실시간 영상 처리 역량 강화: OpenCV와 딥러닝 모델을 결합하여 비디오 스트림을 처리하고 시각화하는 실무 기술 습득
- 다양한 응용 분야 적용: 행동 인식, 피트니스 자세 교정, 제스처 제어 등 포즈 추정 기술을 활용한 다양한 애플리케이션 개발의 기초 마련
- 
## 4. 참고 및 확장
- 모델 크기 변경: n, s, m, l, x 등 다양한 크기의 YOLOv8 모델을 적용하여 속도와 정확도 간의 트레이드오프(Trade-off) 분석
- Custom Dataset 학습: 자신만의 포즈 데이터셋을 구축하고 YOLOv8-Pose 모델을 파인튜닝(Fine-tuning)하여 특정 도메인에 특화된 모델 개발
- 멀티 퍼슨 포즈 추정: 영상 내 다수의 사람에 대해 동시에 포즈를 추정하고 추적(Tracking)하는 기능으로 확장