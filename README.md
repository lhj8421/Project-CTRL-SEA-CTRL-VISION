# CTRL SEA CTRL VISION

## 1. 프로젝트 소개
> ### **AI 기반 선박 제어실 보조 On-Device 시스템**

### 주요 기능
- **안개 너머 객체 탐지 및 이상 감지**  
- **선원 안전 확보**  
- **자동 항해 일지 작성 및 브리핑**

**개발 기간**: 2025.09.26 ~ 2025.10.22  
**개발 환경**: Jetson Nano / Raspberry Pi 5 / Python / MQTT  

## 2. 안개 제거 Dehazing

> ### **이미지 향상(Image Enhancement) 및 복원(Image Restoration)을 통한 시야 확보**
>
### 기술 특징
- **Image Enhancement**: 대비 향상 및 노이즈 제거를 통한 시인성 개선
- **Image Restoration**: 안개로 손실된 이미지 정보 복원

### 🔄 동작 과정
1. **카메라에서 안개 낀 영상 입력**
2. **어두운 부분(Dark Channel) 분석** → 안개가 없는 곳 찾기
3. **안개 농도 계산** → 얼마나 안개가 짙은지 파악
4. **원래 색상 복원** → 안개를 수학적으로 제거
5. **깨끗한 영상 출력** → 화면에 표시

💡 **쉽게 말하면**: 사진에서 뿌연 부분을 찾아서 "원래는 이 색깔이었을 거야"라고 역계산하는 방식

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/adc06fb6-177a-465c-8293-398858c72615" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/e36f7998-aaec-4078-b02e-ea67ee78bf2d" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/1101517e-e61d-4b42-b561-4ee45c78f94f" />

## 3. 이상 감지 Anomaly Detection

**학습 방법**
- **정상 데이터**: 깨끗한 바다 사진들
- **이상 데이터**: 장애물이 있는 사진들
- **AI 모델**: EfficientNet-B3

### 🔄 동작 과정
1. **카메라에서 바다 영상 촬영**
2. **안개 제거 처리** (Dehazing)
3. **AI 모델에 이미지 입력** (EfficientNet-B3)
4. **정상/이상 판단** 
   - 정상: 깨끗한 바다 → 아무 조치 없음
   - 이상: 장애물 발견 → 경고음 + 위치 표시
5. **상황실로 경보 전송** (MQTT)

💡 **쉽게 말하면**: AI가 "이건 깨끗한 바다야" vs "어? 뭔가 있네?"를 구분

### 🛰 이상 감지 학습 방식
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/985ad610-50d7-4ccc-9a17-2aa1e0382648" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/4751b0ca-cb80-4c3a-ba1a-3fddf19bb0d1" />


## 4. 낙상 감지 Fall Detection

- **카메라로 사람 관절 위치 파악** (머리, 어깨, 팔, 다리 등)
- **자세 각도 계산** (서 있는지, 누워있는지)
- **낙상 판정** → 즉시 상황실에 경보 전송 (MQTT)

### 🔄 동작 과정
1. **카메라로 선원 촬영**
2. **AI가 사람 관절 33개 지점 인식** (머리, 어깨, 팔꿈치, 무릎 등)
3. **몸의 각도 계산**
   - 서 있음: 어깨-엉덩이 각도 > 60도
   - 쓰러짐: 어깨-엉덩이 각도 < 30도
4. **낙상 판정 조건 확인**
   - 각도가 30도 이하 + 2초 이상 유지
5. **긴급 상황 알림** → 즉시 상황실에 MQTT 전송

💡 **쉽게 말하면**: 사람이 서 있는지 쓰러져 있는지 각도로 판단

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/31dbde92-9598-485e-a084-1bc7e134c20a" />

<img src="https://github.com/user-attachments/assets/ac1ceadf-53a7-4eb9-8f55-9cbd8d159dfe" width="800"/>  
<img src="https://github.com/user-attachments/assets/58486cd9-d9b5-46f6-bcaf-c36f92431969" width="800"/>  

 


## 5. 상황실 Ctrl Room

**MQTT**
- 센서들이 메시지를 주고받는 통신 방식
- 신문을 신청하듯이 "토픽"에 메시지 발행하면, 구독을 한 사람이 받아봄

### 🔄 동작 과정
1. **각 센서/카메라가 데이터 생성**
   - 안개 제거 이미지
   - 이상 탐지 결과
   - 낙상 감지 알림
2. **MQTT Broker(중앙 서버)로 메시지 발행**
   - 예: "ship/ai/anomaly" 토픽에 "장애물 발견!" 발행
3. **상황실 컴퓨터가 해당 토픽 구독**
   - 미리 신문 구독하듯이 "이 정보 받을게요" 등록
4. **실시간으로 메시지 수신 → 화면에 표시**
5. **긴급 상황 시 경보음 자동 재생**

💡 **쉽게 말하면**: 
- 센서 = 신문사 (정보 발행)
- MQTT Broker = 우체국 (중간 전달)
- 상황실 = 구독자 (정보 받아서 확인)

### 🛰 MQTT 통신 구조
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/d11e990d-bc68-49d7-85ee-3318ded7239e" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/7fba15d9-5d4e-474f-a1f1-ca6866c52cb1" />

## 6. 팀원 소개
| 이름 | 담당 |
|------|------|
| **문두르** | PM |
| **류균봉** | Image Enhancement / Dehazing |
| **나지훈** | Server / MQTT / GUI / LLM / STT / TTS |
| **김찬미** | Pose Estimation / Fall Detection |
| **이환중** | Object Detection / Anomaly Detection |


### 💦 겪었던 문제

**문제: Jetson Nano에서 AI 모델이 안 돌아감** 😓
- Jetson Nano는 2019년 구형 모델
- 최신 AI 모델 변환 시 오류 발생 (INT64 타입 문제)
- 버전 업그레이드도 안됨 (지원 종료)

**해결 : 프로젝트 발표에서 ONNX파일을 Post-Traing 기법을 사용해서 JetsonNano에서 발생한 문제들을 해결할 수 있다는 것을 현재 근무하고 계시는 멘토분들에게 피드백을 받음**
