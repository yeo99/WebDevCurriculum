# Quest 08. 웹 API의 기초

## Introduction
* 이번 퀘스트에서는 웹 API 서버의 기초를 알아보겠습니다.

## Topics
* HTTP Method
* node.js `http` module
  * `req`와 `res` 객체

## Resources
* [MDN - Content-Type Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type)
* [MDN - HTTP Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
* [MDN - MIME Type](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type)
* [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
* [HTTP Node.js Manual & Documentation](https://nodejs.org/api/http.html)

## Checklist
* HTTP의 GET과 POST 메소드는 어떻게 다른가요?
```
- HTTP는 요청 메서드를 정의하여, 주어진 리소스에 수행하길 원하는 행동을 나타냅니다. 각각의 메서드는 서로 다른 의미를 구현하지만, 일부 기능은 메서드 집합간에 서로 공유하기도 합니다.
이를테면 응답 메서드는 안전하거나, 캐시 가능(cacheable)하거나, 멱등성을 가질 수 있습니다.

- HTTP GET 메서드는 특정한 리소스를 가져오도록 요청합니다. GET요청은 데이터를 가져올 때만 사용해야 합니다.
  ex) GET /index.html

- HTTP POST 메서드는 서버로 데이터를 전송합니다. 요청 본문의 유형은 Content-Type 헤더로 나타냅니다.
  PUT과 POST의 차이는 멱등성으로, PUT은 멱등성을 가집니다. PUT은 한 번을 보내도, 여러 번을 보내도 같은 효과를 보입니다. 즉 부수 효과(side effect)가 없습니다.

- POST요청은 보통 HTML 양식을 통해 서버에 전송하며, 서버에 변경사항을 만듭니다.
  이 경우의 콘텐츠 유형(Content-Type)은 form요소의 enctype 특성이나 input, button 요소의 formenctype 특성 안에 적당한 문자열을 넣어 결정합니다.

+) 멱등성?
- 동일한 요청을 한 번 보내는 것과 여러 번 연속으로 보내는 것이 같은 효과를 지니고, 서버의 상태도 동일하게 남을 때, 해당 HTTP 메서드가 멱등성을 가졌다고 말합니다.
- 다른 말로는, 멱등성 메서드에는 통계 기록 등을 제외하면 어떠한 부수 효과(side effect)도 존재해서는 안됩니다.
- 올바르게 구현한 경우 GET, HEAD, PUT, DELETE 메서드는 멱등성을 가지며, POST메서드는 그렇지 않습니다.
- 모든 안전한 메서드는 멱등성을 가집니다.
```
  * 다른 HTTP 메소드에는 무엇이 있나요?
  ```
  - HEAD: HTTP HEAD 메서드는 특정 리소스를 GET 메서드로 요청했을 때 돌아올 헤더를 요청합니다.
    HEAD 메서드에 대한 응답은 본문을 가져선 안되며, 본문이 존재하더라도 무시해야 합니다.
    HEAD 요청의 응답이 캐시했던 이전 GET 메서드의 응답을 유효하지 않다고 표시할 경우, 새로운 GET 요청을 생성하지 않더라도 캐시를 무효화합니다.

  - PUT: HTTP PUT 메서드는 요청 페이로드를 사용해 새로운 리소스를 생성하거나, 대상 리소스를 나타내는    데이터를 대처합니다. PUT과 POST의 차이는 멱등성으로, PUT은 멱등성을 가집니다.

  - DELETE: HTTP DELETE 메서드는 지정한 리소스를 삭제합니다.
    DELETE메서드를 성공적으로 적용한 후에 사용할 수 있는 응답 상태 코드는 다음과 같이 몇 가지가 있습니다.
    - 아마도 명령을 성공적으로 수행할 것 같으나 아직은 실행하지 않은 경우 202(Accepted) 상태 코드
    - 명령을 수행했고 더 이상 제공할 정보가 없는 경우 204(No Content) 상태 코드
    - 명령을 수행했고 응답 메시지가 이후의 상태를 설명하는 경우 200(OK) 상태 코드

  - CONNECT: HTTP CONNECT 메서드는 요청한 리소스에 대해 양방향 연결을 시작하는 메소드입니다.
    이는 터널을 열기 위해서 사용될 수 있습니다.
    예를 들어, CONNECT 메소드는 SSL(HTTPS)를 사용하는 웹 사이트에 접속하는데 사용될 수 있습니다.
    - 클라이언트는 원하는 목적이와의 TCP연결을 HTTP 프록시 서버에 요청합니다.
    - 그러면 서버는 클라이언트를 대신하여 연결의 생성을 진행합니다.
    - 한번 서버에 의해 연결이 수립되면, 프록시 서버는 클라이언트에 오고가는 TCP 스트림을 계속해서 프록시합니다.

  - OPTIONS: HTTP OPTIONS 메서드는 목표 리소스와의 통신 옵션을 설명하기 위해 사용됩니다.
    클라이언트는 OPTIONS 메소드의 URL을 특정지을 수 있으며, aterisk(*)를 통해 서버 전체를 선택할 수 있습니다.

  - TRACE: HTTP TRACE 메서드는 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행하여 유용한 디버깅 메커니즘을 제공합니다.

  - PATCH: HTTP PATCH 메서드는 리소스의 부분적인 수정을 할 때에 사용합니다.
    HTTP PUT 메서드는 문서 전체의 완전한 교체만을 허용합니다. 반면 PATCH 메소드는 PUT 메소드와 달리 멱등성을 가지지 않는데, 이는 동일한 PATCH 요청이 다른 결과를 야기할 수도 있음을 뜻합니다.
    하지만 PATCH를 PUT과 같은 방식으로 사용함으로써 멱등성을 가지게 할 수도 있습니다.
    PATCH(혹은 PUT)은 다른 리소스에 부수효과를(side-effects)를 일으킬 가능성이 있습니다.
    PATCH가 허용되는지 확인할 수 있는 또 다른(암묵적인)지표로 Accept-Patch의 존재 유무를 들 수 있는데, 이를 통해 patch 문서 양식이 서버에 받아 들여졌음을 알 수 있습니다.
  ```
* HTTP 서버에 GET과 POST를 통해 데이터를 보내려면 어떻게 해야 하나요?
```
  - 1. form 태그에 method속성을 명시하여 전송
  - 2. POSTMAN을 이용하여 전송
```
  * HTTP 요청의 `Content-Type` 헤더는 무엇인가요?
  ```
  - Content-Type 개체 헤더는 리소스의 media type(MIME type, content type)을 나타내기 위해 사용됩니다.
    ex) 오디오 파일은 audio/ogg로, 그림 파일은 image/png 등으로 분류
  - 응답 내에 있는 Content-Type 헤더는 클라이언트에게 반환된 컨텐츠의 유형이 실제로 무엇인지를 알려줍니다.
  - 브라우저들은 어떤 경우에는 MIME 스니핑을 해서 이 헤더의 값을 꼭 다르지는 않을겁니다.
    => 이를 막기 위해 X-Content-Type-Options헤더를 nosniff로 설정할 수 있습니다.
  - 요청 내에서, 클라이언트는 서버에게 어떤 유형의 데이터가 실제로 전송됐는지를 알려줍니다.
  ```
  * Postman에서 POST 요청을 보내는 여러 가지 방법(`form-data`, `x-www-form-urlencoded`, `raw`, `binary`) 각각은 어떤 용도를 가지고 있나요?
  ```
  - x-www-form-urlencoded: Default content-type, url의 분리가 &로 분리되며 =기호를 통해 key/value를 연결, 인코딩한다.
  - form-data: form-urlencoded와 같이 text/plain을 기본값으로 하며, 문자열이 인코딩되지 않는다.
  - raw: 문자열 자체를 전송할때 사용하며, JSON, text, xml 등의 형태를 전송한다.
  - binary: img/audio와 같이 사람이 수동으로 입력할 수 없을때 사용하는 옵션이다.
  ```
  - 
* node.js의 `http` 모듈을 통해 HTTP 요청을 처리할 때,
  * `req`와 `res` 객체에는 어떤 정보가 담겨있을까요?
  ```
  - createServer를 통해 생성된 server로 트랜잭션이 진행되면서 client의 request 정보가 req에 담겨지고, 이에 대한 server의 response 정보가 res에 담겨진다.

  - req(client가 server로 보내는 요청): 기본적으로 url 및 method 정보를 확인하며, 세부적인 정보는 method의 내부적인 property인 body에 담긴다

  - res(server가 client로 보내는 응답): client로 부터 받은 res정보를 적절한 logic으로 parsing하여 client에게 응답하는 정보가 담겨져 있다.
  ```
  * GET과 POST에 대한 처리 형태가 달라지는 이유는 무엇인가요?
  ```
  - GET이 리소스를 READ하기 위한 목적이라면, POST는 리소스를 기반으로 업데이트한 정보를 create하기 위한 목적이기 때문입니다.
  - GET은 READ이므로 멱등성의 특징을 지닌 반면, POST는 그렇지 않기 때문에 이러한 부분들을 고려할 수 있습니다.
  ```
* 만약 API 엔드포인트(URL)가 아주 많다고 한다면, HTTP POST 요청의 `Content-Type` 헤더에 따라 다른 방식으로 동작하는 서버를 어떻게 정리하면 좋을까요?
```
- endpoint 관련 문제
  client로 부터 많은 요청이 오고, 이에 따른 resource update(PUT req)가 발생
  HTML form tag로 부터의 request등 예상치 못한 API exception이 발생

- 방안
  미들웨어에서 parsing하는 부분을 더 효율적으로 구상
  content-type을 json방식 혹은 x-www-url-encoded 방식으로 제공하는 두 개의 method를 구상하는 등 지원하는 data 형식을 확인한다.
```
  * 그 밖에 서버가 요청들에 따라 공통적으로 처리하는 일에는 무엇이 있을까요? 이를 어떻게 정리하면 좋을까요?
  ```
  - 기본적으로 http module을 사용한다면 res 인자에 server 응답 정보가 담겨져 온다.
  이 res인자를 parsing하여 client가 어떠한 가공된 정보를 받아야 하는지 결정하고 구현
  ```

## Quest
* 다음의 동작을 하는 서버를 만들어 보세요.
  * 브라우저의 주소창에 `http://localhost:8080`을 치면 `Hello World!`를 응답하여 브라우저에 출력합니다.
  * 서버의 `/foo` URL에 `bar` 변수로 임의의 문자열을 GET 메소드로 보내면, `Hello, [문자열]`을 출력합니다.
  * 서버의 `/foo` URL에 `bar` 키에 임의의 문자열 값을 갖는 JSON 객체를 POST 메소드로 보내면, `Hello, [문자열]`을 출력합니다.
  * 서버의 `/pic/upload` URL에 그림 파일을 POST 하면 서버에 보안상 적절한 방법으로 파일이 업로드 됩니다.
  * 서버의 `/pic/show` URL을 GET 하면 브라우저에 위에 업로드한 그림이 뜹니다.
  * 서버의 `/pic/download` URL을 GET 하면 브라우저에 위에 업로드한 그림이 `pic.jpg`라는 이름으로 다운로드 됩니다.
* expressJS와 같은 외부 프레임워크를 사용하지 않고, node.js의 기본 모듈만을 사용해서 만들어 보세요.
* 처리하는 요청의 종류에 따라 공통적으로 나타나는 코드를 정리해 보세요.

## Advanced
* 서버가 파일 업로드를 지원할 때 보안상 주의할 점에는 무엇이 있을까요?
