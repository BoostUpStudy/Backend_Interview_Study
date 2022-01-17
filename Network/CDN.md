## CDN(Content Delivery Network) 이란?

콘텐츠 전송 네트워크는 지리적으로 분산된 서버 집단으로 웹 콘텐츠 고속 전송을 위한 기술입니다. 일반적으로 오리진 서버와 각 지역에 PoP(Cache Server)로 구성하여 사용됩니다.

HTML, JS, CSS, Image, 동영상부터 웹에 필요한 콘텐츠들을 신속하게 전송하며 Netflix, Amazon, Youtube 과 같은 웹사이트들도 CDN 을 사용하고 있습니다. CDN 의 주요 목적은 웹 서버의 대역폭을 사용자에게 가장 가까운 서버로 분산하는 것을 목적으로 DDoS 공격을 완화가 가능합니다.

## 이점은?

CDN  을 구성한다면 성능, 가용성, 보안에 이점을 기대할 수 있습니다.

### 성능

CDN 서버는 자원을 캐싱합니다. 사용자가 웹 콘텐츠를 요청하는 경우 오리진 서버와 물리적으로 거리가 있을 수 있습니다. 하지만 CDN 을 활용한다면 물리적으로 거리가 있는 오리진 서버가 아닌 사용자 근처에 존재하는 CDN 서버에게 콘텐츠를 응답받을 수 있습니다.

**정적 콘텐츠**

일반적으로 CDN 서버에서 자원을 일정시간 동안 캐싱하여 사용자에게 제공합니다.

**동적 콘텐츠**

동적 콘텐츠는 스크립트로 인해 생성되는 자원으로 매번 다른 결과가 발생될 수 있습니다. 그렇기 때문에 캐싱이 제기능을 하기 힘듭니다.

하지만 최신 CDN 은 동적 콘텐츠를 보다 빠르게 전달하기 위해 짧은 캐싱 시간 혹은 오리진 서버와 데이터 압축 혹은 HTTP 2.0, WS 등의 방식으로 최적화를 시도할 수 있습니다.

### 가용성

MSA 의 핵심 개념으로 서버는 장애 혹은 과도한 트래픽이 발생해도 사용자에게 콘텐츠가 제공되어야 하는 개념입니다.

CDN 을 구성하지 않으면 전세계의 사용자들이 자원에 접속하기 위해 전부 오리진 서버로 요청이 도달하게 됩니다.

CDN 을 구성한다면 각 사용자들은 각 지역에 구성된 CDN 서버로 트래픽이 분산되며 해당 CDN 서버들 역시 이중화를 통해 가용성을 보장합니다.

### 보안

CDN 을 사용하면 DDoS 공격을 어느정도 보완할 수 있습니다.

- DDoS 공격?

    ```jsx
    DDOS 란?
    네트워크 계층, 어플리케이션 계층에 대한 사이버 공격입니다.
    - 네트워크 계층
    대역폭 얍축 공격
    서버가 제공할 수 없는 대량의 트랙픽을 발생시킴으로 서비스 중단을
    초래합니다. 예로는 "Reflection attack" 등이 
    존재합니다.
    세션 하이재킹
    공격자는 서버로 데이터 요청 패킷을 보내고 서버의 응답을 무시하여
    서버의 리소스를 낭비시킵니다. 예로는 "TCP SYN flood attack"
    등이 존재합니다.
    
    - 어플리케이션 계층
    간단하게 HTTP 요청을 많이 보내여 서버의 성능 저하를 유발합니다.
    "HTTP GET flood attack", "HTTP POST flood attack"
    등이 존재합니다.
    ```

    ```jsx
    Reflection attack?
    UDP 프로토콜 서비스를 제공하는 반사 서버를 구성하여 공격하는
    방식입니다.
    송신자의 IP 주소를 피해받는 서버의 IP 주소로 스푸핑하여 UDP 
    프로토콜을 구성한 반사 서버로 요청을 보냅니다. 해당 반사 서버
    들은 모두 피해자의 IP 주소로 응답을 전송합니다. 이런 행위를
    비 연결적 UDP 프로토콜로 빠르게 반복하여 서버의 장애를 
    발생시키는 공격방식입니다.
    ```

    ```jsx
    TCP SYN flooding attack?
    기본적으로 TCP 3 way handshake 를 이용하는 공격입니다.
    지속적으로 다른 IP 를 사용하여 연결의 시작인 SYN 을 보내며
    공격자는 서버의 SYN-ACK 를 받지 않거나 승인을 하지 않습니다.
    이 경우 서버는 클라이언트의 SYN-ACK 의 승인을 기다리는 상태인
    "half-open" 상태가 유지되며 서버의 연결 오버플로 테이블 초과시
    서비스의 장애가 발생합니다.
    ```


기본 CDN 역할로 어느정도 DDoS 공격은 완화됩니다.

예를 들어 CDN 구성으로 인해 전세계 사용자들은 지리적으로 근처에 존재하는 서버로 요청을 합니다. DDoS 공격으로 인한 트래픽 부하는 특정 지역에 국한될 것입니다. 하지만 DDoS 공격이 완전히 해결된 것은 아닙니다. DDoS 공격이 걸린 해당 지역은 서비스의 장애를 겪을 것 입니다. 또한 캐싱되지 않은 자원이나 캐시가 이루어지지 않는 동적 콘텐츠의 경우는 그대로 오리진 서버에 트래픽이 전달됩니다.

CDN 의 역할만으로 DDoS 공격에 완전히 대비되는 것은 아니므로 오늘날 CDN 제공 업체는 WAF(웹 어플리케이션 방화벽), DDoS 완화 서비스 등 클라우드 기반 보안 솔루션을 제공합니다.

## 참고자료

[CDN 이점](https://www.akamai.com/ko/our-thinking/cdn/what-is-a-cdn)

[DDoS, CDN](https://www.cdnetworks.com/ko/cloud-security-blog/employing-cdn-as-a-ddos-mitigation-can-be-useful/)

[Reflection attack](https://namu.wiki/w/%EB%B6%84%EC%82%B0%20%EB%B0%98%EC%82%AC%20%EC%84%9C%EB%B9%84%EC%8A%A4%20%EA%B1%B0%EB%B6%80%20%EA%B3%B5%EA%B2%A9?from=DRDos)

[SYN flood attack](https://www.imperva.com/learn/ddos/syn-flood/)

[CDN 캐싱](https://www.cloudflare.com/ko-kr/learning/cdn/caching-static-and-dynamic-content/)

[CDN Dynamic Content Optimization](https://gcorelabs.com/blog/how-to-speed-up-dynamic-content-delivery-using-cdn/)

[Cloud vs CDN](https://www.inap.com/blog/cdn-versus-cloud-computing-whats-difference-do-i-need-both/)