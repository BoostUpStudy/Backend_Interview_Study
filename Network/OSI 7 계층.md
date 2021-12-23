## OSI(Open Systems Interconnection) 모델이란?

컴퓨터 시스템이 네트워크를 통해 통신하며 사용하는 7개의 계층으로 국제 통신 표준 규약

![OSI 7계층 데이터 전송 흐름](https://user-images.githubusercontent.com/74395748/147263985-fd2fdc25-c8a9-4ee0-a121-8976d37da4b3.png)

OSI 7계층 데이터 전송 흐름

## 기능

### [**Layer 7] 응용 계층 (Application Layer)**

OSI 모델의 최상위 계층으로 통신의 최종 목적지로 다양한 프로토콜

**기능**

- Network Virtual Terminal
어플리케이션은 원격 호스트의 에뮬레이션을 생성하여 사용자가 원격 호스트에 log on 하는 기능
사용자의 컴퓨터 ↔ 소프트웨어 터미널 ↔ 호스트 형식의 통신
- Directory Service
다양한 전역 정보에 대한 엑세스 기능
- File Transfer Access and Management(FTAM)
파일에 엑세스하고 파일을 관리하는 표준 메커니즘
원격 컴퓨터의 파일에 엑세스 및 관리, 검색 기능
- Mail Service

**단위 - Data**

**키워드**

> HTTP, FTP, SMTP, Telnet 등
> 

### [Layer 6] 표현 계층 (Presentation Layer)

응용 계층으로부터 전송 받거나 전송해야되는 데이터를 인코딩, 디코딩 하는 계층
암호화 복호화 작업도 해당 계층에서 이루어짐

**기능**

- 번역
네트워크에 필요한 형식과 어플리케이션의 데이터의 형식 변환 기능
송신 데이터 → 비트 스트림 (인코딩)
수신 데이터 → 문자 및 숫자 (디코딩)
- 암호화
송신기에서 암호화, 수신기에서 복호화 작업을 수행하는 기능
- 압축
대역폭을 줄이기 위해 데이터를 압축하는 기능
오디오, 비디오, 텍스트 등 멀티미디어 전송에 중요하며 0으로 전송되는 비트의 수를 줄이는 역할

**단위 - Data**

**키워드**

> ASCII, JPEG, MPEG 등
> 

### [Layer 5] 세션 계층 (Session Layer)

통신하는 호스트 사이 세션 설정 및 유지 및 동기화를 처리하는 계층
**기능**

- 동기화
통신하는 메세지 스트림에 대해 동기화 지점으로 체크포인트를 추가하며 세션이 중단되면 체크포인트를 통해 데이터 전송을 재개할 수 있는 기능
- 토큰 관리
각 사용자가 중요한 작업을 동시에 엑세스하는 것을 방지하기 위한 기능
- Dialog Control
두 시스템이 반이중, 전이중으로 서로 통신을 시작할 수 있도록 설정하는 기능

**단위 - Data**

### [Layer 4] 전송 계층 (Transport Layer)

송신 과정은 상위 계층에서 전달받은 데이터를 더 작은 조각(Segment, Databram)으로 분할하여 네트워크 계층으로 전달하며 수신 과정은 분할된 조각(Segment, Databram)을 재조립하는 프로세스간 논리적 통신을 수행하는 계층
데이터가 잘못 수신되었는지 확인하며 다시 요청하는 오류 제어 기능을 수행

**기능**

- Service Point Addressing
해당 Layer header 에 서비스 포인트 주소인 포트번호를 포함하여 올바른 프로세스로 메세지를 전달하는 기능
- 분할 및 재조립
메세지는 시퀀스 번호가 포함되어 있는 세그먼트 형태로 분할
세그먼트의 시퀀스 번호를 통해 메세지 재조립
- 흐름 제어
종단간(end-to-end) 신뢰성있는 메세지 전달을 보장하는 기능
- 오류 제어
수신 과정에서 메세지가 오류 없이 전달 받았는지 확인하는 기능

**단위 - Segment(TCP), Datagram(UDP)**

**키워드**

> TCP, UDP

<aside>
  💡 <strong>TCP(연결 지향적 프로토콜) vs UDP(비연결 프로토콜)</strong> <br>
  - TCP는 데이터 전송을 위해 3-way handshaking 으로 연결하고 전송 완료시 4-way handshaking 으로 연결을 종료하는 방식의 프로토콜이지만 UDP 는 별도의 연결 없이 통신하는 프로토콜<br>
  - TCP 는 데이터를 순차적으로 전송하여 시퀀싱, 흐름제어, 오류제어, 재전송을 수행할 수 있지만 UDP 는 순서를 지정할 수 없으며 흐름제어 및 재전송을 수행할 수 없고 체크섬을 이용한 간단한 오류검사만 가능<br>
  - 속도적으로 UDP 는 수신기의 준비 상태를 확인하지 않으므로 TCP 보다 빠름<br>
  - TCP 는 HTTP, HTTPS, SMTP, FTP 등에 사용되며 UDP 는 화상회의, 스트리밍 등에 사용

</aside>

### [Layer 3] 네트워크 계층 (Network Layer)

네트워크에서 패킷의 소스-대상 또는 호스트-호스트 사이 논리적 통신을 담당하는 계층

**기능**

- 라우팅
라우터, 게이트웨이를 통해 패킷을 최종 목적지로 라우팅하기 위한 기능
- ARP
송신 과정에서 수신자의 MAC Address 를 알 수 없는 경우 수신자의 IP와 ARP Address 를 담은 패킷을 네트워크에 뿌리며 수신자의 MAC Address 를 담은 응답을 받는 기능
- 캡슐화
인터네트워크의 각 장치를 식별하기 위해 발신자와 수신자의 IP 를 네트워크 계층에 의해 헤더에 배치
- 분할
    
    큰 패킷을 보다 작은 패킷으로 분할하는 기능
    

**단위 - Packet**

**키워드**

> 라우터, IP
> 

### [Layer 2] 데이터 링크 계층 (Data Link Layer)

물리 계층으로 송수신 되는 데이터를 안전하게 전달되도록 처리하는 계층

**기능**

- 프레이밍
관리가능한 네트워크 계층에서 수신되는 비트 스트림이 프레임으로 해당 비트 스트림 분할은 데이터 링크 계층에서 수행
- 흐름제어
빠른 송신기로 인해 느린 수신기의 트래픽을 방지하기 여분의 비트를 버퍼링하여 흐름제어
- 오류 제어
프레임 끝부분에 트레일러를 추가하여 프레임의 복제 방지
- 엑세스 제어
두개 이상의 장치가 해당 링크에 연결된 경우 주어진 시간에 가능한 장치를 결정하는 기능

**단위 - Frame**

**키워드**

> 브릿지, 스위치
> 

### [Layer 1] 물리 계층 (Physical Layer)

OSI 의 가장 낮은 계층으로 다른 물리적 컴퓨터로 전기적 신호를 전송하는 계층
오직 0, 1의 데이터 전송만을 다루는 계층

**기능**

- 비트 표현
데이터 링크 계층의 비트 스트림을 0, 1 신호로 변경하는 기능
- 동기화
수신기와 송신기의 비트 수준의 동기화를 처리하는 기능

**단위 - Bit**

**키워드**

> 허브, 리피터
> 

## 질문 리스트

- OSI 모델과 7 layer 대해서 서술해주세요.
    
- 웹 브라우저는 Application Layer 에 속해있나요?
    
- TCP 와 UDP 의 차이를 서술해주세요.

- 네트워크 계층과 전송 계층의 차이를 서술해주세요.
    

## 참고 자료

[OSI 위키](http://wiki.hash.kr/index.php/OSI_7_%EA%B3%84%EC%B8%B5)

[OSI Layer](https://www.geeksforgeeks.org/layers-of-osi-model/)

[OSI Layer 기능](https://www.studytonight.com/computer-networks/osi-model-application-layer)

[브라우저 ≠ Application Layer](https://www.quora.com/What-do-you-mean-by-an-application-layer-in-networking)

[네트워크 계층 vs 전송 계층](https://the-brain-of-sic2.tistory.com/51)

[TCP vs UDP](https://www.lifesize.com/en/blog/tcp-vs-udp/)
