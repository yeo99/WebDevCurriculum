# Quest 07. node.js의 기초

## Introduction
* 이번 퀘스트에서는 node.js의 기본적인 구조와 개념에 대해 알아 보겠습니다.

## Topics
* node.js
* npm
* CommonJS와 ES Modules

## Resources
* [About node.js](https://nodejs.org/ko/about/)
* [Node.js의 아키텍쳐](https://edu.goorm.io/learn/lecture/557/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-node-js/lesson/174356/node-js%EC%9D%98-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90)
* [npm](https://docs.npmjs.com/about-npm)
* [npm CLI commands](https://docs.npmjs.com/cli/v7/commands)
* [npm - package.json](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)
* [How NodeJS Require works!](https://www.thirdrocktechkno.com/blog/how-nodejs-require-works)
* [MDN - JavaScript Modules](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)
* [ES modules: A cartoon deep-dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
* [require vs import](https://www.geeksforgeeks.org/difference-between-node-js-require-and-es6-import-and-export/)

## Checklist
* node.js는 무엇인가요? node.js의 내부는 어떻게 구성되어 있을까요?
```
- Javascript 언어로 동작하는 (Javascript 엔진 기반의) 웹 애플리케이션 프레임워크다.
- non-blocking I/O 및 단일 스레드 동작을 통해 효율적인 네트워킹을 가능하게 한다.
- 이에 따라 기존 client 기반의 Javascript 특징을 Server 영역까지 확장할 수 있게 되었다.

- node.js의 가장 강력한 기능이자 특징은 single thread, asynchronized pattern이다.
- 전통적인 Web 프레임워크에 비해 훨씬 간단하고 효율적인 방식으로, 다수의 request 처리가 가능하고 빠른 응답을 구현할 수 있게 되었다.
```
* npm이 무엇인가요? `package.json` 파일은 어떤 필드들로 구성되어 있나요?
```
- Node Package Module의 약자로써 자바스크립트 프로그래밍 언어를 위한 패키지 관리자이다.
- 자바스크립트 런타임 환경 Node.js의 기본 패키지 관리자이다.
- package.json 파일은 배포한 모듈 정보를 담고자 만들어졌다.
- package.json 파일은 기본적으로 CommonJS의 명세를 충실히 따르고 있으며 JSON 형식의 파일이다.
- 직접 작성할 수도 있고, npm init 명령을 통해서 자동으로 생성할 수도 있다.

- name과 version필드는 필수항목이며 이 값 없이는 package를 설치할 수 없습니다.
- 위 두 필드는 유일하면서 중복되지 않는 식별자를 구성합니다. 패키지가 변경되면 버전도 같이 변경되어야 합니다.
- description(설명, npm search로 검색 가능)
- keywords(npm search로 검색 가능)
- homepage(프로젝트의 홈페이지 주소를 기록)
- bugs(프로젝트의 이슈 트랙커의 주소, 이슈를 보고할 수 있는 이메일 주소)
- license(사용자들이 사용상의 허용범위를 확인할 수 있도록 패키지의 라이센스를 지정)
- people fields: author, contributors(author는 개인을, contributors는 여러 사람들의 배열을 기록. "person"은 "name"필드를 가진 객체로써 url과 email필드는 옵션)

- files(프로젝트에 포함시킬 파일들의 배열. 이 배열에 폴더 이름을 기록하면 해당 폴더내의 모든 파일들이 포함. 패키지 최상위 폴더나 하위 폴더에 ".npmignore" 파일이 있고. 여기에 기록된 파일들은 files 배열에 포함되어있더라도 패키지에서 제외됨. git ignore와 동일한 방법)
- 설정과 관련없이 항상 포함되는 파일들
  package.json
  README (및 여기에 해당되는 여러가지 변형파일들)
  CHANGELOG (와 여기에 해당되는 변형 파일들)
  LICENSE/LICENCE
- 여기에 대비해서 다음의 파일들은 항상 제외
  .git
  CVS
  .svn
  .hg
  .lock-wscript
  .wafpickle-N
  *.swp
  .DS_Store
  ._*
  npm-debug.log

- main(프로그램의 시작 포인트를 가리키는 모듈ID. 패키지 이름이 foo라고 한다면 이 패키지를 설치한 사용자가 require("foo")를 호출하면 패키지의 메인 모듈이 익스포트한 객체를 반환받게 됩니다. 모듈 ID는 패키지 폴더의 최상위를 기준으로한 상대 경로)
(나머지는 https://outofbedlam.gitbooks.io/npm-handbook/content/config/package-json.html 참고)
```
* npx는 어떤 명령인가요? npm 패키지를 `-g` 옵션을 통해 글로벌로 저장하는 것과 그렇지 않은 것은 어떻게 다른가요?
```
- node package execution, 노드 패키지의 실행에 중점을 둔 명령어
- npm의 영구적인 설치, 관리 등의 부가적인 절차 없이 원하는 패키지를 npm 레지스트리에 접근시켜 실행만 할 수 있도록 설치하는 일종의 실행도구이다.
- 말 그대로 실행목적의 실행도구이기 때문에, 빠른 실행결과를 보고자 할 때 별도의 패키지 업데이트나 관리할 필요없이 손쉬운 실행이 가능하다.

- npm local 설치시)
  프로젝트 폴더 내의 ./node_modules/.bin 에 설치
- npm global 설치시)
  Linux의 경우 /usr/local/bin 에
  Windows의 경우 %appdata%/npm 에
```
* 자바스크립트 코드에서 다른 파일의 코드를 부르는 시도들은 지금까지 어떤 것이 있었을까요? CommonJS 대신 ES Modules가 등장한 이유는 무엇일까요?
```
- CommonJS?: ESModules를 제외하고도 HTML에서의 script, AMD, UMD 등이 있었다.
  HTML에서 script를 통해 여러개의 js를 불러오면 전역으로 정의되며 함수명, 변수명이 재정이됨에 따라 오염되는 현상이 있었다.
  브라우저 외부에서도 JS를 실행할 수 있는 구글의 V8엔진이 등장, JS의 서버 런타임 아이디어 등장
  => 이로인해 모듈화의 필요성 제기
  CommonJS(AMD, UMD 포함)은 JS를 브라우저 뿐 아니라 server-side/desktop application에서도 사용할 수 있도록 하는 것이었다.
  여러개의 단체에서 각각 모듈을 만든 것은, 결국 그들의 철학이 충돌했기 때문인데, 결국 JS언어 자체에서 module system을 지원해야 할 필요성이 생겼고, 결과적으로 ES6에서 ESmodule을 직접 지원하기 시작했다.
```
* ES Modules는 기존의 `require()`와 동작상에 어떤 차이가 있을까요? CommonJS는 할 수 있으나 ES Modules가 할 수 없는 일에는 어떤 것이 있을까요?
```
- CommonJS는 동적으로, ESM은 정적으로 작동한다.
  그렇기 때문에 commonJS는 if(~) require(~)가 가능하지만 ESM은 가능하지 않다.
  미리 종속성 그래프(dependencies graph)를 그리지 않고 필요한 순간에 가져다 쓰는 방식
  여기서 순환참조에 대한 한계점이 드러난다. 이로인해 CommonJS는 tree shaking에도 약할 수 밖에 없다.

  ESM은 정적으로 작동 (즉, 종속성 그래프를 모두 그려놓고 시작하기에, 순환참조를 극복)

- call by value vs call by reference
  CommonJS는 call by value 방식, ESM은 call by reference 방식이다.
  그렇기 때문에 이미 파일을 불러온 후에, 원본파일에서 비동기처리로 값이 바뀌면, ESM은 이를 인식하고, CommonJS는 인식하지 못한다.
  + ESM을 통해 불러오면 CONST처리가 되어서 import해서는 수정이 불가능
```
* node.js에서 ES Modules를 사용하려면 어떻게 해야 할까요? ES Modules 기반의 코드에서 CommonJS 기반의 패키지를 불러오려면 어떻게 해야 할까요? 그 반대는 어떻게 될까요?
```
- nodeJS에서 ES Module 사용하기
  파일 단위: .mjs로 파일 확장자 변경 후 사용
  프로젝트 단위: package.json에 type:module을 적으면 js확장자로도 이용 가능

- ESM 기반에서 CommonJS 사용하기
  default import로 가능 / 내부적인 메서드는 CJS.method1()과 같이 .을 찍어서 이용가능
```

```
+ require는 프로그램의 어느 지점에서나 호출 할 수 있지만 import()는 파일의 시작 부분에서만 실행할 수 있습니다(import 전용 비동기 문법으로 처리하면 가능).
+ require와 import는 동시에 사용 불가능
+ import()는 사용자가 필요한 모듈 부분만 선택하고 로드가 가능.
```

## Quest
* 스켈레톤 코드에는 다음과 같은 네 개의 패키지가 있으며, 용도는 다음과 같습니다:
  * `cjs-package`: CommonJS 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  * `esm-package`: ES Modules 기반의 패키지입니다. 다른 코드가 이 패키지의 함수와 내용을 참조하게 됩니다.
  * `cjs-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, CommonJS 기반의 프로젝트입니다.
  * `esm-my-project`: `cjs-package`와 `esm-package`에 모두 의존하는, ES Modules 기반의 프로젝트입니다.
* 각각의 패키지의 `package.json`과 `index.js` 또는 `index.mjs` 파일을 수정하여, 각각의 `*-my-project`들이 `*-package`에 노출된 함수와 클래스를 활용할 수 있도록 만들어 보세요.

## Advanced
* node.js 외의 자바스크립트 런타임에는 어떤 것이 있을까요?
