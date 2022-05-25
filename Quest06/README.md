# Quest 06. 인터넷의 이해

## Introduction
* 이번 퀘스트에서는 인터넷이 어떻게 동작하며, 서버와 클라이언트, 웹 브라우저 등의 역할은 무엇인지 알아보겠습니다.

## Topics
* 서버와 클라이언트, 그리고 웹 브라우저
* 인터넷을 구성하는 여러 가지 프로토콜
  * IP
  * TCP
  * HTTP
* DNS

## Resources
* [OSI 모형](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)
* [IP](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
  * [Online service Traceroute](http://ping.eu/traceroute/)
* [TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
  * [Wireshark](https://www.wireshark.org/download.html)
* [HTTP](https://ko.wikipedia.org/wiki/HTTP)
  * Chrome developer tool, Network tab
* [DNS](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)
  * [Web-based Dig](http://networking.ringofsaturn.com/Tools/dig.php)

## Checklist
* 인터넷은 어떻게 동작하나요? Internet Protocol Suite의 레이어 모델에 입각하여 설명해 보세요.
[How does the internet work - MDN](https://developer.mozilla.org/ko/docs/Learn/Common_questions/How_does_the_Internet_work)
```
- Local PC가 인터넷에 접근할 때 인터넷 영역에서의 수 많은 라우팅을 관리하는 Hob(Default Gateway)가 필요하며, 최종적으로 인터넷 사이트에 해당하는 라우터에 접근합니다.
- 통신하려는 목적지 IP주소는 특정 값으로 정해지지만, 인터넷의 경우엔 0.0.0.0/0으로 특정지어지지 않습니다.
- 라우팅 경로 정보가 정해져있는 정적 라우팅과는 달리, 동적 라우팅은 네트워크 상황에 따라 정보를 빠르게 확보할 수 있는 경로를 중심으로 패킷을 전송하는 라우팅입니다.
- 데이터 정보에 포함된 목적지 주소가 인터넷처럼 광범위하거나, 정적 라우팅을 통한 탐색이 불가능할 경우 동적 라우팅(보통 지역 통신사 등)을 통해 데이터 전달을 진행합니다.
```
  * 근거리에서 서로 떨어진 두 전자기기가 유선/무선으로 서로 통신하는 프로토콜은 어떻게 동작할까요?
  ```
  - 근거리에 놓여진 두 기기의 네트워크 대역은 보통 정적 라우팅을 통해 연결하며, 라우팅 테이블에 저장된 두 기기의 IP와 PORT 정보를 통해 데이터 전달이 이루어진다.
  - 와이파이를 통해 연결한다면 무선 공유기를 통한 라우팅을 진행할 것이고, 블루투스를 통해 연결한다면 BLE stack 프로토콜을 기반으로 통신을 진행할 것이다.
  ```
  * 근거리에 있는 여러 대의 전자기기가 서로 통신하는 프로토콜은 어떻게 동작할까요?
  ```
  - LAN(Local Area Network), 근거리 통신망을 이용하여 여러 대의 컴퓨터와 주변장치가 전용의 통신회선을 통하여 연결합니다.
  ```
  * 아주 멀리 떨어져 있는 두 전자기기가 유선/무선으로 서로 통신하는 프로토콜은 어떻게 동작할까요?
  ```
  - 사용하는 프로토콜은 두 기기간 거리보다는, 두 기기가 네트워크를 어떤 형태를 통해 연결하였으며 어떤 통신규약을 채용하고 있는지에 영향을 받습니다.
  - 보통 멀리 떨어져 있는 기기의 경우엔 근거리 대역의 네트워크가 없어 라우팅 테이블 작성이 어려우므로, 인터넷과 같이 Hob(지역 통신사)를 통한 데이터 전달이 이루어집니다.
  - WAN(Wide Area Network), 원거리 통신망을 이용하여 멀리 떨어진 다른 지역을 연결합니다.
  ```
  * 두 전자기기가 신뢰성을 가지고 통신할 수 있도록 하기 위한 프로토콜은 어떻게 동작할까요?
  ```
  - 웹과 사용자간의 대표적인 통신규약인 HTTP에 SSL인증을 적용한 HTTPS 프로토콜을 이용합니다.
  - HTTP 프로토콜을 통한 데이터 통신 과정에 SSL/TLS 암호화 방식(양방향 암호화)를 적용하여 상대적으로 안전한 데이터 전달이 가능하도록 한 방식입니다. 
  ```
  * HTTP는 어떻게 동작할까요?
  ```
  - HTTP는 하이퍼텍스트를 빠르게 교환하기 위한 프로토콜의 일종으로, 서버와 클라이언트 사이에서 어떻게 메시지를 교환할지를 정해 놓은 규칙입니다.
  - 요청(Request)과 응답(Response)로 구성되어 있으며, 일반적으로 80번 포트를 사용합니다.
  - 메시지 포맷은 평문(ASCII) 메시지로 이루어집니다.
  - 클라이언트는 서버로 요청 메시지를 전달하며 서버는 응답 메시지를 보냅니다.
  ```
  클라이언트 요청 예제
  ```
  GET /restapi/v1.0 HTTP/1.1
  Accept: application/json
  Authorization: Bearer UExBMDFUMDRQV1MwMnzpdvtYYNWMSJ7CL8h0zM6q6a9ntw
  ```
  서버 응답 예제
  ```
  HTTP/1.1 200 OK
  Date: Mon, 23 May 2005 22:38:34 GMT
  Content-Type: text/html; charset=UTF-8
  Content-Encoding: UTF-8
  Content-Length: 138
  Last-Modified: Wed, 08 Jan 2003 23:11:55 GMT
  Server: Apache/1.3.3.7 (Unix) (Red-Hat/Linux)
  ETag: "3f80f-1b6-3e1cb03b"
  Accept-Ranges: bytes
  Connection: close

  <html>
    <head>
      <title>An Example Page</title>
    </head>
    <body>
      Hello World, this is a very simple HTML document.
    </body>
  </html>
  ```
* 우리가 브라우저의 주소 창에 www.knowre.com 을 쳤을 때, 어떤 과정을 통해 서버의 IP 주소를 알게 될까요?
```
1. 주소 창에 www.knowre.com 입력
2. URL parsing
   - URL을 입력받은 브라우저는 URL의 구조를 해석합니다.
   - 어떤 프로토콜(https, http, ftp, sftp, pop3, IMAP, ,,,)인지?
   - 어떤 URL인지?
   - 어떤 포트인지?
      => 명시적으로 포트를 선언하지 않았다면 브라우저에서 기본 설정된 값을 이용해 요청합니다.
3. HSTS 목록 조회
   - HSTS(HTTP Strict Transport Security)는 HTTP를 허용하지 않고 HTTPS를 사용하는 연결만 허용하는 기능입니다.
   - 만약 HTTP로 요청이 왔다면 HTTP 응답 헤더에 "Strict Transport Security"라는 필드를 포함하여 응답하고, 이를 확인한 브라우저는 해당 서버에 요청할 때 HTTPS만을 통해 통신합니다.
   - 그리고 자신의 HSTS 캐시에 해당 URL을 저장하는데 이를 HSTS 목록이라고 부릅니다.
   - HSTS목록에 해당 URL이 존재한다면 명시적으로 HTTP를 통해 요청한다 해도 브라우저가 이를 HTTPS로 요청합니다.
4. domain에 해당하는 IP를 dns에서 검색
   - Domain Name(ex. www.knowre.com)으로는 컴퓨터끼리 통신할 수가 없기에 이를 인터넷 상에서 컴퓨터가 읽을 수 있는 IP주소로 변환해야 서로 통신이 가능합니다.
   - 브라우저는 (browser - OS - Router - ISP)순으로 확인합니다.

   0. 제일 먼저 브라우저의 DNS캐시가 존재하는지 확인
   1. 없다면 미리 설정 된 Local DNS에 해당 URL 주소의 IP 주소를 요청
   2. Local DNS에 해당 IP주소가 존재한다면 응답하고, 없다면 다른 DNS서버와 통신하는데 root DNS 서버에 해당 URL의 IP주소를 요청
   3. root DNS서버도 IP주소가 없다면 하위 DNS 서버에 요청하라고 응답합니다.
      이 응답을 받은 Local DNS는 .com 도메인을 관리하는 DNS 서버에 같은 내용을 요청합니다.
   4. .com DNS 서버에 해당 IP주소가 없다면 하위 DNS 서버에 요청하라고 응답합니다.
      이 응답을 받은 Local DNS는 www.knowre.com 도메인을 관리하는 DNS 서버에 같은 내용을 요청합니다.
   5. knowre.com DNS 서버에서 IP주소를 응답받은 Local DNS는 해당 IP주소를 캐싱하고 응답합니다.
5. 라우터를 통해 해당 서버의 게이트웨이까지 이동
   - IP 주소를 할당 받은 후, 해당 서버로 요청을 보냅니다. 이 요청이 네트워크를 어떻게 이동할지는 네트워크 라우터의 라우팅이 경로를 설정합니다.
   - 라우터에서는 라우팅 테이블을 통해 해당 요청이 어떤 경로를 통해 가야할지 경로를 지정해줍니다.
6. ARP를 통해 IP주소를 MAC 주소로 변환
   - 실질적 통신을 위해 논리 주소인 IP를 물리 주소인 MAC 주소로 변환합니다.
   - 이를 위해 네트워크 내에서 ARP를 브로드캐스팅 합니다.
   - 해당 IP주소를 가지고 있는 노드는 자신의 MAC 주소를 응답합니다.
7. IP를 통해 서버와 TCP 연결
   - 대상 서버와 통신하기 위해 TCP 소켓 연결을 진행합니다.
   - 소켓 연결은 3-way-handshaking을 통해 이루어집니다.
   - 서버에게 접속 요청을 보내면, 서버는 해당 요청을 확인하고 수락하는 메시지를 보냅니다.
   - 클라이언트는 서버의 요청 수락 메시지를 받고 알겠다는 응답 메시지를 보내줍니다.
   +) HTTPS 요청의 경우에는 암호화 통신을 위한 TLS 핸드쉐이킹이 추가됩니다. (HTTP + TLS = HTTPS)
   +) 이를 통해 서버와 클라이언트는 암호화 통신을 진행할 수 있습니다.
8. GET /index.html
   연결이 확정된 후, 해당 페이지를 서버에게 요청하게 됩니다. 서버에서 요청을 받고 이 요청을 수락할 수 있는지 검사 후, 요청에 대한 응답을 생성하여 브라우저에게 전달합니다.
9. HTML parse
   서버의 응답(HTML, CSS, JS ..)을 브라우저에서 해석하여 화면을 출력합니다.
```

## Quest
* tracert(Windows가 아닌 경우 traceroute) 명령을 통해 www.google.com 까지 가는 경로를 찾아 보세요.
  * 어떤 IP주소들이 있나요?
  * 그 IP주소들은 어디에 위치해 있나요?
* Wireshark를 통해 www.google.com 으로 요청을 날렸을 떄 어떤 TCP 패킷이 오가는지 확인해 보세요
  * TCP 패킷을 주고받는 과정은 어떻게 되나요?
  * 각각의 패킷에 어떤 정보들이 담겨 있나요?
* telnet 명령을 통해 http://www.google.com/ URL에 HTTP 요청을 날려 보세요.
  * 어떤 헤더들이 있나요?
  * 그 헤더들은 어떤 역할을 하나요?

## Advanced
* HTTP의 최신 버전인 HTTP/3는 어떤 식으로 구성되어 있을까요?
* TCP/IP 외에 전세계적인 네트워크를 구성하기 위한 다른 방식도 제안된 바 있을까요?
