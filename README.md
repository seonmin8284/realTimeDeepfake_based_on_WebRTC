# 🎭 realTimeDeepfake_based_on_WebRTC

### 📌 개요
본 프로젝트는 **WebRTC 기반의 실시간 딥페이크 스트리밍 서비스**로, AI 기반 얼굴 변환 기술을 활용하여 낮은 지연 시간으로 실시간 영상 변환을 제공합니다.  

✅ **주요 기능**  
- **실시간 얼굴 변환**: AI 딥러닝 모델을 활용한 얼굴 변환  
- **WebRTC 스트리밍**: 낮은 지연 시간의 실시간 영상 처리  
- **P2P 및 TURN 서버 지원**: 방화벽/NAT 환경에서도 원활한 연결  
- **웹 및 모바일 지원**: 브라우저에서 실행 가능


![설명](./processD.png)
---

### 📌 서버 구성 요소
이 서비스는 다음과 같은 3개의 주요 서버로 구성됩니다.

1️⃣ **WebRTC 서버** – 클라이언트 간 P2P 연결 관리 및 신호 전달 (Signaling Server)  
2️⃣ **TURN 서버** – NAT/방화벽 우회 (Relay Server)  
3️⃣ **프레임 변환 서버 (AI 서버)** – 실시간 얼굴 변환 수행 (딥페이크 모델 실행)  

---

### 📍 흐름도 설명
1. **클라이언트 (Broadcaster, Viewer)** 가 **웹 및 모바일 브라우저**를 통해 **WebRTC 서버 접속**
2. **클라이언트 (Broadcaster)** 가 **WebRTC 서버를 통해 시그널링 (Signaling) 및 스트리밍 서비스 송출 시작**
3. **P2P 연결 실패 시 -> TURN 서버를 거쳐** 데이터 전송
4. **WebRTC에서 캡처한 프레임을 -> 프레임 변환 Deepfake용 AI서버로 전송**
5. **프레임 변환 서버에서 AI 변환 후 -> WebRTC 서버로 반환**
6. **변환된 프레임을 WebRTC를 통해 -> 클라이언트 B에게 전송**


![설명](./sequence.png)
---
### 📌 주요 흐름

#### ✅ 1. WebRTC 서버
- 클라이언트 간 시그널링 처리 (ICE Candidate 교환)
- 연결 정보를 전달하고 TURN 서버 정보를 제공

#### ✅ 2. TURN 서버 (P2P 연결 실패 시)
- 방화벽/NAT 문제로 P2P 연결이 불가능할 경우 중계 서버 역할

#### ✅ 3. 프레임 변환 서버 (AI 딥페이크 서버)
- 클라이언트에서 WebRTC로 전달된 프레임을 변환
- 변환된 프레임을 다시 클라이언트로 전송

#### ✅ 4. WebRTC 스트리밍
- 변환된 영상이 WebRTC를 통해 상대방 클라이언트로 전달

---

### 📌 특징 및 장점
✅ **서버 분리로 확장성 및 부하 분산 가능**  
✅ **TURN 서버를 통한 네트워크 우회 지원**  
✅ **딥페이크 서버를 독립적으로 운영하여 AI 연산 부담 분산**  
✅ **P2P 연결이 가능한 경우 TURN 서버를 거치지 않아 트래픽 절감**  

---

### 📌 기술 스택

#### 🖥 **Backend**
- **WebRTC** (Signaling & P2P Video Streaming)
- **Python / Flask** (API Server)
- **PyTorch / TensorFlow** (딥페이크 AI 모델)
- **Redis / Celery** (비동기 프레임 처리)

#### 📡 **Infra**
- **AWS EC2, GPU 인스턴스** (AI 연산 서버)
- **Docker / Kubernetes** (컨테이너 관리)
- **Nginx / WebSocket** (실시간 연결 지원)

#### 💻 **Frontend**
- **React.js / Next.js** (웹 UI)
- **WebRTC API** (카메라 스트리밍 & P2P 연결)

