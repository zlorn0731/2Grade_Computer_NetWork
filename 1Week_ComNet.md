# 📚 컴퓨터 네트워크 (Computer Network)
## 📘 1장 컴퓨터 네트워크와 인터넷

### 인터넷이란 무엇인가?
- 종단 시스템(end system/ hosts)
  - 인터넷의 가장자리에서 네트워크 에플리케이션을 실행하는 장치
- 패킷 스위치
  - 패킷(packet)을 목적지로 전달하는 장비
  - L2 스위치(엑세스), L3 라우터(코어)
- 통신 링크
  - 동축 케이블, 구리선, 광케이블, 라디오 스펙트럼 등 다양한 물리 매체
  - 전송 속도 = 대역폭(bps)
- ISP
  - 가정, 기업, 대학 등에 인터넷 접속을 제공하는 사업자망
- Internet : "network of networks"
  - 인터넷 : "네트워크들로 이루어진 네트워크"
  - Interconnected ISPs
- 프로토콜
  - 인터넷의 모든 통신 활동을 제어하는 약속/규약
  - (예시) HTTP, streaming video, TCP, IP, WiFi, Ethernet
- 인터넷 표준
  - RFC : Request For Comments
  - [IETF] : Internet Engineering Task Force

### 서비스 관점에서 본 인터넷 (access network, subscribe network, core network)
- 분산 애플리케이션의 인프라 (서비스 관점 : 인터넷 = 분산 애플리케이션)
  - 웹, 비디오 스트리밍, 이메일, 온라인 게임, SNS, P2P 등에 통신 서비스를 제공
  - 애플리케이션은 네트워크 코어가 아닌 종단 시스템(Host)에서만 실행됨
- 소켓 인터페이스(Socket)
  - 송신 프로그램이 인터넷 인프라를 통해 목적지 프로그램으로 [데이터]를 전달하도록 지시하는 프로그래밍 인터페이스
- 우편 서비스 [API] 비유
  - 편지 작성 → 봉투에 주소/우표 부착 → 우체통에 투입 → 우체국 전달

### 프로토콜이란 무엇인가?
```
human protocols:
- "몇 시에요?" "질문이 있습니다" 등 상대방과의 대화 및 예의 범절

network protocols:
- 컴퓨터/네트워크 장치 간의 통신
- 인터넷의 모든 통신 활동은 프로토콜이 제어함
```
- 프로토콜 3대 요소 🔥
  - Format(포멧/문법) : 메시지의 구조 및 인코딩 방식
  - Order(순서) : 메시지 주고받는 시퀀스
  - Actions(행동) : 메시지 송수신 또는 이벤트 발생 시 수행할 동작
```
a human protocol and a computer network protocol:

[Human protocol]

A →Hi→ B →Hi→ A →Got the time?→ B →2:00→
_________________________________________________________

[Network protocol]

Computer →TCP connection [request]→ Server →TCP connection response→ Computer →Get http://www.....→ Server →<file>→
```

### 네트워크 구분
- PAN(Personal Area Network)
  - [10m 이내의 개인통신망]
  - 기술 : Bluetooth, Zigbee 등
- LAN(Local Area Network, 근거리망)
  - [대학 캠퍼스, 건물 내 수m ~ 수백m 범위]
  - 기술 : Ethernet(IEEE 802.3)
- MAN(Metropolitan Area Network, 도시권망)
  - [하나의 도시나 대형 캠퍼스 범위]
  - 기술/장비 : Metro Ethernet, Carrier Ethernet Switch, DWDM 관정송, MPLS
- WAN(Wide Area Network, 광역망)
  - [국가, 대륙 간 수백~수천km 범위를 연결하는 광역 시스템]
  - 기술/장비 : 백본 라우터, SD-WAN, 전용 회선
 
##### ✍️ 작성자: 박지안
##### 🗓️ 작업일: 2026-10-06
