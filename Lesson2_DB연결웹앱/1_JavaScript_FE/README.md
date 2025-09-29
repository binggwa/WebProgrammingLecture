# JavaScript - FE
- 웹사이트에 있는 데이터를 관리하기 위해 데이터베이스를 이용해야 한다.
- mysql DB를 이용해 데이터를 쓰고, 읽고, 수정하고, 삭제하는 작업을 어떻게 하는지 배운다.
- Spring JDBC를 이용한 데이터베이스 활용법을 안다.
- 자바스크립트로 웹 화면의 다양한 요소를 움직이는 작업을 한다.
- DOM, 이벤트, 서버와 통신하는 Ajax 기술을 배운다.
- 서블릿, JSP의 **forward, redirect, 4개의 scope, JSP의 내장 객체** 등 중요한 키워드
- **자바스크립트, DOM, 이벤트**가 중요한 키워드
## 1) 자바스크립트 변수 - 연산자 - 타입
### 자바스크립트 버전
- ECMAScript(줄여서 ES)의 버전에 따라서 결정되고, 자바스크립트실행 엔진이 반영한다.
- ES5, ES6와 같은 식으로 버전을 일컫는다.
- 2018년 기준 ES6(ES2015)를 지원하는 브라우저가 많다.
### 변수
- 변수는 var, let, const 로 선언할 수 있다.
- 어떤 것을 사용하는가에 의해서 scope라는 변수의 유효범위가 달라진다.
ex)
```javaScript
var a = 2;
var a = "aaa";
var a = 'aaa';
var a = true;
var a = [];
var a = {};
var a = undefined; 
```
### 연산자
- 연산자 우선순위를 표현하기 위해서는 ()를 사용하면 된다.
- 수학연산자는 +,-,*,/,% 등이 있다.
- 논리 연산자, 관계연산자, 삼항연산자도 있음.
ex)
```JavaScript
const name = "crong";
const result = name || "codesquad";
console.log(result);
const name = "";
const result = name || "codesquad";
console.log(result);
```
- const는 한번 할당한 값은 재할당이 되지 않는다.
- ||은 왼쪽이 false면 오른쪽으로 넘어가고, 값이 있다면 왼쪽 값 반환
- &&은 오른쪽까찌 확인하므로, 오른쪽 값 반환. 하지만, 왼쪽 값이 false라면, 그 이후의 값은 확인하지 않고 false 반환
### 삼항연산자
- 간단한 비교와 값 할당은 삼항연산자를 사용할 수 있음.
ex)
```JavaScript
const data = 11;
const result = (data > 10) ? "OK" : "fail";
console.log(result);
```
### 연산자 - 비교연산자
- 비교는 ==보다는 ===를 사용한다. ==로 인한 다양한 오류 상황이 있기 때문.
ex)
```JavaScript
0 == false;
"" == false;
null == false;
0 == "0";
null == undefined; 
```
### 자바스크립트의 Type
- 자바스크립트 타입에는 다양한 것이 존재
- undefined, null, boolean, number, string, object, function, array, Date, RegExp
- 타입은 선언할 때가 아니고, 실행타임에 결정된다. 함수 안에서의 파라미터나 변수는 실행될 때 그 타입이 결정된다.
- 타입을 체크하는 또렷한 방법은 없다. 정확하게는 toString.call 을 이용해서 그 결과를 매칭하곤 하는데, 문자, 숫자와 같은 기본타입은 typeof 키워드를 사용해서 체크할 수 있다.
- 배열의 경우 타입을 체크하는 isArray함수가 표준으로 있다.
### MDN에서의 자바스크립트 타입/변수
- 자바스크립트의 변수는 var/let/const 가 있으며, 함수 스코프와 블록 스코프, 재할당 여부에 따라 나뉜다.
- 자바스크립트의 타입은 크게 primitive 타입과 객체 타입으로 나뉘며, Null, Undefined, Boolean, Number, BigInt, String, Symbol 등의 primitive 타입, 그 외 모든 것, 배열, 함수, 날짜, Map, Set 등이 객체 타입이다.
## 2) 자바스크립트 비교-반복-문자열
### 비교문
- if, else if, else 를 통해서 다양한 비교문을 사용할 수 있다.
- 로직을 분기하기 위해서 switch 문을 통해서도 해결할 수 있다.
### 반복문
- for 문이나 while 문을 사용해서 반복문을 구현할 수 있다.
ex)
```Java
function howMany(selectObject) {
    var numberSelected = 0;
    for (var i = 0; i < selectObject.options.length; i++) {
        if (selectObject.options[i].selected) {
            numberSelected++;
        }
    }
    return numberSelected;
}
```
- for 문의 반복 구간, i < arr.length; 에서 반복을 돌때마다 arr.length를 확인하기 때문에
var i = 0, len = arr.length; i < len; 과 같은 식으로 선언하면 성능개선이 된다.
### 문자열 처리
- 자바스크립트의 문자와 문자열은 같은 타입이다. 모두 문자열
- 다양한 메서드가 있음
ex)
```Java
"ab:cd".split(":");     // ["ab", "cd"]
"ab:cd".replace(":", "$");      // "ab$cd"
" abcde ".trim();       // "abcde"
```
## 3) 자바스크립트 함수
### 함수 - 함수의 선언
- 함수는 여러개의 인자를 받아서, 그 결과를 출력한다.
- 파라미터의 갯수와 인자의 갯수가 일치하지 않아도 오류가 나지 않는다.
- 파라미터가 1개일 때, 인자의 갯수가 0개라면, 파라미터는 undefined라는 값을 갖게 된다.
### 함수 - 함수 표현식
- 함수는 아래 printName과 같이 표현할 수도 있다.
- 함수선언문과 달리 선언과 호출순서에 따라서 정상적으로 함수가 실행되지 않을 수 있다.
```java
function test() {
    console.log(printName());
    var printName = function() {
        return 'anonymouse';
    }
} 
test();
//TypeError : printName is not a function
```
### 함수 표현식과 호이스팅
- 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 미리 다 모아서 선언한다.
- 함수 안에 있는 변수들을 모두 끌어올려서 선언한다고 해서, hoisting 이라고 한다.
- 아래 코드 역시 함수를 값으로 가지지만 어쨌든 printName도 변수임으로 끌어올려지게 되고, 값이 할당되기 전에 실행됬음으로 undefined이 할당된 상태이다.
```java
printName();
var printName = function(){}
```
### 함수 - arguments 속성
- 함수가 실행되면 그 안에서 arguments라는 특별한 지역변수가 존재한다.
- 자바스크립트 함수는 선언한 파라미터보다 더 많은 인자를 보낼 수도 있다.
- 이 때 넘어온 인자를 arguments로 배열의 형태로 하나씩 접근할 수가 있다.
- arguments는 배열타입은 아니다. 따라서 배열의 메서드를 사용할 수가 없다.
ex)
```java
function a() {
    console.log(arguments);
}
a(1,2,3);
```
### arrow function
- ES2015에는 arrow function이 추가됐다. 간단하게 함수를 선언할 수 있는 문법
```java
function getName(name) {
    return "Kim " + name;
} 
// 위아래 두개는 같은 함수이다.
var getName = (name) => "Kim " + name;
```
## 4) 자바스크립트 함수 호출 스택
### 함수 호출
- 자바스크립트 함수 호출 : 아래 코드는 run이 호출되고 그 다음에 printName이 호출된다.
```java
function printName(firstname) {
    var myname = "jisu";
    return myname + " ," + firstname;
} 

function run(firstname) {
    var firstname = firstname || "Youn";
    var result = printName(firstname);
    console.log(result);
}
```
- 브라우저에서 대부분 지정된 횟수만큼만 call stack을 쌓게 미리 설정해둔 경우가 많다.
- Maximum call stack size exceeded 오류가 뜰 수 있다.