# Quest 02. CSS의 기초와 응용

## Introduction
* CSS는 Cascading StyleSheet의 약자입니다. 웹브라우저에 표시되는 HTML 문서의 스타일을 지정하는 (거의) 유일하지만 다루기 쉽지 않은 언어입니다. 이번 퀘스트를 통해 CSS의 기초적인 레이아웃 작성법을 알아볼 예정입니다.

## Topics
* CSS의 기초 문법과 적용 방법
  * Inline, `<style>`, `<link rel="stylesheet" href="...">`
* CSS 규칙의 우선순위
* 박스 모델과 레이아웃 요소
  * 박스 모델: `width`, `height`, `margin`, `padding`, `border`, `box-sizing`
  * `position`, `left`, `top`, `display`
  * CSS Flexbox와 Grid
* CSS 표준의 역사
* 브라우저별 Developer tools

## Resources
* [MDN - CSS](https://developer.mozilla.org/ko/docs/Web/CSS)
* [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)
* [A complete guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [그리드 레이아웃과 다른 레이아웃 방법과의 관계](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Grid_Layout/%EA%B7%B8%EB%A6%AC%EB%93%9C_%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83%EA%B3%BC_%EB%8B%A4%EB%A5%B8_%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83_%EB%B0%A9%EB%B2%95%EA%B3%BC%EC%9D%98_%EA%B4%80%EA%B3%84)

## Checklist
* CSS를 HTML에 적용하는 세 가지 방법은 무엇일까요?
```
1. 인라인 스타일 적용
2. link하여 외부 스타일시트 사용(Internal Style Sheet)
3. <head>내부에 <style></style> 태그를 사용하여 스타일 작성
```
  * 세 가지 방법 각각의 장단점은 무엇일까요?
  ```
  1. 인라인 스타일로 적용할 경우 가독성이 떨어지고, 재사용이 불가능하다.
  3. 다른 html문서에서는 적용할 수 없음.
  ```
* CSS 규칙의 우선순위는 어떻게 결정될까요?
```
1. 속성 값 뒤에 !important를 붙인 속성
2. inline style attribute
3. id
4. class, 다른 attribute, Pseudo Class(ex. first-child)
5. tag element, Pseudo Element

+) 우선 순위가 같다면 개수가 많은 css가 우선 순위가 높다

```
* CSS의 박스모델은 무엇일까요? 박스가 화면에서 차지하는 크기는 어떻게 결정될까요?
```
문서의 레이아웃을 계산할 때, 브라우저의 렌더링 엔진은 표준 CSS 기본 박스 모델에 따라 각각의 요소를 사각형 박스로 표현합니다. CSS는 박스의 크기, 위치, 속성(색, 배경, 테두리 모양 등)을 결정합니다.

하나의 박스는 네 부분(영역)으로 이루어집니다.
각 영역을 콘텐츠 영역,
안쪽 여백(패딩) 영역,
테두리 영역,
그리고 바깥 여백(마진)영역

콘텐츠 영역(content area)는 콘텐츠 경계(content edge)가 감싼 영역으로,
글이나 이미지, 비디오 등 요소의 실제 내용을 포함합니다. 콘텐츠 영역의 크기는 콘텐츠 너비(콘텐츠 박스 너비)와 콘텐츠 높이(콘텐츠 박스 높이)입니다. 배경색과 배경 이미지를 가지고 있기도 합니다.
box-sizing 속성의 값이 기본값인 content-box 이며 요소가 블록 레벨 요소인 경우, 콘텐츠 영역의 크기를 width, min-width, max-width, height, min-height, max-height 속성을 사용해 명시적으로 설정할 수 있습니다.

안쪽 여백 영역(패딩 영역, padding area)은 안쪽 여백 경계(padding edge)가 감싼 영역으로, 콘텐츠 영역을 요소의 안쪽 여백까지 포함하는 크기로 확장합니다. 영역의 크기는 안쪽 여백 박스 너비와 안쪽 박스 높이입니다.

테두리의 두께는 border-width의 단축 속성인 border가 결정합니다. box-sizing 속성의 값이 border-box라면 테두리 영역의 크기를 width, min-width, max-width, height, min-height, max-height 속성을 사용해 명시적으로 설정할 수 있습니다. 박스의 배경은 테두리 바깥 경계까지 늘어나고, 그릴 땐 테두리에 가려집니다.

바깥 여백 영역(마진 영역, margin area)은 바깥 여백 경계(margin edge)가 감싼 영역으로, 테두리 요소를 확장해 요소와 인근 요소 사이의 빈 공간까지 포함하도록 만듭니다. 영역의 크기는 바깥 여백 박스 너비와 바깥 여백 박스 높이입니다.
```
* `float` 속성은 왜 좋지 않을까요?
```
float를 이용한 레이아웃을 작성할 때, 부모 요소가 자식 요소의 크기를 반영하지 못하는 문제가 발생한다.
예를 들어 자식 요소에 float를 설정하면 부모 요소의 높이가 초기화 되어 사라지게된다.
```
* Flexbox(Flexible box)와 CSS Grid의 차이와 장단점은 무엇일까요?
```
grid는 컨테이너이고, flex는 컨텐츠이다.
flex는 1차원 레이아웃 시스템(수직, 수평중 택1)이고 grid는 2차원 레이아웃 시스템(수직, 수평 둘 다 가능)

flex 단점: 브라우저 호환성, 마크업에 <div class="container"></div>를 추가해야함, 레이아웃을 정의하기에 직관적이지 않음.
```
* CSS의 비슷한 요소들을 어떤 식으로 정리할 수 있을까요?
```
그룹화
```

## Quest
* Quest 01에서 만들었던 HTML을 바탕으로, [이 그림](screen.png)의 레이아웃과 CSS를 최대한 비슷하게 흉내내 보세요. 꼭 완벽히 정확할 필요는 없으나 align 등의 속성은 일치해야 합니다.
* **주의사항: 되도록이면 원래 페이지의 CSS를 참고하지 말고 아무것도 없는 백지에서 시작해 보도록 노력해 보세요!**

## Advanced
* 왜 CSS는 어려울까요?
```
1. 어떤 CSS 규칙이 최종적으로 적용될지 예측하기 어렵다
2. CSS 규칙의 상호작용을 모두 알기 어렵다
3. 런타임 환경을 예상하기 어렵다
```
* CSS의 어려움을 극복하기 위해 어떤 방법들이 제시되고 나왔을까요?
```
1. BEM
  * Block, Element, Modifier를 의미함. 이 세 가지를 이용하여 이름을 짓고 __와 --로 구분
    ex)
    .header__navigation--navi-text {
      color: red;
    }
    일 때, header는 block, navigation은 Element, navi--text는 Modifier
  * BEM은 기본적으로 ID를 사용하지 않으며, class만을 사용
  * '어떻게 보이는가'가 아니라 '어떤 목적인가'에 따라 명명.
    ex) 에러 메시지를 띄우는 P 태그에게는 .red가 아닌 .error라는 이름을 준다.

2. 어떤 런타인 환경을 대상으로 할 지를 정하고 이 환경을 확실히 지원(전부다 완벽하게 동작하는 css를 작성하는 것은 어려움)
3. CSS 전처리기(CSS-Preprocessor) - css module
   * CSS가 가지는 여러 한계점들을 극복하기 위해 탄생한 CSS의 확장 버전
   * CSS의 문제점들을 Programmatically 한 방식. 즉 변수, 함수, 상속 등 일반적인 프로그래밍 개념을 사용가능(전처리기는 태생적으로 기존 css가 가질 수 있는 불리한 점 해결 위해 탄생
   * CSS 를 확장하기 위한 스크립팅 언어로 컴파일러를 통해 CSS 포맷으로 변환
   * CSS 전처리기에는 다양한 모듈이 존재(Sass/SCSS,less,Stylus,PostCSS)
   * 장점
     * 재사용성
         * 공통 요소 또는 반복적인 항목을 변수, 함수로 대체 가능
     * 시간적 비용 감소
         * 임의 함수 및 내장 함수로 인한 개발 시간적 비용 절약
     * 유지 관리
         * CSS코드를 여러 파일로 나눠 유지 보수성 향상
         * 중첩, 상속과 같은 요소로 인해 구조화된 코드로 유지 및 관리 용이
     * Learning curve 낮음
   * 단점
     * 전처리기를 위한 도구 필요 
```
* CSS가 브라우저에 의해 해석되고 적용되기까지 내부적으로 어떤 과정을 거칠까요?
```
(브라우저마다 다른 방식으로 작업을 처리합니다.)

1. 브라우저는 HTML을 로드
2. HTML을 DOM로 변환. DOM은 컴퓨터 메모리의 문서를 나타냅니다.
3. 그런 다음 브라우저는 포함된 이미지 및 비디오와 같은 HTML 문서에 연결된 CSS를 가져옵니다. Javascript는 작업에서 나중에 처리되므로 더 간단하게 하기위해 여기에서는 다루지 않습니다.
4. 브라우저는 가져온 CSS를 구문 분석하고 선택자 유형별로 다른 규칙을 다른 "buckets"으로 정렬합니다.
  ex) 요소, class, ID등 찾은 선택자를 기반으로 DOM의 어느 노드에 어떤 규칙을 적용해야 하는지 결정하고, 필요에 따라 스타일을 첨부함. (이 중간 단계를 render tree라고 함)
5. render tree는 규칙이 적용된 후에 표시되어야 하는 구조로 배치됩니다.
6. 페이지의 시각적 표시가 화면에 표시됩니다. (이 단계를 painting이라고 함)
```
* 웹 폰트의 경우에는 브라우저 엔진 별로 어떤 과정을 통해 렌더링 될까요?
