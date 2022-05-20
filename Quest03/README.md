# Quest 03. 자바스크립트와 DOM

## Introduction
* 자바스크립트는 현재 웹 생태계의 근간인 프로그래밍 언어입니다. 이번 퀘스트에서는 자바스크립트의 기본적인 문법과, 자바스크립트를 통해 브라우저의 실제 DOM 노드를 조작하는 법에 대하여 알아볼 예정입니다.

## Topics
* 자바스크립트의 역사
* 기본 자바스크립트 문법
* DOM API
  * `document` 객체
  * `document.getElementById()`, `document.querySelector()`, `document.querySelectorAll()` 함수들
  * 기타 DOM 조작을 위한 함수와 속성들
* 변수의 스코프
  * `var`, `let`, `const`

## Resources
* [자바스크립트 첫걸음](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps)
* [자바스크립트 구성요소](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Building_blocks)
* [Just JavaScript](https://justjavascript.com/)

## Checklist
* 자바스크립트는 버전별로 어떻게 변화하고 발전해 왔을까요?
```
S1 -> ES2 -> ES3 -> ES4 -> ES5 -> ES6/ES2015 -> ES7/ES2016 -> ES8/ES2017 -> ES9/ES2018

ES6: Default Parameters, Template Literals, Multi-line Strings, Destructuring Assignment, Enhanced Object Literals, Arrow Functions, Promises, Block-Scoped Constructs Let and Const, CLasses, Modules  등 새로운 내용들 추가

ES7: Array.prototype.includes(), Exponentiation operator,,

ES8: String padding, Object.values and Object.entries, Object.getOwnPropertyDescriptors, Trailing commas in function parameter lists and calls, Async functions

ES9: Object Rest/Spread, Promise finally, Async iteration, Regular expression

```
  * 자바스크립트의 버전들을 가리키는 ES5, ES6, ES2016, ES2017 등은 무엇을 이야기할까요?
  ```
  ES는 ECMAscript의 약자입니다. 자바스크립트를 표준화 하기위해 만들어진, ECMA-262 기술 규격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어를 말합니다.
  ```
  * 자바스크립트의 표준은 어떻게 제정될까요?
  ```
  ECMA International 표준화 기구에 의해서 제정됩니다.
  ```
* 자바스크립트의 문법은 다른 언어들과 비교해 어떤 특징이 있을까요?
```
프로토타입 기반의 프로그래밍 언어. 스크립트 언어이다. 모든 웹 브라우저에 인터프리터가 내장되어 있다. 특징적인 부분으로는 동적 선언과 비동기처리이다.

동적선언: Javascript에서는 자료형과 변수의 형태를 일치시키지 않아도 되는 런타임형 언어이며, 다른 정적언어(C, C++, Java)에 비해 디버깅 오류가 자주 발생할 수 있다.

비동기처리: Javascript의 코드 실행은 순차적으로 이루어지지 않으며, 이전 코드의 실행결과가 이후 코드의 실행원인에 영향을 주는 것을 보장하지 않는다.
```
  * 자바스크립트에서 반복문을 돌리는 방법은 어떤 것들이 있을까요?
  ```
  for(var i=0; i < selectObject.options.length; i++)

  do{
    i= i+1; result = result + i
  } while(i < 5)

  n = 0;
  x = 0;
  while (n < 3) {
    n++;
    x+=n;
  }

  단, 실무에서는 이러한 원론적인 반복문보다는 map과 같은 특수목적의 메서드를 더 많이 활용한다.
  ```
* 자바스크립트를 통해 DOM 객체에 CSS Class를 주거나 없애려면 어떻게 해야 하나요?
```
sampleDOM.classList.add('주거나');
sampleDOM.classList.Remove('없애거나');
```
  * IE9나 그 이전의 옛날 브라우저들에서는 어떻게 해야 하나요?
  ```
  ~IE9에서는 지원이 안되므로, Pollyfill을 이용(웹 개발에서 기능을 지원하지 않는 웹 브라우저 상의 기능을 구현하는 코드)
  https://gist.github.com/devongovett/1381839
  https://github.com/eligrey/classList.js
  ```
* 자바스크립트의 변수가 유효한 범위는 어떻게 결정되나요?
```
- 기본적으로 선언한 변수는 하나의 component 및 function 등 변수가 선언된 요소 내부에서만 유효하다.
- project내부의 모든 script에 유효한 변수로 적용이 필요한 경우엔, 전역변수를 별도 지정해주어야한다.
```
  * `var`과 `let`으로 변수를 정의하는 방법들은 어떻게 다르게 동작하나요?
  ```
  - var는 이전부터 Javascript에서 변수를 선언하는 방식이었으며, 동일한 변수명을 가져도 중복된 변수선언이 가능하였다.
  - 변수를 var로 중복선언하는 것에 대한 오류를 줄이기 위해, let키워드로 변수를 선언하는 방법이 추가되었다.
  - const는 상수값을 선언할 때 사용하며, 재선언 및 재할당 모두 불가능하다.
  ```
* 자바스크립트의 익명 함수는 무엇인가요?
```
Javascript의 특성상 함수 자체가 변수, 또 다른 함수의 인자, return 등으로 활용 될 수 있다.
이렇게 함수 표현식의 경우 익명함수가 될 수 있고, 함수 선언식은 반드시 이름이 있어야 한다.
```
  * 자바스크립트의 Arrow function은 무엇일까요?
  ```
  화살표 함수 표현(arrow function expression)은 전통적인 함수 표현(function)의 간편한 대안입니다. 하지만, 화살표 함수는 몇 가지 제한점이 있고 모든 상황에 사용할 수 없습니다.
  - this나 super에 대한 바인딩이 없고, methods로 사용될 수 없습니다.
  - new.target 키워드가 없습니다.
  - 일반적으로 스코프를 지정할 때 사용하는 call, apply, bind methods를 이용할 수 없습니다.
  - 생성자(Constructor)로 사용할 수 없습니다.
  - yield를 화살표 함수 내부에서 사용할 수 없습니다.
  ```

## Quest
* (Quest 03-1) 초보 프로그래머의 영원한 친구, 별찍기 프로그램입니다.
  * [이 그림](jsStars.png)과 같이, 입력한 숫자만큼 삼각형 모양으로 콘솔에 별을 그리는 퀘스트 입니다.
    * 줄 수를 입력받고 그 줄 수만큼 별을 그리면 됩니다. 위의 그림은 5를 입력받았을 때의 결과입니다.
  * `if`와 `for`와 `function`을 다양하게 써서 프로그래밍 하면 더 좋은 코드가 나올 수 있을까요?
  * 입력은 `prompt()` 함수를 통해 받을 수 있습니다.
  * 출력은 `console.log()` 함수를 통해 할 수 있습니다.
* (Quest 03-2) skeleton 디렉토리에 주어진 HTML을 조작하는 스크립트를 완성해 보세요.
  * 첫째 줄에 있는 사각형의 박스들을 클릭할 때마다 배경색이 노란색↔흰색으로 토글되어야 합니다.
  * 둘째 줄에 있는 사각형의 박스들을 클릭할 때마다 `enabled`라는 이름의 CSS Class가 클릭된 DOM 노드에 추가되거나 제거되어야 합니다.
* 구현에는 여러 가지 방법이 있으나, 다른 곳은 건드리지 않고 TODO 부분만 고치는 방향으로 하시는 것을 권장해 드립니다.

## Advanced
* Quest 03-1의 코드를 더 구조화하고, 중복을 제거하고, 각각의 코드 블록이 한 가지 일을 전문적으로 잘하게 하려면 어떻게 해야 할까요?
* Quest 03-2의 스켈레톤 코드에서 `let` 대신 `var`로 바뀐다면 어떤 식으로 구현할 수 있을까요?
