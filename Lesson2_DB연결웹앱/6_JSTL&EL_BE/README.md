# JSTL & EL - BE
## 1) EL (Expression Language)
### 표현 언어
- 값을 표현하는 데 사용되는 스크립트 언어로서 JSP의 기본 문법을 보완하는 역할을 한다.
- 표현 언어가 제공하는 기능
  - JSP의 스코프(scope)에 맞는 속성 사용
  - 집합 객체에 대한 접근 방법 제공
  - 수치 연산, 관계 연산, 논리 연산자 제공
  - 자바 클래스 메소드 호출 기능 제공
  - 표현언어만의 기본 객체 제공
### 표현 언어의 표현 방법
- 문법
  - ${expr}
  - expr - 표현언어가 정의한 문법에 따라 값을 표현하는 식
- ex)
  - < jsp:include page ="/module/${skin.id}/header.jsp" flush = "true" />
  - <b>${sessionScope.member.id}</b>님 환영합니다.
- 표현언어는 JSP의 스크립트 요소 (스크립트릿, 표현식, 선언부)를 제외한 나머지 부분에서 사용될 수 있으며, 표현식을 통해서
보다 편리하게 값을 출력할 수 있다.
### 표현 언어의 데이터 타입
- boolean 타입 - true, false
- 정수 타입 - 0~9 로 이루어진 정수 값, 음수의 경우 '-'가 붙음
- 실수 타입 - 0~9로 이루어져 있으며, 소숫점을 사용할 수 있고 3.24e3과 같은 지수형 표현 가능
- 문자열 타입 - 따옴표로 둘러싼 문자열. 작은 따옴표(')를 사용해서 표현할 경우 값에 포함된 작은 따옴표는 \'와 같이 \ 기호와 함께 사용해야 한다.
- \ 기호 자체는 \\로 표시한다.
- 널 타입 - null
### 객체 접근 규칙
- ${<표현1>.<표현2>}
- 둘 중 하나가 null이면 null 반환
- 표현1이 Map일 경우, 표현2를 key로한 값을 반환한다.
- 표현1이 List일 경우, 표현2가 정수일 경우 해당 정수번째 index에 해당하는 값을 반환한다.
- 정수가 아닐 경우, 오류 발생
- 표현1이 객체일 경우, 표현2에 해당하는 getter메소드에 해당하는 메소드를 호출한 결과를 반환한다.
### 수치 연산자 사용 가능
- +, -, *, /, %
- 숫자로 변환할 수 없는 객체와 수치연산자를 함께 사용하면 에러 발생
- 수치 연산자에서 사용되는 객체가 null이면 0으로 처리
### empty 연산자, 비교선택 연산자
- empty <값>
1. 값이 null이면 true를 리턴한다
2. 값이 빈 문자열이면 true를 리턴한다
3. 값이 길이가 0인 배열이면 true를 리턴한다
4. 값이 빈 Map이면 true를 리턴한다
5. 값이 빈 Collection이면 true를 리턴한다
6. 이 외의 경우에는 false를 리턴한다
### 표현 언어 비활성화 가능 : JSP에 명시하기
- <%@ page isELIgnored = "true" %>
## 2) JSTL (JSP Standard Tag Library)
### JSTL이란?
- JSTL 은 JSP 페이지에서 조건문 처리, 반복문 처리 등을 html tag 형태로 작성할 수 있게 도와준다.
- JSTL을 사용함으로써 java코드를 없애고 태그형태로 표현할 수 있다.
### 코어 태그
- set
- remove
- if
- choose
- forEach
- forTokens
- import
- redirect
- url
- catch
- out
### 변수 지원 태그 - set, remove
- 변수 설정 : 지정한 영역에 변수를 생성한다.
- 문법
  - <c:set var="varName" scope="session" value="someValue" />
  - <c:set var="varName" scope="request">
  - some Value
  - </c:set>
- var : EL에서 사용될 변수명
- scope : 변수값이 저장될 영역
- value : 변수값
### 코어태그 : 변수 지원 태그 - 프로퍼티, 맵의 처리
- 문법
  - <c:set target="${some}" property="propertyName" value="anyValue" />
  - some 객체가 자바빈일 경우 : some.setPropertyName(anyValue)
  - some 객체가 맵(map)일 경우 : some.put(propertyName, anyValue);
### 코어태그 : 흐름제어 태그 - if
- 문법
  - <c:if test="조건">
  - test의 조건이 true이면 몸체 내용을 처리한다.
  - </c:if>
### 코어태그 : 흐름제어 태그 - choose
- 문법
  - <c:choose>
    - <c:when test="조건1">
    - ...
    - </c:when>
    - <c:otherwise>
    - ...
    - </c.otherwise>
  - </c:choose>
### 코어태그 : 흐름제어 태그 - forEach
- 배열 및 Collection에 저장된 요소를 차례대로 처리한다.
- 문법
  - <c:forEach var="변수" items="아이템" [begin="시작번호"][end="끝번호"]>
  - ...
  - ${변수}
  - ...
  - </c:forEach>
### 코어태그 : 흐름제어 태그 - import
- 지정한 URL에 연결하여 결과를 지정한 변수에 저장한다.
- 문법
  - <c:import url="URL" charEncoding="캐릭터인코딩" var="변수명" scope="범위">
    - <c:param name="파라미터이름" value="파라미터값" />
  - </c:import>
### 코어태그 : 흐름제어 태그 - redirect
- 지정한 페이지로 리다이렉트한다. response.sendRedirect()와 비슷
- 문법
  - <c:redirect url="리다이렉트할URL">
    - <c:param name="파라미터이름" value="파라미터값" />
  - </c:redirect>
### 코어태그 : 기타 태그 - out
- JspWriter에 데이터를 출력한다.
- 문법
  - <c:out value="value" escapeXml="{true|false}" default="defaultValue" />