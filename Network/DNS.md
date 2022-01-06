## DNS(Domain Name System)

호스트의 도메인 이름과 호스트의 네트워크 주소(ip address) 변경해주는 System 입니다.

해당 DNS 기능이 없다면 [naver.com](http://naver.com) 과 같은 도메인 이름으로 웹 사이트에 접근할 수 없으며 해당 호스트의 네트워크 주소를 통해서만 접근이 가능합니다.

> 응용계층에서 http 프로토콜과 병렬로 이루어지는 작업입니다.
>

### Domain

IP 를 사용하는 서버의 주소를 사용자가 기억하기 쉽게 만들어진 주소로 `.` 으로 구분됩니다.

> 💡 URL 이 도메인?  
URL Web Site 자원의 주소입니다.  
도메인을 포함하여 프로토콜, 자원의 경로, 자원의 Parameter, Fragment 까지 구성된 주소로 도메인의 상위 개념입니다.


**루트 도메인 체계**

![domain](https://user-images.githubusercontent.com/74395748/148407029-8127c5eb-00f8-42eb-b438-66d9683fc659.png)


- **Root Domain**

  인터넷 체계에서와 웹사이트 수준에서 다른 의미를 가집니다.

  인터넷 체계 수준에서는 TLD 보다 높은 인터넷 계층 수준입니다. TLD 뒤 이름없는 `.` 만으로 구분되지만 묵시적으로 사용됩니다.

  웹 사이트 수준에서는 TLD 부터 도메인 이름까지를 루트 도메인으로 부릅니다.

  > ex. dongmin.dev
>
- **TLD(Top Level Domain)**

  인터넷 DNS 시스템에서 루트 도메인 이후에 명시되는 것을 TLD 라고 부릅니다.  ccTLD, gTLD, New gTLD 가 존재합니다.

    - ccTLD

      국가 코드 최상위 도메인으로 국가, 종속 지역을 나타내는 도메인 이름입니다.

      특정 국가를 타겟팅하는 웹사이트의 경우 Google SEO 에 보다 효과적입니다.

      > ex. kr, jp ...
    >
    - gTLD

      일반 최상위 도메인으로 국가 코드 최상위 도메인을 제외한 일반적으로 사용되는 최상위 도메인입니다.

      > ex. com, net
    >
    - New gTLD

      특정 기업이나 기관의 신청으로 기존의 gTLD 이외의 생성되는 도메인입니다.

- **SLD(Second Level Domain)**

  최상위 도메인 바로 아래 영역에 존재하는 도메인입니다.

    - ccSLD

      최상위 도메인이 국가 코드 도메인인 경우 도메인 등록 조직을 나타냅니다.

      > ex. co.kr, [ac.kr](http://ac.kr) ...
    >
    - SLD

      최상위 도메인이 일반 최상위 도메인인 경우 일반적으로 등록 조직이 지정한 도메인 이름이 됩니다.

      > ex. [naver.com](http://naver.com), dongmin.dev
>
- **3LD(Third Level Domain)**

  국가 코드 도메인을 사용하는 경우 등록 조직이 지정한 도메인 이름입니다.

  > ex. konkuk.ac.kr
>


### DNS Server 종류

> 💡 DNS Server ?   
관리하는 도메인 이름과 ip 주소를 매핑하여 관리하며 클라이언트의 요청이 들어오면 ip 주소나 도메인 이름을 반환해주는 Server 입니다.


- **Recursive Name Server**

  Local DNS Server, 기지국 DNS Server 라고도 불립니다. 말그대로 재귀적으로 Domain 에 대해서 IP 작업을 찾습니다.

  우선 DNS 쿼리를 받으면 캐시 목록을 통해 결과를 찾습니다. 결과값이 없다면 Root Name Server, TLD Name Server, Authoritative Name Server 순으로 요청과 응답을 하며 결과값을 Client 로 전달합니다.

- **Root Name Server**

  전역적인 최상위 도메인 TLD 목록 정보가 구성되어 있습니다. 12 개의 조직에서 구성되어 운영됩니다.

  Recursive Name Server 의 DNS 쿼리에 대해서 TLD Name Server 주소를 반환하는 역을 맡습니다.

- **TLD Name Server**

  Top Level Domain 을 관리하는 Name Server 입니다.

  com 과 같은 특정 TLD 에 대한 웹사이트 정보들로 구성되어 있어 요청받은 도메인의 Authoritative Name Server 의 주소를 반환합니다.

- **Authoritative Name Server**

  IP 주소를 얻는 마지막 단계입니다. 도메인 이름에 대한 고유 정보와 각 레코드 정보들이 존재합니다. 일반적으로 도메인/호스팅 업체들의 DNS 서버이며 개인 DNS 서버 역시 Authoritative Name Server 로 분류됩니다.

  A 레코드에서 도메인을 찾았다면 해당 IP 를 반환하며 CNAME 레코드에서 도메인을 찾은경우 해당 도메인을 Recursive Name Server 로 반환하여 Recursive Name Server 는 처음부터 IP 를 찾아가는 과정을 수행합니다.


### Process

<img width="998" alt="dns" src="https://user-images.githubusercontent.com/74395748/148407058-99851725-e37e-4027-9591-5af4d5375cf6.png">


1. 사용자가 브라우저를 통해 [www.dongmin.dev](http://www.dongmin.dev) 에 접근합니다.
2. Recursive DNS Server 로 [www.dongmin.dev](http://www.dongmin.dev) 의 IP 주소를 요청합니다.
3. Recursive DNS Server 레코드에 정보가 없는 경우 Root DNS Server 로 [www.dongmin.dev](http://www.dongmin.dev) IP 주소를 요청합니다.
4. Root DNS Server 는 요청 받은 도메인의 Top Level Domain(.dev) Name Server 의 IP 주소를 반환합니다.
5. Recursive DNS Server 는 응답받은 TLD Name Server IP 로 [www.dongmin.dev](http://www.dongmin.dev) IP 주소를 요청합니다.
6. TLD Name Server 는 [www.dongmin.dev](http://www.dongmin.dev) 에서 dongmin.dev 를 관리하는 Authoritative Name Server 주소를 반환합니다.
7. 마지막으로 Recursive DNS Server 는 Authoritative Name Server 로 [www.dongmin.dev](http://www.dongmin.dev) IP 주소를 요청합니다.
8. Authoritative Name Server 는 명시된 레코드에서 도메인을 찾으며 A 레코드에서 찾았다면 해당 IP 주소를 Recursive DNS Server 로 반환합니다.
9. Authoritative Name Server 로 부터 받은 IP 주소를 Recursive DNS Server 는 TTL 만큼 캐싱하며 브라우저에게 IP 주소를 응답합니다.
10. 브라우저는 응답받은 IP 주소를 통해 Web Server 에 접근합니다.

> 💡 DNS 에서 사용하는 전송 프로토콜은 뭘까?    
기본적으로 DNS message 가 512 byte 이하일 경우 UDP 프로토콜을 사용하여 통신하며 zone-transfer, 512 byte 초과시 TCP 프로토콜을 사용하여 통신합니다.


> 💡 zone-transfer ?    
Master DNS 와 Slave DNS 서버로 이중화가 구성된 경우 발생하는 작업입니다.   
한마디로 Master 서버의 Zone(도메인과 IP 매핑 정보) 파일을  Slave 서버로 최신화하는 작업입니다.


## 참고자료

[DNS Process](https://www.cloudflare.com/ko-kr/learning/dns/dns-server-types/)

[Root Domain](https://raventools.com/marketing-glossary/root-domain/)

[Name Server 종류](https://www.dynu.com/en-US/Blog/Article?Article=DNS-Servers-Authoritative-Recursive-Root-TLD)

[Domain 체계](https://better-together.tistory.com/128)

[Second-level domain](https://en.wikipedia.org/wiki/Second-level_domain)

[ccTLD](https://www.affde.com/ko/what-is-a-cctld.html)

[DNS 512 byte UDP](https://serverfault.com/questions/587625/why-dns-through-udp-has-a-512-bytes-limit)