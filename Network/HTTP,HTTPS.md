# HTTP, HTTPS

![출처 : [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)](https://mdn.mozillademos.org/files/13677/Fetching_a_page.png)

출처 : [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)

## HTTP(HyperTextTransferProtocol)

HTML과 같은 하이퍼미디어 문서를 전송하기 위한 어플리케이션 레이어 프로토콜입니다. 

HTTP는 비연결성의 무상태 프로토콜이며 서버/클라이언트 모델을 따라 데이터를 주고 받고, 기본 포트로 80번 포트를 사용합니다.

### HTTP 버전별 기능

- HTTP/0.9
    - HTTP의 가장 초기 버전으로 원래는 버전 번호가 없는데 구분을 위해 향후 붙였다고 합니다
    - 헤더 없이 단순히 HTML 파일만 전송하며, GET 메소드만 사용 가능
- HTTP/1.0 – 확장성 만들기
    - 헤더를 통해 HTTP 버전 코드를 송신하고, 상태 코드를 회신 받을 수 있게 되었습니다.
    - 헤더의 Content-Type을 통해 HTML이 아닌 형태도 전송 가능해졌습니다. (문자열 전송)
    - 사용가능한 메서드: GET, POST, PUT
- HTTP/1.1 (표준 프로토콜)
    - Keep Alive로 커넥션이 재사용 될 수 있도록 개선되었습니다.
    - Host 헤더가 추가되어 동일 IP 주소에 다른 도메인을 호스트하는 기능이 서버 코로케이션을 가능하게 했습니다.
    - 사용가능한 메서드: OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE
- HTTP/2 – 더 나은 성능을 위한 프로토콜
    - 2015년에 발표됨, 구글의 SPDY를 기반으로 표준화 되었습니다.
    - 문자열 전송 기반이 아닌 이진 데이터 전송 기반으로, 스트림, 메시지 및 프레임으로 데이터 교환 방식이 변경됨
        - 스트림:  구성된 연결 내에서 전달되는 바이트의 양방향 흐름이며, 하나 이상의 메세지가 전달 가능함(request or response는 하나의 메시지)
        - 메시지: 논리적 요청 또는 응답 메시지에 매핑되는 프레임의 전체 시퀀스
        - 프레임: http/2.0에서 통신의 최소 단위, 각 최소 단위에는 하나의 프라임 헤더가 포함된다. 이 프라임 헤더는 최소한으로 프레임이 속하는 스트림을 식별한다. Headers Type Frame, Data Type Frame이 존재한다.
    - 주요 스팩
        - HTTP Header Data Compression (HTTP 헤더 데이터 압축)
            
            이전 Header의 중복되는 필드를 재전송하지 않아서 데이터를 절약하고, HPACK이라는 Header 압축방식을 이용하여 데이터 전송 효율을 높였다.
            
        - Server Push
            
            클라이언트가 요청 하지 않은 JavaScript, CSS, Font, 이미지 파일 등과 같이 필요하게 될 특정 파일들을 서버에서 단일 HTTP 요청 응답으로 전송 가능하게 한다.
            
        - HOL(Head-of-Line) 문제 해결
            
            HTTP/1.1 까지는 한번에 하나의 파일만 전송이 가능했었지만, 여러 파일을 한번에 병렬 전송할 수 있께 개선되었다.
            
        - Stream 우선순위
            
            HTTP 메시지가 많은 개별 프레임으로 분할될 수 있고 여러 스트림의 프레임을 다중화(Multiplexing)할 수 있게 되면서, 스트림들의 우선순위를 지정할 필요가 생겼다. 클라이언트는 우선순위 지정을 위해 ‘우선순위 지정 트리'를 사용하여 서버의 스트림처리 우선순위를 지정할 수 있다. 서버는 우선순위가 높은 응답이 클라이언트에 우선적으로 전달될 수 있도록 대역폭을 설정한다.
            
        
- HTTP/3
    - QUIC(Quick UDP Internet Connections) 프로토콜 사용, UDP를 사용한다.
    - 클라이언트의 IP가 바뀌어도 연결이 유지됨, (ex)와이파이에서 LTE로 전환할때)

### HTTP 구성요소

- HTTP는 요청(Request)와 응답(Response)로 구성되어 있다.
- 시작줄, 헤더, 바디로 이루어져있다.
- **요청**
    
    ![출처: [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)
    출처: [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
    
    시작줄에 수행하고자 하는 메서드, HTTP 버전과 같은 프로토콜이 표시된다. 
    
    헤더에는 가져오려는 리소스의 경로; 예를 들면 [프로토콜](https://developer.mozilla.org/ko/docs/Glossary/Protocol) (`http://`), [도메인 (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/Domain) (여기서는 `developer.mozilla.org`), 또는 TCP [포트 (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/Port) (여기서는 `80`)인 요소들을 제거한 리소스의 URL입니다.
    
    > 그 이외에 추가하고자 하는 헤더, POST의 경우 body가 들어감
    > 
- **응답**
    ![출처: [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)
    출처: [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
    - 시작줄에  HTTP 프로토콜 버전, 상태코드와 메시지가 표시된다.
    - 그 이외에 각종 헤더들이 들어가고, 요청에 맞는 리소스가 body에 포함되기도 한다.

## HTTPS (Hyper Text Transfer Protocol Secure)

말 그대로 HTTP에 Secure, 보안이 추가된 프로토콜이며 443번을 기본 포트로 사용한다. 클라이언트와 서버간의 모든 커뮤니케이션을 암호화 하기 위해 SSL / TLS 를 사용한다.

### 대칭키와 비대칭키(공개키)

**대칭키**의 경우에는 암호화, 복호화에 사용하는 키가 동일하고 속도가 빠른 대신 키를 교환 해야 하기 때문에 탈취 관리를 해야하고, 기밀성을 제공하지만 무결성/인증을 보장하지 않는다. 

**비대칭키(공개키)**는 암복호화에 사용하는 키가 서로 다르며 속도가 느린 대신 , 기밀성, 무결성,인증 기능이 모두 제공된다. 대표적으로 RSA가 있다.

### 공개키와 비밀키 (Public Key Private Key )

비대칭키로 공개키와 비밀키를 사용하는데 다음과 같다.

1) 공개키로 암호화 하면 개인키로만 복호화 가능하다

2) 개인키로 암호화 하면 공개키로만 복호화가 가능하다.

따라서 1)의 경우 개인키를 가지고 있어야만 볼 수 있고, 2)의 경우 공개키로 복호화가 된다면 해당 정보에 대한 신뢰성이 보장된다.

### TSL / SSL

암호화를 담당하는 프로토콜, HTTPS에서 사용됨

**SSL (Secure Scoket Layer)**

- HTTP와 독립된 프로토콜로 HTTP 외에도 다방면으로 사용되고 있습니다.
- 두 통신 사이에 핸드셰이크를 통해 인증 프로세스가 진행됨

**TLS (Transport Layer Security)**

- TLS는 SSL 3.0을 기초로 해서 IETF가 만든 프로토콜이다. (TLS 1.0 == SSL3.1)
- SSL과 거의 동일하다고 생각하면 됨

### HTTPS 동작과정(SSL)

서버는 클라이언트가 요청을 보낼 때 암호화를 하기 위한 공개키를 생성해야 하는데, 일반적으로는 인증된 기관(Certificate Authority) 에 공개키를 전송하여 인증서를 발급받고 있다. 자세한 과정은 다음과 같다.

- 공개키 암호화 방식과 대칭키 암호화 방식의 장점을 활용해 하이브리드 사용
    - 데이터를 대칭키 방식으로 암복호화하고, 공개키 방식으로 대칭키 전달
1. **클라이언트가 서버 접속하여 Handshaking 과정에서 서로 탐색**
    
    1.1. **Client Hello**
    
    - 클라이언트가 서버에게 전송할 데이터
        - 클라이언트 측에서 생성한 **랜덤 데이터**
        - 클-서 암호화 방식 통일을 위해 **클라이언트가 사용할 수 있는 암호화 방식**
        - 이전에 이미 Handshaking 기록이 있다면 자원 절약을 위해 기존 세션을 재활용하기 위한 **세션 아이디**
    
    1.2. **Server Hello**
    
    - Client Hello에 대한 응답으로 전송할 데이터
        - 서버 측에서 생성한 **랜덤 데이터**
        - **서버가 선택한 클라이언트의 암호화 방식**
        - **SSL 인증서**
    
    1.3. **Client 인증 확인**
    
    - 서버로부터 받은 인증서가 CA에 의해 발급되었는지 본인이 가지고 있는 목록에서 확인하고, 목록에 있다면 CA 공개키로 인증서 복호화
    - 클-서 각각의 랜덤 데이터를 조합하여 pre master secret 값 생성(데이터 송수신 시 대칭키 암호화에 사용할 키)
    - pre master secret 값을 공개키 방식으로 서버 전달(공개키는 서버로부터 받은 인증서에 포함)
    - 일련의 과정을 거쳐 session key 생성
    
    1.4. **Server 인증 확인**
    
    - 서버는 비공개키로 복호화하여 pre master secret 값 취득(대칭키 공유 완료)
    - 일련의 과정을 거쳐 session key 생성
    
    1.5. **Handshaking 종료**
    
2. **데이터 전송**
    - 서버와 클라이언트는 session key를 활용해 데이터를 암복호화하여 데이터 송수신
3. **연결 종료 및 session key 폐기**

    

## 참고자료

- HTTP 버전

  [HTTP의 진화 - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)

  [HTTP](https://itwiki.kr/w/HTTP)

  [HTTP/1.1, /2, /3 의 차이점](https://velog.io/@zzzz465/HTTP1.1-2-3-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

  [[CS/Network] HTTP 버전 별 특징](https://koonii.tistory.com/m/21)

- HTTP 구성요소
    
    [HTTP 개요 - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
    
- HTTPS와 TSL/SSL
    
    [](https://velog.io/@moonyoung/HTTPS%EC%9D%98-%EC%9B%90%EB%A6%AC)
    
    [HTTPS 와 SSL(TLS)](https://futurecreator.github.io/2018/07/12/https-and-ssl-tls/)
    
    [✔ SSL/TLS 보안](https://velog.io/@saseungmin/SSLTLS-%EB%B3%B4%EC%95%88)
    
    [대칭키 vs 공개키(비대칭키)](https://velog.io/@gs0351/%EB%8C%80%EC%B9%AD%ED%82%A4-vs-%EA%B3%B5%EA%B0%9C%ED%82%A4%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4)
    
    [✔ SSL/TLS 보안](https://velog.io/@saseungmin/SSLTLS-%EB%B3%B4%EC%95%88)
    
    [tech-interview/network.md at master · WeareSoft/tech-interview](https://github.com/WeareSoft/tech-interview/blob/master/contents/network.md)
    
- HTTP 2.0
    
    [HTTP/2(HTTP 2.0) 정리](https://velog.io/@taesunny/HTTP2HTTP-2.0-%EC%A0%95%EB%A6%AC)
    
    [HTTP/2 소개 | Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/performance/http2?hl=ko)