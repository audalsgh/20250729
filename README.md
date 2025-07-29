# 27일차

## 앙상블 방식으로 피플넷 + 트래픽넷 + YOLOv11 통합해보기
[PeopleNet 코드에서 JSON 사용 이유](https://docs.google.com/document/d/1SnvIRPLFytKIlkodnae1Oy3yTGx06QKs6U2mvX7UhUw/edit?tab=t.0#heading=h.7bz91vm5rr3n)<br>
[NVIDIA API키 얻는 링크](https://org.ngc.nvidia.com/setup/api-keys)<br>
<img width="1388" height="835" alt="image" src="https://github.com/user-attachments/assets/b5642df7-2700-43c1-b6d1-80f7062f5543" /><br>

1. 먼저 NVIDIA TAO Toolkit에서 제공하는 사전 학습된 "인물 탐지 모델"인 피플넷부터 사용해보자.<br>
[peoplenet파일 다운로드 링크](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/tao/models/peoplenet)<br>
Colab에 다운받은 Peoplenet 모델을 직접 업로드 → 추론 테스트 → 영상에 사람 감지 표시하는 코드 짜기<br>
<img width="701" height="171" alt="image" src="https://github.com/user-attachments/assets/ced10690-4e96-4bef-bf65-90fa67de42c8" /><br>
다운받은 Peoplenet.onnx 파일을 직접 업로드하도록 짰다.<br>
<img width="1179" height="670" alt="image" src="https://github.com/user-attachments/assets/4b69cffc-5d89-4430-9a46-793bea520409" /><br>
되긴했는데 YOLO처럼 정확한 성능을 뽐내진 못했다. 코드를 잘 못짠건지, 모델이 잘못된걸수도 있음.

