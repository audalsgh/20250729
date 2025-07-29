# 27일차

## 앙상블 방식으로 피플넷 + 트래픽넷 + YOLOv11 통합해보기
[PeopleNet 코드에서 JSON 사용 이유](https://docs.google.com/document/d/1SnvIRPLFytKIlkodnae1Oy3yTGx06QKs6U2mvX7UhUw/edit?tab=t.0#heading=h.7bz91vm5rr3n)<br>
[NVIDIA API키 얻는 링크](https://org.ngc.nvidia.com/setup/api-keys)<br>
runpod에서 실습해볼땐, 교수님이 주신코드를 활용하고 api키는 내것으로 써야한다.<br> 
<img width="276" height="349" alt="image" src="https://github.com/user-attachments/assets/1809e4a5-c531-4bf5-bb4b-b1e66e675885" /><br>
<img width="1388" height="835" alt="image" src="https://github.com/user-attachments/assets/b5642df7-2700-43c1-b6d1-80f7062f5543" /><br>

## 먼저 NVIDIA TAO Toolkit에서 제공하는 사전 학습된 "인물 탐지 모델"인 피플넷부터 사용해보자.
**시간관계상 피플넷까지만 실습해보고 마침.**<br>
[peoplenet파일 다운로드 링크](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/tao/models/peoplenet)<br>

### 목적
- 화면(영상)에서 사람(pedestrian)을 빠르고 경량화된 방식으로 검출하기 위해 설계된 딥러닝 모델

### 구조(Architecture)
- 백본(Backbone)
  - 보통 ResNet-34/50 계열을 사용해 영상에서 특징(feature) 맵 추출
  
- 헤드(Head)
  - 사람의 머리, 가슴, 다리 등 주요 부위별로 따로 히트맵(heatmap) 출력
  - 각 히트맵은 해당 부위 존재 확률을 픽셀 단위로 표시

### 후처리(Post-processing)
- 히트맵들을 합산하거나 별도 채널별 thresholding
- 컨투어 혹은 bounding‐box 회귀를 통해 최종 사람 위치 박스 생성

### 입출력
- 입력: 보통 (1, 3, H, W) 형식의 RGB 이미지 배치
- 출력: (1, C, h, w) 형태의 히트맵 텐서 (C = 부위 채널 개수, 예: 3)
  히트맵 → 이진 마스크 변환 → 컨투어/박스로 사람 위치 표시

### 장점
- 부위별 히트맵 덕분에 자세(pose)에 강건
- 비교적 가벼운 구조로 실시간 추론에 적합

### 단점
- 히트맵 해상도가 낮으면 작은/멀리 있는 사람 검출이 어려움
- 후처리(합산·morphology)가 추가로 필요

### 활용 예시
- 자율주행 차량의 보행자 감지
- CCTV 영상 내 실시간 이상 행동 모니터링
- 스마트 시티 안전 시스템

### 챗GPT로, Colab에 다운받은 Peoplenet 모델을 직접 업로드 → 추론 테스트 → 영상에 사람 감지 표시하는 코드 실습<br>
<img width="701" height="171" alt="image" src="https://github.com/user-attachments/assets/ced10690-4e96-4bef-bf65-90fa67de42c8" /><br>
다운받은 Peoplenet.onnx 파일을 직접 업로드하도록 짰다.<br>

<img width="1179" height="670" alt="image" src="https://github.com/user-attachments/assets/4b69cffc-5d89-4430-9a46-793bea520409" /><br>
되긴했는데 YOLO처럼 정확한 성능을 뽐내진 못했다. 코드를 잘 못짠건지, 모델이 잘못된걸수도 있음.
