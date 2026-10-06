# 📚 컴퓨터 네트워크 (Computer Network)
## 📘 1장 컴퓨터 네트워크와 인터넷 pg 10부터

### 데이터 통신
- 데이터와 신호 : digital vs analog
  - 데이터 : 기기 또는 매체에 저장된 정보
  - 신호 : 특정 형태(electric, electromagnetic, optical)로 데이터를 표현한 것
- 한 기기에 저장된 데이터를 다른 기기로 효과적으로 전송하기 위해서는 신호로 변환해야 한다
```
 Data    Signal               Data   
-----→[]←----------------→[]←-----
                  Medium

 [Data]                  [Signal]
Analogue←-→[Telephone]←-→Analogue
 Digital←-→[Modern]←-→Analogue
Analogue←-→[CODEC]←-→Digital 
 Digital←-→[Digital Transmitter]←-→Digital
```
- 데이터 전송 시 고려사항
  - 감쇄(attenuation), 왜곡(distortion), 잡읍(noise)

### 정보의 전송 과정
```
                                                     [라인 코딩]  기저대역전송
                                                                 NRZ, RZ, Bipolar
송신    [A/D 변환]---→ [소스 코딩]---→ [채널 코딩]---→ [(변조)]------------|
          PCM         데이터 압축     오류 검출/정정   아날로그 매체 전송   |
          샘플링       JPEG, MPEG     parity bit      ASK/FSK/PSK        |
          양자화       MP3            CRC             QPSK               |
          부호화                                                         |
                                                                        |
                                                                        |
수신    [D/A 변환] ←---[역소스 코딩] ←---[역채널 코딩] ←---[(복조)]←-------|
```

### 디지털 데이터 → 디지털 신호 변환 : 라인 코딩
- 이진 비트 스트림을 디지털 통신 채널에 적합한 전기적/광학적 디지털 파형으로 변환

### 디지털 데이터 → 아날로그 신호 변환 : 변조
- 변환 기법들
  - ASK(Amplitude Shift Keying)
  - FSK(Frequency Shift Keying)
  - PSK(Phase Shift Keying)
  - QAM(Quadrature Amplitude Modulation)

### 물리 계층(Physical layer)
- 한 기기에서 다른 기기로 비트 스트림의 전송을 담당
  - 전송 매체의 물리적, 전기적 특성 및 신호 변환 담당
- 다양한 물리 매체가 전송에 사용된다
  - 대역폭, 지연, 비용, 설치의 용이성, 유지 보수 등의 고유한 특성을 가짐
  - 유도 매체, 유도되지 않은 매체
- 유도 매체(guided media)
  - 고체 매체를 통해서 신호가 전달
  - (예시) 꼬임쌍 동선, 동축케이블, 광섬유
- 비유도 매체(unguided media)
  - 자유 공간을 통해서 신호가 전달
  - (예시) 라디오파, 마이크로파, 위성
 
pg15부터
