# WEB UI 개발 - FE
## 1) window 객체 (setTimeout)
- 브라우저 개발을 하다보면, window라는 객체가 있다.
- window에는 많은 메서드들이 존재하며, 아래와 같이 사용할 수 있다.
- 별로 좋지 않은 UX라고도 함
- window는 전역객체라서 생략가능하다.
```java
window.setTimeout()
setTimeout()
```
### setTimeout 활용
- setTimeout은 낯설게 동작함
- 인자로 함수를 받고 있으며, 보통 나중에 실행되는 함수를 **콜백함수**라고도 함
- 자바스크립트는 함수를 인자로 받을 수 있는 특징이 있다. 함수를 반환도 가능
```java
function run() {
    setTimeout(funtion() {
        var msg = "hello codesquad";
        console.log(msg);       // 이 메시지는 즉시 실행되지 않는다.
    }, 1000);
}
run();
```
- setTimeout의 특성을 잘 이해하고, 지연실행이 필요한 경우에 잘 활용하면 좋다.
- setTimeout의 지연시간이 0ms 여도 나중에 나온다.
- 비동기는 이벤트 큐에 저장되어 있다가 모두 실행되고 나서 나중에 실행된다.
## 2) DOM과 querySelector
### DOM
- 브라우저에서는 HTML 코드를 DOM (Document Object Model)이라는 객체형태의 모델로 저장함
- 그렇게 저장된 정보를 DOM Tree 라고 함. 결국 HTML element는 Tree 형태로 저장됨
- 복잡한 DOM Tree를 탐색하기 위해 JavaScript로 탐색알고리즘을 구현하면 너무 힘들다.
- 그래서 브라우저에서는 DOM 개념을 통해 다양한 DOM API(함수묶음정도)를 제공하고 있다.
- 브라우저는 DOM Tree 찾고 조작하는 걸 쉽게 도와주는 여러가지 메서드(DOM API)를 제공한다.
### getElementById()
- ID정보를 통해서 찾을 수 있다.
### querySelector()
- document.querySelector("div");
- document.querySelector(".nav-line-2"); -> id는 #, 클래스는 .이 필요하다.
- CSS 스타일을 결정할 때 사용하던, Selector 문법을 활용해 DOM에 접근할 수 있다.
- 비슷하지만 다른 querySelectorAll이 있다.
## 3) Browser Event, Event object, Event handler
### Event
- 브라우저에는 많은 이벤트가 발생함
- 화면 크기 마우스 조절, 스크롤, 마우스로 이동, 무언가 선택 등
- 이벤트를 브라우저가 발생시켜주니, 어떤일을 하라고 할일을 등록할 수 있음
- HTML 엘리먼트별로 어떤 이벤트가 발생했을 때 특정 행위를 하고 싶다면, 대상엘리먼트를 찾고 어떤일을 등록하면 된다.
### 이벤트 등록
- 표준방법으로 addEventListener 함수
```java
var el = document.getElementById("outside");
el.addEventListener("click", function() {
    // do something..
}, false);
```
- addEventListener함수의 두번째 인자는 함수다.
- 나중에 이벤트가 발생할 때 실행되는 함수로 이벤트핸들러 or 이벤트리스너라고 한다.
## 4) AJAX 통신의 이해
### Ajax (XMLHTTPRequest 통신)
- 웹에 데이터를 갱신할 때, 브라우저 새로고침 없이 서버로부터 데이터를 받는 것이 좋겠다는 생각에서 출발한 기술
- 더 좋은 UX를 제공할 수 있다.
- 탭UI에서, 상단 탭을 누를때마다 컨텐츠가 달라지는 등, 누르지도 않은 탭의 컨텐츠까지 초기로딩시점에 모두 불러온다면
초기 로딩속도에 영향을 줄 것이다. 따라서 동적으로 필요한 시점에 컨텐츠를 받아와서 표현하는 것이 Ajax 기술의 활용 대표적인 경우다.
### JSON
- 표준적인 데이터 포맷을 결정하기 위해서 주로 JSON (JavaScript OBject Notation) 포맷을 사용한다.
- 서버와 클라이언트로 데이터를 주고받을 때 많이 사용한다.
### AJAX 실행코드
```java
function ajax(data) {
    var oReq = new XMLHttpRequest();
    oReq.addEventListener("load", function() {
        console.log(this.responseText);
    });
    oReq.open("GET", "http://www.example.org/~~");
    oReq.send();
}
```
- XMLHttpRequest 객체를 생성해서, open 메서드로 요청을 준비하고, send 메서드로 서버로 보낸다.
- 요청처리가 완료되면 (서버로 응답이 오면) load 이벤트가 발생하고, 콜백함수가 실행된다.
- 콜백함수가 실행될 때는 이미 ajax함수는 반환하고 콜스택에서 사라진 상태
## 5) JavaScript Debugging
- 자바스크립트는 런타임에 실행되는 코드이기 때문에, 브라우저에서 디버깅을 많이 한다.
- 