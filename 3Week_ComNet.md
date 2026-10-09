# 📚 컴퓨터 네트워크 (Computer Network)
## 📘 2장 애플리케이션 계층

### 다양한 네트워크 애플리케이션들
- 텍스트/파일 서비스 : 전자메일(SMTP), 파일 전송(FTP), 원격 접속(SSH/Telnet)
- 웹 & 전자상거래 : WWW, 검색엔진, 전자상거래
- 메시징 & 소셜 미디어 : 인스턴스 메시징, SNS(Instargram, Facebook, X)
- 미디어 스트리밍 : 저장형 동영상(YouTube, Netflix), IPTV
- 실시간 대화형 서비스 : VolP / 화상회의(Zoom, Teams, Skype), 다중 사용자 온라인 게임
- 클라우드 AI API(OpenAI/Gemini API 서비스)
- 실시간 웹 협업 툴(Figma, Notion)
- ...

### 네트워크 애플리케이션의 원리
- 종단 시스템 중심 개발
  - 개발자는 오직 종단 시스템에서 동작하는 앱 SW만 작성
  - (예) 웹 서버 SW ←→ 브라우저 SW
- 네트워크 장비 프로그래밍 불필요
  - 라우터/스위치를 위한 사용자 앱을 SW 작성 불필요
  - 네트워크 장비는 사용자 애플리케이션을 실행하지 않고 패킷 전달만 전담

### 애플리케이션 구조
- 애플리케이션 구조
  - 애플리케이션 개발자에 의해 설계되는 소프트웨어의 조직적 배치 구조
  - 다양한 종단 시스템 상에서 프로세스들이 어떻게 배치되고 통신할지 지시
- 대표적인 두 가지 패러다임
  - 클라이언트-서버(Client-Server) 구조
  - P2P(Peer-to-Peer) 구조

### 클라이언트-서버 구조
- 서버
  - 항상 켜져있는 고정 호스트
  - 고정 IP를 보유
  - 대규모 접속 처리를 위해 수만대의 서버 클러스터(데이터센터)로 확장
- 클라이언트
  - 서버와 통신하는 단말 프로세스
  - 간헐적으로 인터넷에 연결되며, 동적 IP 주소를 할당받음
  - 클라이언트끼리는 직접 통신하지 않음(모든 통신은 서버를 경유)
 
### P2P 구조
- 항상 켜져 있는 서버에 의존하지 않거나 최소한으로만 의존
- 간헐적으로 연결되는 종단 시스템 쌍이 직접 데이터를 주고받음
- 새로운 피어가 참여하면 서비스 요청(부하)도 늘어나지만, 동시에 새로운 데이터 분배 능력(서버 용량)도 추가됨
- 특징
  - 확장성이 높다
  - 비용 효율적이다
  - 보안에 문제가 있을 수 있다

### 프로세스간 통신
- 프로세스
  - 종단 시스템에서 실행 중인 프로그램
  - 네트워크에서 실제로 통신하는 주체는 '프로그램'이 아니라 '프로세스'이다
- 통신 환경에 따라
  - 동일 호스트의 내부 프로세스 간 통신:
    - OS가 제공하는 IPC(inter-process communication)를 이용해서 통신한다
  - 서로 다른 호스트 간 프로세스 통신:
    - 컴퓨터 네트워크를 통한 메시지 교환 방식으로 통신한다
- 프로세스의 역할
  - 클라이언트 프로세스 : 두 프로세스 간의 통신을 초기화하는 프로세스
    - (예) 웹 브라우저
  - 서버 프로세스 : 세션을 시작하기 위해 접속을 기다리는 프로세스
    - (예) 웹 서버
  - P2P : 클라이언트 프로세스와 서버 프로세스를 모두 가지고 있다

### 소켓(Sockets)
- 프로세스가 네트워크로 메시지를 보내고 받기 위한 출입구
- 애플리케이션 계층과 전송 계층 사이의 프로그래밍 인터페이스 : API
- 애플리케이션 개발자
  - 소켓의 응용 계층을 통제
  - 전송 계층 프로토콜 선택 및 일부 매개변수 설정(최대 버퍼 크기, 세그먼트 크기 등)
- 운영체제
  - 전송 계층 및 네트워크 계층을 통제

### 프로세스의 주소 : 포트 번호
- 메시지를 수신하려면 프로세스는 식별자를 가져야 한다
- 호스트 상의 프로세스는 IP 주소와 포트번호를 식별자로 삼는다
  - (예) HTTP 메시지를 gaia.cs.umass.edu web server로 보내기 위해서
    - IP address : 128.119.245.12 and Port number : 80
- 포트 번호 리스트
  - Well-known Ports : 0 ~ 1023
    - IANA에 의해 주요 표준 서비스용으로 예약됨
    - (예) HTTP 80, HTTPS 443, SMTP 25, DNS 53, SSH 22, FTP 20/21
  - Registered Ports : 1024 ~ 49151
    - 특정 상용 앱/서버용 등록 포트
    - (예) MySQL 3306
  - Dynamic/Private Ports : 49152 ~ 65535
    - 클라이언트가 임시로 할당받는 포트
   
### Java 소켓 프로그램
- 서버 소켓
  - 여러 개의 클라이언트로부터 접속 요청을 받아 각각의 클라이언트와 통신할 별도의 서버 측 소켓을 생성
```
__________[클라이언트]_________                  ___________[서버]_____________
|프로그램  ←입출력 스트림→  소켓|-----------------|소켓  ←입출력 스트림→  프로그램|
|_____________________________|                 |____________________________|
```

### TCP를 이용한 클라이언트/서버 통신 순서
```
            [클라이언트]                                                             [서버]
                ⬇️                                                                   ⬇️
  [3. Socket 생성                 ] ↘                               [1. ServerSocket 생성                  ]
                ⬇️                     4.Socket 생성 시 접속 시도                     ⬇️
  [6. Socket으로부터 InputStream과                                 ↘ [2. ServerSocket의 accept() 메소드 대기]
               OutputStream을 구함]                               ↙ 
                ⬇️                                               |                   ⬇️
  [7. InputStream과 OutputStream을     ↖↘                        ↘ [5. 클라이언트가 접속을 시도하면, accept() 
                        이용한 통신]        ↖↘                            메소드가  클라이언트의 Socket을 반환]
                ⬇️                             ↖↘                                   ⬇️
  [9. Socket의 close() 메소드 호출 ]                 ↖↘             [6. Socket으로 부터 InputStream과
                                     8. 연결이           ↖↘                              OutputStream을 구함]
                                     끊어질 때까지            ↖↘                      ⬇️
                                     통신                        ↖↘ [7. InputStream과 OutputStream을 이용한
                                                                                                        통신]
                                                                                      ⬇️
                                                                     [9. Socket의 close() 메소드 호출]
```
- 서버
```
public void runServer() {
  try (ServerSocket server = new ServerSocket(5000)) {
    Socket connection = server.accept(); // 접속 대기 및 소켓 반환
    BufferedReader input = new BufferedReader(
      new InputStreamReader(connection.getInputStream())); // 데이터 수신
    BufferedWriter output = new BufferedWriter(
      new OutpurStreamWriter(connection.getOutputStream())); // 데이터 전송
  } catch (IOException e) {...}
}
```
- 클라이언트
```
try (Socket theSocket = new Socket("www.sungkyul.ac.kr", 80)) { // 서버 접속
  DataInputStream dis = new DataInputStream(theSocket.getInputStream()); // 수신
  // dis.readUTF() 등을 통해 데이터 읽기
} catch (IOException e) {...}
```

### 네트워크 애플리케이션 요구사항
- 성능 지표
  - 데이터 손실, 대역폭, 시간 민감성
- 애플리케이션별 성능 요구사항
- 
| Application | Data Loss | Bandwidth | Time-Sensitive |
|--------------|-----------|-----------|---------------|
| File transfer | No loss | Elastic | No |
| E-mail | No loss | Elastic | No |
| Web documents | No loss | Elastic(few kbps) | No |
| Internet telephony / Video conferencing | Loss-tolerant | Audio : few kbps-1Mbps / Video : 10 kbps-5Mbps | Yes : 100s 0f msec |
| Stored audio / video | Loss-tolerant | Same as above | Yes : few seconds |
| Interactive games | Loss-tolerant | Few kbps-10 kbps | Yes : 100s of msec |
| Instant messaging | No loss | Elastic | Yes and no |

### 애플리케이션이 사용하는 응용 및 전송 계층 프로토콜
- 
| Application | Application Layer Protocols | Underlying Transport Protocols(Port number) |
|--------------|-----------------------------|---------------------------------------------|
| Electronic mail | SMTP(RFC 2821) | TCP(25) |
| Remote terminal | SSH / Telnet(RFC 854) | TCP(SSH : 22, Telnet : 23) |
| Web | HTTP(RFC 2616) | TCP(80) | 
| File transfer | FTP(RFC 959) | TCP(FTP : 20, 21) |
| Streaming multimedia | HTTP(YouTube, Netfilx), RTP | TCP(HTTP : 80, 433) or UDP(RTP : 동적 포트) |
| Internet telephony | SIP, RTP, Proprietary(Zoom, Skype) | Typically UDP(SIP : 5060, RTP : 동적 포트) (or TCP) |
| Domain name | DNS [RFC 1034 / 1035] | Typically UDP(53) |

### 애플리케이션 계층 프로토콜
- 애플리케이션 계층 프로토콜은 다음과 같은 것을 정의한다
  - 프로세스가 언제, 어떻게 메시지를 보내고 응답하는 지에 대한 규칙
  - 메시지 유형
    - (예) 요청, 응답
  - 메시지 문법(syntax)
    - 메시시 내의 각 필드의 구조, 배치, 구별자 구분
  - 메시지 의미(semantics)
    - 메시지 내의 각 필드의 의미
- 표준 프로토콜
  - 상호 연동성을 보장해야 함
  - (예) HTTP(RFC2616), SMTP(RFC2821)
- 사설 프로토콜
  - 특정 기업이 자사 앱 전용으로 비공개 운용
  - (예) Skype
 
### Web과 HTTP
- World Wide Web
  - 인터넷을 통해서 사용자들 간에 정보를 공유할 수 있는 정보 시스템
  - HTML로 구성된 문서를 HTTP를 이용해서 전달
  - 웹 브라우저를 통해서 문서를 읽음
- 웹 페이지
  - 객체들(objects)로 구성
  - 객체는 URI(Uniform Resource Identifier)로 지정할 수 있는 하나의 파일이다
    - HTML파일, JPEG 이미지, GIF 이미지, 오디오 클립 등
  - 대부분의 웹 페이지는 기본 HTML파일과 여러 참조 객체들로 구성된다
    - 기본 HTML파일은 페이지 내부의 다른 객체를 그 객체의 URI로 참조한다
   
### URI(Uniform Resource Identifier)
- URI(RFC 3986)
  - 인터넷에 존재하는 자원(resource)을 식별하기(identifier) 위한 통일된(uniform) 규칙
- URL - Locator
  - 자원이 어디에 있는지 위치를 나타내는 식별자
  - (예) https://example.com/index.html
- URN - Name
  - 자원의 위치와 상관없이 고유한 이름으로 식별
  - (예) urn:isbn:0451450523

### URI 구성
```
scheme://[userinfo@]hos[:post][/path][?query][#fragment]
https://www.google.com:443/search?q=hello&hl=ko
|_________________________|
          URL
|_____________________________________________|
                      URI
```
- scheme : https
  - 프로토콜 : 어떤 방식으로 자원에 접근할 것인가에 대한 약속
- userinfo
  - 사용자 인증 정보(보안상 현재는 사용하지 않음)
- host : www.google.com
  - 도메인명 또는 IP 주소
- port : 443
  - 서버 접속 또는 포트 번호(생략 시 scheme의 기본 포트 적용)
- path : /search
  - 서버 내 자원의 계층적 경로
- query : q=hello&hl=ko
  - ?로 시작 key=value 형태(&로 추가 가능)
- fragment
  - #으로 시작하며, 서버에 전송하지 않고 브라우저 내부 북마크 용으로 사용
  ```
  https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html
  #getting-started.introducing-spring-boot
  ```

### 웹 서버
- HTTP의 서버 측을 구현하며, URL로 각각을 지정할 수 있는 웹 객체들을 가지고 있음
  - Apache, NGINX, MS IIS(Internet Information Server) 등
- 웹 서버의 주요 기능
  - 요청 처리
    - 브라우저가 전송한 HTTP 메서드(GET, POST, PUT, DELETE 등) 요청을 해석하여 정적 파일(HTML, CSS, JS, 이미지) 또는 동적 콘텐츠를 생성하여 변환
  - 응답 제공
    - 처리 결과와 함께 상태 코드를 전송(200 OK, 404 Not Found, 500 Server Error)
  - 세션 및 상태 관리
    - 쿠키(Set-Cookie), 세션, 토큰(JWT) 등을 활용하여 사용자별 맞춤 상태 관리(로그인 유지, 장바구니 등)
  - 콘텐츠 최적화 및 전달
    - 캐시 제어(Cache-Control, ETag), 데이터 압축, CDN 연동을 통한 지연시간 최소화

### 웹 브라우저
- 제어기
  - 사용자 UI 이벤트(주소창, 버튼)수신, 이벤트 루프 스케줄링, 브라우저 내부 모듈 간 흐름 제어
- 클라이언트 프로토콜
  - HTTP / HTTPS, WebSockets 등 애플리케이션 프로토콜 송수신 및 TLS 암호화 모듈 제어
- 해석기
  - HTML / CSS 파싱(DOM/CSSOM 트리 생성) → Render Tree → Layout → Paint 화면 렌더링
  - JavaScript 엔진(Chrome V8, Firefox SpiderMonkey 등)을 통한 동적 스크립트 실행
 
### 웹 서버 접속 및 연결 설정/해제
```
                    사용자
                      |                                                              
                      |  
(1) 서버 주소 제공     |    
(www.korea.co.kr)     |              (3) 연결 설정                    _______ 웹 서버_________  
                      |              (4)~(5) 웹 서비스 진행           |                      |
                      ↓              (6) 연결 해제                    |                      |
                (7) 웹 브라우저  ←----------------------------------→ |   포트 80             |
                    |     ↑                                          |   www.korea.co.kr    |
    www.korea.co.kr | (2) | 211.223.201.17                           |   211.223.201.17     | 
                    ↓     |                                          |______________________|
                    DNS 서버
```

### HTTP(Hypertext Transfer Protocol, RFC 2616, RFC 9110)
- 웹의 응용 계층 프로토콜
  - 클라이언트와 서버 간에 교환되는 메시지 구조와 교환 규약을 정의
- 클라이언트/서버 모델
  - 클라이언트 : 웹 객체를 요청하고, 수신하여 이를 화면에 표출
  - 서버 : 클라이언트 요청에 따라 웹 객체를 찾아서 전송
- TCP를 전송 계층 프로토콜로 사용
  - 클라이언트와 서버 간에 TCP 연결을 설정한 후에 HTTP 메시지를 교환한다
 
### 비상태 프로토콜(stateless protocol)
- 웹 서버는 클라이언트로부터의 요청을 처리한 후에, 해당 처리 결과에 대한 상태 정보를 유지하지 않는다
  - 즉, 특정 클라이언트가 몇 초 후에 같은 객체를 서버로 다시 요청해도 서버는 이전에 해당 객체를 보낸 것을 알지 못하므로 다시 보낸다
- 비상태의 장단점
  - 서버가 다수의 클라이언트 상태 정보를 기억하지 않으므로, 서버 구조가 단순하고 확장성 및 부하 분산에 유리
  - 로그인 유지, 장바구니 등 연속적인 상태 유지가 필요한 서비스 구현이 어려움
- 상태 유지를 위한 기술
  - 쿠키(cookie), 세션(session), 토큰(JWT) 기법을 도입하여 비상태 HTTP 위에 상태 유지 세션을 생성

### HTTP 연결 방식
- 비지속 연결 HTTP(nonpersistent HTTP, HTTP/1.0)
  - 하나의 요청/응답에 대해서 하나의 TCP 연결을 사용한다
    - 웹 페이지 내 객체가 10개면 11번의 TCP 연결/해제 수행(웹페이지-10개 객체)
  - 각 객체 요청 마다 2RTT(round trip time)지연 발생, 서버 OS 메모리 및 TCP 버퍼 오버헤드 가중
- 지속 연결 HTTP(HTTP/1.1)
  - 하나의 TCP 연결을 설정한 후, 여러 HTTP 요청/응답 메시지 전송
    - 서버는 응답 메시지를 송신한 후에도 일정 시간 동안 TCP 연결을 열어 둠
  - Connection : keep-alive 헤더를 이용해 지속 연결을 유지
    - 서버 설정(Timeout, Max Request)에 따라 연결을 유지함
  - 파이프라이닝(pipelining)
    - HTTP 요청에 대한 응답을 기다리지 않고, 여러 HTTP 요청을 보내는 기능
    - 데이터 전송에 시간이 걸리는 경우에 유용
   
### RTT(round-trip time)
- 패킷이 클라이언트에서 서버까지 가고, 다시 클라이언트로 돌아오는 데 걸리는 왕복 시간
- 응답 시간
  - TCP 연결을 개시하는 하나의 RTT
  - HTTP 요구와 HTTP 응답의 첫 번째 바이트가 돌아오기까지의 RTT
  - 파일 전송 시간 = 2RTT + 파일 전송 시간
 
### HTTP 요청 메시지(Request)
- HTTP 요청 메시지 포맷
  - 요청 라인
    - 요청 메소드, URL, HTTP 버전
  - 헤더 라인
    - 헤더 명-값 형태의 메타 데이터
  - 공백 라인(\r\n)
    - 헤더의 끝을 알리는 필수 구분자
  - 엔티티 바디
    - POST/PUT 시 서버로 전송할 페이로드 데이터
- 요청 메소드의 종류(CRUD)
  - Create - POST, PUT
  - Read - GET
  - Update - PUT, PATCH
  - Delete - DELETE
```
[요청 메시지 포맷]
(ASCII 코드로 구성)

|     요청문      |
| (Request Line) |
|________________|
|       헤더      |
|    (Header)    |
|________________|
|    공백 한 줄   |
|________________|
|       바디      |
|      (Body)    |
|________________|
```

### 요청 메시지 예시
```
GET /index.html HTTP/1.1\r\n
Host: www-net.cs.umass.edu\r\n
User-Agent: Firefox/3.6.10\r\n
Accept: text/html,application/xhtml+xml\r\n
Accept-Language: en-us,en;q=0.5\r\n
Accept-Encoding: gzip,deflate\r\n
Accept-Charset: ISO-8859-1,utf-8;q=0.7\r\n
Keep-Alive: 115\r\n
Connection: keep-alive\r\n
\r\n
--------------------------------------------------------------

요청 라인(Request Line) : GET, POST, HEAD commands
- GET /index.html HTTP/1.1
GET : 서버에 데이터를 요청하는 HTTP 메서드
/index.html : 서버에서 요청하는 파일 경로
HTTP/1.1 : 사용하는 HTTP 프로토콜 버전
즉, HTTP/1.1을 사용해서 서버의 index.html 파일을 요청한다는 뜻

헤더 라인(Header Lines) : 브라우저, 언어, 인코딩, 연결 정보 등을 전달
|       헤더       | 의미 |
|      Host       |       요청 대상 서버의 호스트 이름   |
|    User-Agent   |       클라이언트 브라우저 정보       |
|     Accept      | 클라이언트가 받을 수 있는 콘텐츠 형식 |
| Accept-Language |           선호하는 언어             |
| Accept-Encoding |          지원하는 압축 방식         |
| Accept-Charset  |          지원하는 문자 인코딩        |
|   Keep-Alive    |         연결 유지와 관련된 설정      |
|   Connection    |          TCP 연결 유지 여부         |

[예시]
1. Host
Host: www-net.cs.umass.edu
어떤 서버에 요청하는지 나타남

2. User-Agent
User-Agent: Firefox/3.6.10
클라이언트가 Firefox3.6.10 브라우저를 사용한다는 뜻

3. Accept-Language
Accept-Language: en-us, en;q=0.5
영어(미국)를 우선적으로 사용하고, 일반 영어는 상대적으로 낮은 우선순위로 허용한다는 의미
여기서 q는 선호도를 나타내는 값

4. Accept-Encoding
Accept-Encoding: gzip,deflate
서버가 데이터를 gzip 또는 deflate 방식으로 압축해서 보내도 클라이언트가 처리할 수 있다는 뜻

5. Connection
Connection: keep-alive
요청과 응답이 끝나도 TCP연결을 바로 종료하지 않고 유지하겠다는 의미

6. \r\n
\r : Carriage Return(CR) - 커서를 줄의 시작 위치로 이동
\n : Line Feed(LF) - 다음 줄로 이동
```

### HTTP 메서드
- Get method
  - 지정된 URL의 웹 객체/문서를 조회 및 요청할 때 사용
  - URL 끝에 쿼리 형태(?key=value 형식)로 데이터 전달 가능
  ```
  www.somesite.com/animalsearch?monkey&banana
  ```
    - 데이터가 브라우저 주소창 및 히스토리에 노출되며, URL 길이 제약(약 2,048자)
  - 동일한 요청을 여러 번 보내도 서버 상태가 바뀌지 않음(멱등성(idempotent))
- Post method
  - 폼에 데이터 입력, 파일 업로드, 리소스 생성 및 처리 시 사용
  - HTTP 요청 메시지의 Entity Body에 데이터 삽입
  - 주소창에 데이터가 노출되지 않으며, 열람 이력이 남지 않음
  - 대용량 데이터 전송 가능
  - 동일한 요청을 전송할 때마다, 서버에 새로운 리소스가 생성됨(비멱등성(non-idempotent))
- HEAD method
  - GET과 동일하나, Entity Body를 제외하고 헤더(메타데이터) 정보만 요청
  - 파일 수정 일시 확인, 다운로드 전 파일 크기 검증, 링크 유효성 체크 등으로 사용
- PUT method
  - 지정된 URL 위치에 리소스(객체)을 업로드하거나 전체를 덮어씀(update/replace)
  - 여러 번 전송해도 결과가 동일한 멱등적 수정
- Delete method
  - 지정된 URL의 웹 리소스를 삭제
 
### HTTP 응답 메시지(Response)
- 응답 메시지 형식
  - 상태 라인
    - HTTP버전, 상태 코드, 상태 이름
  - 헤더 라인
    - 서버 및 전달되는 데이터에 대한 메타 정보
  - 공백 라인
    - 헤더의 끝을 나타내는 필수 구분자
  - 엔티티 바디
    - 요청한 실제 웹 객체 데이터(HTML 파일, 이미지 비트, JSON 데이터 등)
```
[응답 메시지 포맷]

|     상태문     |
| (Status Line) |
|_______________|
|      헤더      |
|    (Header)   |
|_______________|
|   공백 한 줄   |
|_______________|
|      바디     |
|     (Body)    |
|_______________|
```

### 응답 메시지 예시
```
HTTP/1.1 200 OK
Connection: close
Date: Thu, 06 Aug 1998 12:00:15 GMT
Server: Apache/1.3.0 (Unix)
Last-Modified: Mon, 22 Jun 1998 ...
Content-Length: 6821
Content-Type: text/html

data data data data ...
---------------------------------------------

상태 라인(Status Line) : protocol, status code, status phrase
- 요청 처리 결과 표시
HTTP/1.1 200 OK
HTTP/1.1 : HTTP 프로토콜 버전
200 : 상태 코드(Status Code)
OK : 상태 문구(Status Phrase)
200 OK는 클라이언트의 요청이 성공했다는 의미
예를 들어 브라우저가 index.html을 요청했을 때 서버가 정상적으로 파일을 찾아 응답하면 200 OK를 보낼 수 있음

헤더 라인(Header Lines) : 서버 및 응답 데이터에 대한 부가 정보
Connection: close | 응답 후 TCP 연결 종료
- 서버가 응답을 보낸 뒤 TCP 연결을 종료하겠다는 의미
|         close         |      keep-alive      |
|    응답 후 연결 종료    |   응답 후 연결 유지   |
| 다음 요청에 새 연결 필요 | 기존 연결 재사용 가능 |

Data | 서버가 응답 메시지를 생성한 날짜와 시간

Server | 웹 서버 소프트웨어 정보

Last-Modified | 요청한 자원이 마지막으로 수정된 날짜
Last-Modified: Mon, 22, Jun 1998...
- 서버의 자원이 마지막으로 수정된 시각을 나타냄

Content-Length | 응답 본문의 크기(바이트)
Content-Length: 6821
- 서버가 전송하는 응답 본문의 크기가 6,821바이트라는 뜻
HTTT응답 메시지 전체 크기가 아니라 본문 크기를 의미함

Content-Type | 응답 본문의 데이터 형식
Content-Type: text/html
- 서버가 보내는 데이터의 형식이 HTML 문서라는 의미
(예)
text/html : HTML 문서
text/plain : 일반 텍스트
image/jpeg : JPEG 이미지
application/json : JSON 데이터

공백 라인(Blank Line) : 헤더의 끝을 표시

엔티티 바디(Entity Body) : 실제 전송되는 데이터
data data data data ...
- 응답 메시지의 부분으로, 클라이언트가 요청한 실제 데이터가 들어 있음
예를 들어 HTML 파일을 요청했다면 이 부분에 HTML 문서 내용이 들어감

HTTP 요청과 응답 비교
                    HTTP Request
 클라이언트 -------------------------------→ 서버
[웹 브라우저] ←--------------------------- [웹 서버]
                    HTTP Response
            -HTTP/1.1 200 OK + HTML 데이터-
```

### 상태 코드의 종류
- 1XX(Informational) : 요청 수신 후 처리 중
- 2XX(Success) : 성공
  - 200 OK : 요청 성공 및 정상 응답
  - 201 Created : 요청 성공으로 새 리소스 생성 완료
  - 202 Accepted : 요청이 수신되었으나, 비동기 처리 중
- 3XX(Redirectional) 리다이렉션
  - 301 Moved Permanently : 요청한 객체가 새 URL로 영구 이동됨
    - 새로운 URL은 응답메시지의 Location : 헤더에 나와 있음
  - 304 Not Modified : 캐시된 사본이 최신 상태임(본문 미전송으로 대역폭 절감)
- 4XX(Client Error) : 클라이언트 오류
  - 400 Bad Request : 요청 메시지 문법 오류
  - 401 Unauthorized : 인증 필요(요청의 실행에 필요한 권한이 없음)
  - 403 Forbidden : 접근 권한 거부
  - 404 Not Found : 요청한 리소스가 서버에 없음
- 5XX(Server Error) : 서버 오류
  - 500 Internal Server Error : 서버 내부 로직 오류
  - 501 Not Implemented : 서버가 요청 메서드를 지원하지 않음
  - 503 Server Unavailable : 서버가 일시적으로 요청을 처리할 수 없음(서버 과부하, 점검 등)
  - 505 HTTP Version Not Supported : 서버가 요청에 사용된 HTTP 버전을 지원하지 않음
 
### 웹의 상태 유지 기법 : 쿠키, 세션, 토큰
- 비상태 프로토콜은 HTTP 상에서 사용자 식별, 로그인 유지, 장바구니 등 상태를 관리할 필요가 있다
- 쿠키(Cookie - RFC 6265)
  - 서버가 응답 헤더(Set-Cookie)로 전달한 작은 데이터 조각을 브라우저 측에 저장
  - 이후 동일 서버로 재요청 시 브라우저가 Cookie : 헤더에 쿠키를 넣어 전송
- 세션(Session)
  - 사용자 상태 데이터는 서버 메모리/DB에 저장하고, 클라이언트에게는 무작위 Session ID를 쿠키로 발급
  - 보안성은 높으나 접속자 증가 시 서버 메모리 부하 가중
- 토큰 기반 인증(JWT - JSON Web Token, RFC 7519)
  - 사용자 인증 정보를 암호화/서명한 토큰을 클라이언트에 발급
  - 클라이언트는 Authotization:Bearer<token> 헤더에 담아 전송
  - 서버 측 세션 저장소가 필요 없음
 
### 쿠키를 이용한 사용자 상태 유지
- HTTP 응답 메시지의 Set-Cookie : 헤더 라인
- HTTP 요청 메시지의 Cookie : 헤더 라인
- 사용자 브라우저가 관리하는 쿠키 파일
- 웹 사이트의 백엔드(back-end) DV

### 쿠키의 활용
- 쿠키가 제공하는 이점
  - 사용자 인증 : 웹 메일 로그인 상태 유지
  - 쇼핑 카트 : 구매 상품 목록 지속 보관
  - 개인화 및 추천 : 과거 방문 이력 기반 상품 추천
  - 사용자 세션 상태 관리
- 쿠키의 프라이버시 및 보안 문제
  - 타사 광고 쿠키를 통해 사용자의 전 사이트 방문 기록 추적 가능
  - 쿠키 수집 전 사용자 동의 필요
 
### 웹 캐시(web cache, proxy server)
- 원(original) 웹 서버를 대신하여 HTTP 요청에 응답하는 네트워크 개체
- 자체 저장 디스크를 보유하여 최근 요청된 객체의 사본을 저장/관리
- 클라이언트와 서버의 중간자(client+server) 역할을 동시에 수행
- Forward Proxy
  - 클라이언트 측(기업, 학교 내부망)에 위치하여 외부 인터넷 접속 제어, 보안, 캐싱 수행
- Reverse Proxy
  - 원 웹 서버 앞에서 위치하여 로드 밸런싱, 보안, SSL 종단, 캐싱 수행
 
### 웹 캐시 처리 절차
- 1. 브라우저가 엡 캐시와 TCP 연결을 맺고, 객체를 요청하는 HTTP 메시지를 웹 캐시로 전송한다
  2. 웹 캐시 저장 디스크에 최신 사본이 존재하면, 웹 캐시는 즉시 클라이언트로 HTTP 응답 메시지를 전송한다
  3. 웹 캐시가 객체를 가지고 있지 않으면, 웹 캐시는 원 서버로 TCP 연결을 맺고 해당 객체를 원 서버에 요청한다
  4. 요청을 받은 원 서버는 웹 캐시에 HTTP 응답 메시지를 전송한다
  5. 원 서버로부터 응답 메시지를 수신하면, 웹 캐시는 디스크에 객체의 사본을 저장한 후 클라이언트로 응답 메시지를 전송한다
 
### 웹 캐시의 필요성
- 클라이언트 요구에 대한 응답 시간을 줄일 수 있다
  - 원 서버보다 물리적으로 훨씬 가까운 웹 캐시가 즉시 응답하므로 대기 시간 최소화
  - 클라이언트-원 서버의 대역폭이 클라이언트-웹 캐시의 대역폭 대비 매우 작을 때 더욱 효과적
- 기관의 외부 연결 인터넷 접속 회선 상의 웹 트래픽 유입량을 대폭 감소시켜 회선 증설 비용을 줄일 수 있다
- 콘텐츠 제공자의 원 서버가 지속 회선이거나 과부하 상태라도, 캐시 인프라를 통해 고속으로 컨텐츠 분배가 가능하다

### 웹 캐시의 효과
- 가정
  - 평균 웹 객체 크기 : 100K bits
  - 브라우저의 평균 요청율 : 15/sec
  - 브라우저로 들어오는 평균 데이터율 : 1.50Mbps
  - 기관 에지 라우터에서의 원 서버까지의 RTT : 2sec
  - 기관 접속 회선 대역폭 : 1.54Mbps
- 결과
  - LAN 구간 이용률 = 0.15%
  - 접속 회선 이용률 = 97.4%
  - 총 지연시간 = Internet delay + access delay + LAN delay = 2sec + minutes + usecs
- 가능한 해법1
  - 접속 회선 대역폭 증설 : 1.54Mbps → 154Mbps
- 결과
  - LAN 구간 이용률 = 0.15%(동일)
  - 접속 회선 이용률 = 1%
  - 총 지연시간 = Internet delay + access delay + LAN delay = 2sec + msecs + msecs
  - 회선 임대료 폭증
- 가능한 해법2
  - 내부에 웹 캐시를 설치
  - 캐시 적중율 0.4 가정
    - 40% 요청은 웹 캐시가 즉시 응답, 60%는 원 서버로 요청
- 결과
  - 접속 회선 유입 트래픽 양 = 0.6 * 1.50
    - Mbps = 0.9Mbps
      - utilization = 0.9 / 1.54 = 0.58
  - 총 지연시간
    - = 0.6 * (원 서버 지연) + 0.4 * (웹 캐시 지연)
    - = 0.6 * (2.01) + 0.4 * (~msecs) = ~1.2secs
    - 154Mbps 회선 증설 방식보다 빠르고 비용도 훨씬 저렴
   
### 조건부 GET
- 캐시의 최신성 보장 기법
- 동작 방식
  - 최초 요청 : 원 서버가 응답에 리소스의 최종 수정 일시를 담아 전송(Last-Modified : <data>)
  - 재요청(조건부 GET) : 캐시 / 브라우저가 헤더에 수정 날짜를 동봉하여 전송(IF-modified-since : <date>)
  - 서버 판단 및 응답
    - 변경 없음 : 서버가 본문 데이터 없이 헤더만 회신(HTTP/1.1 304 Not Modified)
    - 변경 있음 : 서버가 최신 데이터 전송

### HTTP/2 (RFC 9113)
- 통신 속도 개선을 위해서 구글이 제안한 SPDY를 기반으로 2015년 IETF에서 표준 개발
- 스트림 기반 다중화
  - 하나의 TCP 연결에서 스트림(stream)이라는 가상의 통신 경로를 여러 개 생성하고, 각 스트림 안에서 HTTP 요청/응답 메시지를 전달
  - 각 스트림이 독립적이므로 응답 대기 지연을 피할 수 있음
- 바이너리 형식 사용
  - 응답/요청 메시지를 바이너리 형식의 프레임들로 분할하여 전송
- 헤더 압축
  - 이전 메시지에서 중복된 부분을 제외하고 다른 부분만 압축하여 전송
- 서버 푸시
  - HTTP 요청 메시지를 기반으로 웹서버가 필요한 리소스(CSS, JS 등)를 파악하여 사전에 웹브라우저에 전송함
 
### HTTP/3 (RFC 9000, 9114)
- TCP의 한계로 인한 문제를 해소하고자 2022년 IETF에서 표준화
  - 연걸 설정 지연(TCP + TLS 연결), 전송 계층 HOL 블록킹 등
- 전송 계층 프로토콜로 QUIC(Quick UDP Internet Connection)를 사용
  - 연결 설정 과정 간소화(TLS 내장)
  - 신뢰성을 위한 패킷 재전송, 혼잡 제어, 흐름 제어 등 제공
 
### DNS : Domain Name System (RFC 1034, 1035)
- 사람의 식별자
  - 이름, 주민등록번호, 여권번호
- 인터넷 호스트 / 라우터의 식별자
  - 호스트 이름(Host Name)
    - 사람이 기억하기 쉬운 문자로 구성
    - (예) www.yahoo.com(https://www.yahoo.com)
  - IP 주소(IP adress)
    - 라우터가 데이터그램을 라우팅하기 위해 사용하는 고정 길이 주소(32비트 IPv4 / 128비트 IPv6)

### DNS(Domain Name System)
- 호스트 이름을 IP주소로 변환(디렉토리 서비스)
- DNS 서버들의 계층 구조로 구현된 분산 데이터베이스
- 호스트가 분산 데이터베이스로 질의하도록 허락하는 응용 계층 프로토콜
- DNS 프로토콜은 UDP 상에서 수행되고, 포트번호 53을 사용
  - 연결 설정 지연을 피하고, 짧은 질의/응답을 신속히 처리하기 위해
- 명령 프롬포트에서 nslookup(또는 dig, unix)명령으로 호스트 이름에 대한 IP 주소를 알아낼 수 있다

### DNS가 제공하는 서비스
- 호스트 이름을 IP 주소로 변환
  - (예) 브라우저(HTTP 클라이언트)가 URL www.someschool.edu/index.html을 요청할 때 ... 사용자 호스트는 해당 웹 서버의 IP 주소를 알아야함
- 호스트 별칭(aliasing)
  - 복잡한 정식 이름 대신 기억하기 쉬운 별칭 제공
  - (예) relay1.west-coast.enterprise.com(정식 이름)
         enterprise.com, www.enterprise.com(별칭)
- 메일 서버 별칭
  - 이메일 주소의 도메인을 실제 메일 전송 전용 서버로 매핑
- 부하 분산
  - 하나의 정식 호스트 이름에 여러 IP 주소 집합을 매핑하고, 질의 시 주소 순서를 회전시켜 전송함으로써 중복 웹 서버들 간에 트래픽을 분산시킴

### 호스트 이름을 IP 주소로 변환하는 과정
```

       [사용자(User)]
              │
              │ ① 호스트 이름 입력
              ▼
┌────────── 응용 계층(Application Layer) ──────────┐
│                                                  │
│  ┌──────────────┐  ② 호스트 이름  ┌───────────┐   │
│  │ 파일 전송     │ ──────────────→ │ DNS      │   │
│  │ 클라이언트    │                 │ 클라이언트│   │
│  │              │ ←────────────── │          │   │
│  └──────────────┘  ⑤ IP 주소      └───────────┘  │
│         │                             │    ▲     │
└─────────┼─────────────────────────────┼────┼─────┘
          │                             │    │
          │                        ③ 질의   ④ 응답
          │                             │    │
          │                             ▼    │
          │                       ┌─────────────┐
          │                       │ DNS 서버    │
          │                       └─────────────┘
          │
          │ ⑥ IP 주소 전달
          ▼
    [전송 계층(Transport Layer)]
-------------------------------------------------------------------
[동작 순서]

1. 사용자 → 파일 전송 클라이언트 : 사용자가 호스트 이름을 입력한다
2. 파일 전송 클라이언트 → DNS 클라이언트 : 호스트 이름을 전달한다
3. DNS 클라이언트 → DNS 서버 : 호스트 이름에 해당하는 IP 주소를 질의(Query)한다
4. DNS 서버 → DNS 클라이언트 : IP 주소를 응답(Response)한다
5. DNS 클라이언트 → 파일 전송 클라이언트 : 변환된 IP 주소를 전달한다
6. 파일 전송 클라이언트 → 전송 계층 : IP 주소를 전달하여 통신에 사용한다
```

### DNS 구조
- DNS가 단일 중앙 집중 데이터베이스가 아닌 이유?
  - 단일 장애점, 트래픽 집중, 원 거리로 인한 지연 유발, 유지 관리, 확장성 부족
- 계층적인 분산 데이터베이스
```

                    ┌──────────────────────┐
                    │   Root DNS Servers   │  ← Root
                    └──────────┬───────────┘
                               │
             ┌─────────────────┼─────────────────┐
             │                 │                 │
             ▼                 ▼                 ▼
    ┌────────────────┐ ┌────────────────┐ ┌────────────────┐
    │ .com DNS 서버  │ │ .org DNS 서버  │ │ .edu DNS 서버  │
    └───────┬────────┘ └───────┬────────┘ └───────┬────────┘
            │                  │                  │
            │                  │                  │
      ┌─────┴─────┐            │            ┌─────┴─────┐
      │           │            │            │           │
      ▼           ▼            ▼            ▼           ▼
  ┌─────────┐ ┌──────────┐ ┌─────────┐ ┌─────────┐ ┌───────────┐
  │yahoo.com│ │amazon.com│ │ pbs.org │ │ nyu.edu │ │ umass.edu │
  │ DNS 서버 │ │ DNS 서버 │ │DNS 서버 │ │ DNS 서버 │ │ DNS 서버  │
  └─────────┘ └──────────┘ └─────────┘ └─────────┘ └───────────┘

       ↑                 ↑                    ↑
  Authoritative     Authoritative       Authoritative
     DNS 서버          DNS 서버            DNS 서버
-------------------------------------------------------------------------
[계층 구분]

Root : 루트 DNS 서버
Top Level Domain(TLD) : .com, .org, .edu DNS 서버
Authoritative : yahoo.com, amazon.com, pbs.org, nyu.edu, umass.edu의 권한 있는 DNS 서버
```

### 계층적인 DNS 구조
- 루트 DNS 서버
  - 인터넷 도메인 주소 체계의 최상위 서버
    - 전세계적으로 13개의 루트 DNS 서버(logical)가 있으며, 실제 1980개 이상의 물리 인스턴스로 구성
  - TLD 서버의 위치 정보를 제공
- 최상위 레벨 도메인(TLD) 서버
  - com, org, net, edu 등과 같은 상위 계층 도메인과 kr, uk, fr, ca 등과 같은 국가의 상위 계층 도메인 관리
  - 해당 도메인 하위의 책임 서버 IP 제공
- 책임 DNS 서버
  - 특정 기관이 소유한 호스트 이름과 IP 주소의 실제 매핑 레코드를 관리
  - 가용성 보장을 위해 기본 책임 DNS 서버와 조고 책임 DNS 서버를 운영

### 로컬 DNS 서버
- 엄격한 계층 구조에 속하지 않으며, 클라이언트를 대신해 주소를 찾아주는 대리인(proxy) 역할
- 호스트가 DNS 쿼리를 생성하면, 그 쿼리는 로컬 DNS 서버로 전달된다
  - 로컬 DNS 서버는 프록시로 등장하며, DNS 계층 구조에 따라서 쿼리를 전달한다
- 각 ISP(지역 ISP, 기관, 대학 등)는 로컬 DNS 서버(default name server)를 갖는다
- 공용 퍼블릭 DNS(Public DNS Resolvers)
  - 통신사 로컬 DNS 외에 빠른 응답과 보안을 위해 제공되는 공용 서버
  - Google Public DNS(8.8.8.8 / 8.8.4.4)
  - Cloudflare DNS(1.1.1.1 / 1.0.0.1)
 
### DNS 질의 방식
- 호스트 cse.nyu.edu가 gaia.cs.umass.edu의 IP 주소를 찾는 과정
- 재귀적 질의
  - 질의를 받은 DNS 서버가 직접 상위/하위 서버들을 탐색하여 최종 주소를 찾아서 수신자에게 응답
  - 루트/TDL 서버에 부하 가중
- 반복적 질의
  - 로컬 DNS가 루트 DNS, TDL DNS, 책임 DNS에 번갈아 가면서 질의 수행
  - 루트/TLD 서버는 과부하 방지를 위해 반복적 질의/응답만 수행
 
### DNS 캐싱 및 보안
- DNS 캐싱
  - 지연 성능 향상과 네트워크 상에서 DNS 메시지 수를 줄이기 위해서
  - 질의 사슬에서 DNS 서버가 DNS 응답을 받으면, 그 응답에 포함된 정보를 로컬 메모리에 저장한다
    - 어느 정도 시간이 지나면 해당 정보는 삭제된다
- DNS의 보안 취약점 해결
  - UDP 상에서 동작하는 DNS는 평문으로 전송되므로 보안에 취약
  - DNS over TLS(RFC 7858)
    - TLS를 사용해 DNS 쿼리를 암호화
    - TCP 853 전용 포트를 사용하므로 관리자가 DNS 트래픽임을 쉽게 식별 가능
  - DNS over HTTPS(RFC 8484)
    - HTTPS를 사용해 암호화를 하므로 표준 웹 트래픽과 동일하게 처리 가능
    - DNS → HTTP → TLS → TCP로 패킷화되어 오버헤드가 큼
   
### 비디오 스트리밍과 CDN
- 인터넷 트래픽의 80% 이상이 비디오 스트리밍
- 도전 과제
  - 수억 명의 동시 접속자에게 대용량 미디어를 어떻게 안정적으로 제공할 수 있는가
  - 사용자의 다양한 접속 환경에 어떻게 대응할 수 있는가
- 해결 방안은 분산형 응용 계층 인프라
  - CDN(Content Distribution Networks)
  - 적응형 스트리밍(DASH)
- 멀티미디어 애플리케이션의 종류
  - 저장형 스트리밍
  - 대화형 음성/영상(양방향 통화)
  - 실시간 라이브 스트리밍
 
### 저장형 비디오 스트리밍
- 서버에 저장된 동영상 파일을 인터넷을 통해서 다운로드 받으면서 재생
- 주요 과제
  - 서버-클라이언트 간에 대역폭이 시간에 따라 지속적으로 변한다
    - 가정 내 네트워크, 접속망, 코어망, 서버 상태에 따라
  - 네트워크 혼잡으로 인한 패킷 지연 및 손실이 발생하며 화면이 멈추는 버퍼링 현상 발생

### 클라이언트 버퍼링과 재생 지연
- 클라이언트는 수 초 분량의 데이터를 애플리케이션 버퍼에 저장한 후에 재생 시작
  - 지연 시간 변동(jitter) 상쇄 및 일시적 대역폭 저하 흡수
```

           클라이언트 버퍼링과 재생 지연

누적 데이터량 (Cumulative Data)
    ▲
    │
    │         ┌──┐
    │      ┌──┘  └────── ① 비디오 녹화
    │    ┌─┘              (30 frames/sec)
    │  ┌─┘
    │ ┌┘                 ┌──┐
    │┌┘               ┌──┘  └──── ② 비디오 전송
    ││              ┌─┘
    ││            ┌─┘
    ││          ┌─┘            ┌──┐
    ││        ┌─┘           ┌──┘  └── ③ 비디오 수신 및 재생
    ││      ┌─┘           ┌─┘          (30 frames/sec)
    ││    ┌─┘           ┌─┘
    ││  ┌─┘           ┌─┘
    ││┌─┘           ┌─┘
    └┴─────────────────┼───────────────────→ 시간
                       │
                       │ 재생 시작 시점
                       ▼
              [클라이언트 버퍼링 완료]
              [비디오 재생 시작]

  ① 비디오 녹화 (Video Recorded)
           │
           ▼
  ② 비디오 전송 (Video Sent)
           │
           │ 네트워크 지연 (Network Delay)
           ▼
  [클라이언트 버퍼에 데이터 저장]
           │
           │ 재생 지연 (Playback Delay)
           ▼
  ③ 비디오 수신 및 재생 (Video Played)
-------------------------------------------------------------

버퍼링(Buffering) : 클라이언트가 수 초 분량의 비디오 데이터를 미리 저장하는 과정
재생 지연(Playback Delay) : 비디오 데이터가 도착해도 일정 시간 기다렸다가 재생하는 것
지터(Jitter) : 네트워크에서 데이터 전달 지연 시간이 변동하는 현상

왜 버퍼링을 할까?
- 네트워크 속도가 일시적으로 느려지거나 데이터 도착 시간이 일정하지 않아도 비디오가 끊기지 않도록 하기 위해서임
```
```
          클라이언트 버퍼링과 재생 지연

누적 데이터량 (Cumulative Data)
    ▲
    │
    │              ┌────── ① 비디오 전송
    │           ┌──┘         (일정한 비트율)
    │         ┌─┘
    │       ┌─┘
    │     ┌─┘                 ┌──── ② 비디오 수신
    │   ┌─┘               ┌──┘       (네트워크 지연 변동)
    │ ┌─┘               ┌─┘
    │┌┘              ┌──┘        ┌──── ③ 비디오 재생
    ││             ┌─┘       ┌──┘       (일정한 비트율)
    ││           ┌─┘       ┌─┘
    ││         ┌─┘       ┌─┘
    ││       ┌─┘       ┌─┘
    ││     ┌─┘       ┌─┘
    ││   ┌─┘       ┌─┘
    └┴───────────────────────────────────→ 시간
     t₀    t₀+Δ    t₁     t₂    t₃

     ① 비디오 전송
            │
            │ 가변적인 네트워크 지연
            ▼
     ② 클라이언트 비디오 수신
            │
            │ 버퍼에 데이터 저장
            │ (Buffered Video)
            ▼
     ③ 클라이언트 비디오 재생

     ※ 수신과 재생 사이의 시간 차이
        = 클라이언트 재생 지연
          (Client Playout Delay)
-----------------------------------------------------------------------

|                 구분                  |                   의미                   |
-----------------------------------------------------------------------------------
| Constant Bit Rate Video Transmission |         일정한 비트율로 비디오 전송         |
|        Variable Network Delay        |       네트워크 지연 시간이 일정하지 않음     |
|        Client Video Reception        |       클라이언트가 비디오 데이터를 수신      |
|            Buffered Video            |     수신했지만 아직 재생하지 않은 데이터     |
|         Client Playout Delay         | 클라이언트가 재생을 시작하기 전 기다리는 시간 |
|    Constant Bit Rate Video Playout   |         일정한 비트율로 비디오 재생         |
```

### 적응형 HTTP 스트리밍
- DASH : Dynamic Adaptive Streaming over HTTP
- 서버
  - 비디오 파일을 수 초 길이의 청크(chunk)단위로 분할
  - 각 청크를 다양한 화질/비트율(예 : 720p, 1080p, 4K)로 중복 인코딩하여 저장
  - 각 화질별 청크의 URL 정보를 담은 매니페스트(manifest)파일 제공
- 클라이언트
  - 주기적으로 서버-클라이언트 간 현재 가용 대역폭을 수시로 측정
  - 매니페스트 파일을 참조하여 현재 속도에서 감당 가능한 최고 화질의 청크를 동적으로 요청
- 적응형 스트리밍 규격
  - MPEG-DASH(ISO/IEC 23009-1)
    - 국제 표준 : YouTube, Netflix 등 적용
  - HLS(HTTP Live Streaming - RFC 8216)
    - Apple 주도 규격 : 높은 OTT 글로벌 점유율
   
### Content Distribution Networks(CDN)
- 수 백만 개의 비디오 중에 선택된 콘텐츠를 수 십만 명의 동시 접속자에게 어떻게 전달할 것인가?
- 방안 1 : 단일 대형 데이터센터(메가 서버)를 구축하여 운영
  - 단일 장애점
  - 중복 전송 낭비
  - 네트워크 병목
  - 긴 경로 지연
- 방안 2 : 지리적으로 분산된 다수 지점에 콘텐츠 복사본을 저장하여 서비스를 제공(CDN)
- Enter Deep
  - 전 세계 수천 개 접속 네트워크 내부 깊숙이 CDN 서버 클러스터를 배치
  - 사용자에게 가까이 위치하여 홉 수와 지연 시간 최소화
  - 고도로 분산된 수천 개 지점의 서버 클러스터를 관리, 유지하는 비용 증가
  - (사례) Akamai(1700개 이상 ISP에 설치)
- Bring Home
  - 보다 적은 수(수십 개)의 대형 서버 클러스터를 주요 인터넷 교환 노드 및 대형 POP 인근에 구축
  - 서버 클러스터 수 감소로 유지보수 및 관리 비용 절감
  - Enter Deep 대비 지연 시간 및 처리율 성능이 상대적으로 낮음
  - (사례) Limelight
 
### CDN 노드의 콘텐츠 저장 및 제공
- CDN 노드(서버 클러스터)는 전 세계 비디오의 복사본을 사전에 100% 저장할 필요가 없다
- 주문형 캐싱 방식
  - 가입자가 가장 가까운 CDN 노드로 콘텐츠를 요청한다
  - CDN 노드에 해당 콘텐츠가 없으면, 중앙 원 서버로부터 콘텐츠를 전송받아 가입자에게 서비스함과 동시에 디스크에 복사본을 캐싱한다
  - 네트워크 경로가 혼잡하면 다른 CDN 노드에 요청할 수도 있다
 
### CDN 기반 CDN 콘텐츠 제공
- Bob(client) requests video http://video.netcinema.com/6Y7B23V
  - video stored in CDN at http://KingCDN.com/NetC6y&B23V
```

             DNS 기반 CDN 콘텐츠 제공

                   ┌──────────────┐
                   │ Bob (Client) │
                   │   사용자     │
                   └──────┬───────┘
                          │
          ┌───────────────┼────────────────┐
          │               │                │
          │ ① URL 획득    │ ② DNS 질의     │ ⑥ 비디오 요청
          ▼               ▼                ▼
  ┌─────────────┐  ┌─────────────┐  ┌──────────────┐
  │ netcinema   │  │ 로컬 DNS    │  │ KingCDN 서버 │
  │ .com        │  │ 서버        │  │ (비디오 저장)│
  └──────┬──────┘  └──────┬──────┘  └──────────────┘
         │                │                ▲
         │                │                │
         ▼                │                │
  ┌────────────────┐      │                │
  │ netcinema의    │      │                │
  │ 권한 DNS 서버  │      │                │
  └──────┬─────────┘      │                │
         │                │                │
         │ ③ CDN URL 반환│                │
         └────────────────►                │
                          │                │
                          │ ④ CDN DNS 질의│
                          ▼                │
                 ┌───────────────────┐     │
                 │ KingCDN의         │     │
                 │ 권한 DNS 서버     │     │
                 └─────────┬─────────┘     │
                           │               │
                           │ ⑤ IP 주소 반환│
                           └───────────────┘

       ⑥ Bob → KingCDN 서버
          HTTP로 비디오 요청 및 스트리밍
------------------------------------------------------------

[동작 순서]

1. Bob → netcinema.com : 웹 페이지에서 비디오 URL을 획득
2. Bob → 로컬 DNS : video.netcinema.com의 주소를 질의
3. netcinema 권한 DNS : 실제 비디오가 저장된 KingCDN의 URL을 반환
4. 로컬 DNS → KingCDN 권한 DNS : CDN 서버의 IP 주소를 알아내기 위해 질의
5. KingCDN 권한 DNS → 로컬 DNS : 비디오를 제공할 KingCDN 서버의 IP 주소를 반환
6. Bob → KingCDN 서버 : HTTP로 비디오를 요청하고 스트리밍을 받음
```

### 요약
- 애플리케이션 아키텍처
  - 클라이언트-서버 vs P2P
- 앱 서비스 요구사항
  - 손실 민감도, 대역폭 요구 특성, 시간 지연 민감도
- 소켓 및 통신 기초
  - 프로세스 식별자(IP + Port), 소켓 API
- HTTP
  - 웹 응용 프로토콜, 비상태성, 지속 연결, 쿠키/세션/토큰 상태 관리, 웹 캐시/프록시 및 조건부 GET
  - HTTP/1.1, HTTP/2, HTTP/3
- DNS
  - 계층적 분산 데이터베이스, UDP, 반복적/재귀적 질의 및 캐싱
- 미디어 전송
  - 적응형 스트리밍(DASH), CDN 구조 및 DNS 리디렉션 메커니즘

##### ✍️ 작성자: 박지안
##### 🗓️ 작업일: 2026-10-09
