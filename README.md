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

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/adc06fb6-177a-465c-8293-398858c72615" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/e36f7998-aaec-4078-b02e-ea67ee78bf2d" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/1101517e-e61d-4b42-b561-4ee45c78f94f" />

## 3. 이상 감지 Anomaly Detection

### 🛰 이상 감지 학습 방식
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/985ad610-50d7-4ccc-9a17-2aa1e0382648" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/4751b0ca-cb80-4c3a-ba1a-3fddf19bb0d1" />
<img src="docs/resources/video_gif/02_AD_No_Dehazing.gif" alt="02_AD_No_Dehazing.gif" width="800"/>
<img src="docs/resources/video_gif/03_AD_Dehazing.gif" alt="03_AD_Dehazing.gif" width="800"/>

## 4. 낙상 감지 Fall Detection

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/31dbde92-9598-485e-a084-1bc7e134c20a" />

<img src="https://github.com/user-attachments/assets/ac1ceadf-53a7-4eb9-8f55-9cbd8d159dfe" width="800"/>  
<img src="https://github.com/user-attachments/assets/58486cd9-d9b5-46f6-bcaf-c36f92431969" width="800"/>  
<img src="docs/resources/video_gif/04_PE1.gif" alt="04_PE1.gif" width="800"/>
<img src="docs/resources/video_gif/05_PE2.gif" alt="05_PE2.gif" width="800"/>
 


## 5. 상황실 Ctrl Room

### 🛰 MQTT 통신 구조
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/d11e990d-bc68-49d7-85ee-3318ded7239e" />

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/7fba15d9-5d4e-474f-a1f1-ca6866c52cb1" />
<img src="docs/resources/video_gif/06_Server_SystemLog.gif" alt="06_Server_SystemLog.gif" height="480"/>
<img src="docs/resources/video_gif/07_Server_Logbook.gif" alt="07_Server_Logbook.gif" height="480"/>

## 6. 팀원 소개
| 이름 | 담당 |
|------|------|
| **문두르** | PM |
| **류균봉** | Image Enhancement / Dehazing |
| **나지훈** | Server / MQTT / GUI / LLM / STT / TTS |
| **김찬미** | Pose Estimation / Fall Detection |
| **이환중** | Object Detection / Anomaly Detection |
