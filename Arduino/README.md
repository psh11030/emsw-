# 🐾 IoT 반려동물 자동 간식 급여기  
Arduino + Ultrasonic + Servo + Processing Server + App Inventor

---

## 📘 프로젝트 개요
이 프로젝트는 **반려동물 간식 급여기를 원격으로 제어**할 수 있는 IoT 시스템이다.  
Arduino가 거리 센서 및 스위치 상태를 측정하고, Processing이 PC에서 서버 역할을 하여  
App Inventor 앱과 실시간 통신하는 구조로 되어 있다.

---

## 🏗 시스템 구성

### ✔ Arduino
- 초음파 센서(HC-SR04)로 거리 측정
- 스위치(On/Off) 입력 감지
- 서보모터로 간식 배출
- 시리얼 통신으로 Processing에 상태 전달

📄 파일: `Arduino/pet_dispenser.ino`

---

### ✔ Processing (Server)
- 아두이노 시리얼 데이터를 읽고 App Inventor로 전달
- App Inventor 요청을 받아 아두이노에 명령 전달
- HTML/HTTP 간단 서버 기능 수행

📄 파일: `Processing/server_processing.pde`

---

### ✔ App Inventor (Client App)
- Processing 서버로 GET 요청
- `"거리|스위치|피드"` 형식으로 받은 텍스트를 파싱해 UI 업데이트
- 버튼으로 간식 급여 명령 전송

📄 파일  
- `App/app.aia`  
- `App/AppInventor_Screenshots/` (스크린샷 폴더)

---

## 🔌 전체 동작 흐름

[Arduino] ←Serial→ [Processing Server] ←HTTP→ [App Inventor App]


### 1) Arduino  
센서값을 읽고 `"distance|switch|feed"` 형식으로 시리얼로 전송한다.

### 2) Processing  
- 아두이노의 문자열을 읽는다.  
- HTTP 요청이 오면 앱으로 문자열을 그대로 보낸다.  
- 앱에서 `/feed` 요청이 오면 아두이노에 `"FEED"` 명령 전송.

### 3) App Inventor  
- Web1.GotText → responseText를 `"|"` 기준으로 split  
- 각 항목을 label에 표시  
- 버튼 클릭 시 `/feed` 호출

---

## 📱 App Inventor 파싱 방식 (핵심 블록)

response = "112|ON|0"

list = split response at "|"

Label_Distance ← index 1
Label_Switch ← index 2
Label_Feed ← index 3


---

## 🧪 테스트 방법

### 1) 아두이노 연결  
- 보드 연결 후 시리얼 모니터로 데이터가 출력되는지 확인  
- 초음파 센서 / 스위치 / 서보 동작 점검

### 2) Processing 실행  
- Arduino COM 포트 자동 감지 또는 설정  
- 콘솔에서 아두이노 데이터가 계속 들어오는지 확인  
- 브라우저에서 `http://localhost:8080/` 접속  
  - 상태 문자열이 보이면 성공

### 3) App Inventor 앱 실행  
- Web URL을 **Processing 실행 PC의 IP + ":8080"** 로 설정  
  - 예: `http://192.168.0.13:8080/`

---

## 📂 폴더 구조

/Arduino
pet_dispenser.ino

/Processing
server_processing.pde

/App
app.aia
/AppInventor_Screenshots

/Report
Final_Report.pdf
README.md (이 파일)

/Video
youtube_link.txt


---

## 🎥 시연 영상
YouTube 링크  
(예: https://youtu.be/XXXXXXXX)

---

## 🧑‍💻 개발 환경
- Arduino IDE 2.x
- Processing 3.x 이상
- MIT App Inventor 2
- Windows 10 / 11

---

## 👨‍🏫 제작자
- 20250537 박세훈 (컴퓨터공학과 1학년)
- 2025 IoT 과제 제출용
