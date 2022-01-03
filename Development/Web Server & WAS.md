## Web Server
주로 웹 브라우저에서 HTTP 요청에 응답하여 정적인 컨텐츠를 제공합니다.
web server 는 하드웨어, 소프트웨어 또는 둘다 같이 동작합니다.

<img width="400" src="https://user-images.githubusercontent.com/74395748/147853834-dd096bbc-b45f-449e-8402-1fd931d71f19.png">

**하드웨어**

Web Server 소프트웨어와 Website 의 컴포넌트 파일을 저장하는 컴퓨터입니다.

```jsx
여기서 컴포넌트 파일은 HTML 문서, images, CSS file, js file 등 정적 파일입니다.
```

**소프트웨어**

클라이언트(웹 브라우저)로부터 HTTP 요청을 받아 정적인 컨텐츠를 제공하는 컴퓨터 프로그램입니다.

**흐름**

브라우저에서 웹 서버의 자원이 필요한 경우 HTTP 를 요청합니다. 해당 요청은 웹 서버 하드웨어에 올바르게 도달한 경우 HTTP 요청에 상응하는 자원을 HTTP 를 사용하여 응답합니다.

기능

- 정적 컨텐츠 제공

  별도의 소프트웨어의 영향없이  웹 서버 소프트웨어를 통해 컨텐츠가 제공하는 경우입니다.

  즉, 컨텐츠에 대해서 추가적인 가공없이 HTTP 서버가있는 하드웨어로 구성됩니다.

- 동적 컨텐츠 전달

  정적 웹 서버에서 추가적인 소프트웨어(일반적으로 WAS, Database)가 구성된 경우입니다.

  HTTP 서버를 통해 전송되기 전 WAS 에게 전달하여 컨텐츠 가공이 이루어집니다.


**Example**
Apache Web Server, Nginx Web Server, IIS Web Server 등이 존재합니다.

> [각 Web server 의 간단한 장단점](https://server-talk.tistory.com/296)

## WAS(Web Application Server)

Database 조회나 다양한 로직을 처리하며 동적인 컨텐츠를 제공하기 위한 Application Server 입니다.
즉 웹 서버와 DBMS 사이 미들웨어(비지니스 로직) 역할입니다.

<img width="400" src="https://user-images.githubusercontent.com/74395748/147853856-49fdb485-4e5b-4102-b527-79f0ce604733.png">


**Example**

Java/JSP, .Net(aspx), PHP, Ruby(on Rails), Python, Nodejs(Express) 등이 존재합니다.

**작동 프로세스(Tomcat)**

1. 클라이언트가 브라우저를 통해 웹 사이트에 접근합니다.
2. Web Server 를 통해 HTTP 를 수신하고 동적 페이지가 필요한 경우 WAS 로 전달합니다.
3. Web Container 는 web.xml(배포 서술자, 비슷한 개념으로 node 의 package.json) 를 바탕으로 Thread 를 생성하고 서블릿 요청, 응답 객체(HTTPServletRequest, HTTPServletResponse) 를 생성하여 Thread 에 전달합니다.
4. 컨테이너는 사용자의 요청에 관한 Servlet 을 호출합니다.
5. 해당 Servlet 을 담당하는 Thread 가 요청에 따라 doGet, doPost 를 호출하여 동적 페이지를 생성합니다.
6. 생성된 동적 페이지는 HTTPServletResponse 객체에 실어 컨테이너에 전달합니다.
7. 컨테이너는 응답 객체를 HTTPResponse 형태로 변경하여 Web Server 에 전달하고 생성된 Thread 를 종료 및 서블릿 요청, 응답 객체를 소멸시킵니다.

## Web Server vs WAS

Web Server 는 주로 HTTP(S) 프로토콜의 요청 및 응답으로 HTML 페이지, CSS, Image 등 정적 파일을 클라이언트에 전달합니다.

WAS(Application Server) 는 다양한 프로토콜을 지원하여 비지니스 로직을 통해 동적 페이지를 생성하여 전달합니다.

하지만 오늘날 Web Server, WAS 들은 기술 결합으로 인하여 하이브리드를 제공하기 때문에 경계가 모호하다고 생각합니다. 실제로 Web Server 는 동적 페이지를 생성하기 위해 스크립트 언어용 플러그인을 제공하며 WAS 역시 정적 페이지를 전달할 수 있습니다. 즉, HTTP 프로토콜을 기본으로 제공하지만 다른 프로토콜을 제공하면서 Reverse Proxy, 클러스터링, 로드 밸런싱 등의 기능 역시 사용할 수 있도록 통합이 되고 있습니다.

그럼에도 둘을 나눠서 관리하는 이유는 데이터 처리 방식, 보안이 있습니다.

- 데이터 처리 방식
  정적인 콘텐츠를 Web Server 를 통해서 처리하면 WAS 에게 전달하지 않고 Web Server 에서 바로 응답을 처리할 수 있습니다. 이경우 Web Server 는 WAS 의 부하를 덜어줍니다. + 캐시
- 보안
  WAS 의 정보(Ex. Port) 가 외부에 공개되지 않습니다.
  WAS 의 정보가 탈취되는 경우 Database 서버의 접속 정보, Session 등 보안상 문제가 발생할 수 있는 정보들이 노출될 수 있습니다.