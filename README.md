# CTRL SEA CTRL VISION

## 1. 프로젝트 소개
> ### **AI 기반 선박 제어실 보조 On-Device 시스템**

### 주요 기능
- **안개 너머 객체 탐지 및 이상 감지**  
- **선원 안전 확보**  
- **자동 항해 일지 작성 및 브리핑**

**개발 기간**: 2025.09.26 ~ 2025.10.22  
**개발 환경**: Jetson Nano / Raspberry Pi 5 / Python / MQTT  
**발표 자료 다운로드**: [[Ctrl + Click Here]](https://drive.google.com/drive/folders/1VzminDn5eenhiwE3JjTkIos7xjNJQT3j?usp=sharing)

## 2. 안개 제거 Dehazing

> ### **이미지 향상(Image Enhancement) 및 복원(Image Restoration)을 통한 시야 확보**
>
### 기술 특징
- **Image Enhancement**: 대비 향상 및 노이즈 제거를 통한 시인성 개선
- **Image Restoration**: 안개로 손실된 이미지 정보 복원

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/adc06fb6-177a-465c-8293-398858c72615" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/e36f7998-aaec-4078-b02e-ea67ee78bf2d" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/1101517e-e61d-4b42-b561-4ee45c78f94f" />

## 3. 이상 감지 Anomaly Detection

**학습 방법**
- **정상 데이터**: 깨끗한 바다 사진들
- **이상 데이터**: 장애물이 있는 사진들
- **AI 모델**: EfficientNet-B3

### 🛰 이상 감지 학습 방식
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/985ad610-50d7-4ccc-9a17-2aa1e0382648" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/4751b0ca-cb80-4c3a-ba1a-3fddf19bb0d1" />


## 4. 낙상 감지 Fall Detection

- **카메라로 사람 관절 위치 파악** (머리, 어깨, 팔, 다리 등)
- **자세 각도 계산** (서 있는지, 누워있는지)
- **낙상 판정** → 즉시 상황실에 경보 전송 (MQTT)

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/31dbde92-9598-485e-a084-1bc7e134c20a" />

<img src="https://github.com/user-attachments/assets/ac1ceadf-53a7-4eb9-8f55-9cbd8d159dfe" width="800"/>  
<img src="https://github.com/user-attachments/assets/58486cd9-d9b5-46f6-bcaf-c36f92431969" width="800"/>  

 


## 5. 상황실 Ctrl Room

**MQTT**
- 센서들이 메시지를 주고받는 통신 방식
- 신문을 신청하듯이 "토픽"에 메시지 발행하면, 구독을 한 사람이 받아봄

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


### 겪었던 문제

**문제: Jetson Nano에서 AI 모델이 안 돌아감** 😓
- Jetson Nano는 2019년 구형 모델
- 최신 AI 모델 변환 시 오류 발생 (INT64 타입 문제)
- 버전 업그레이드도 안됨 (지원 종료)
