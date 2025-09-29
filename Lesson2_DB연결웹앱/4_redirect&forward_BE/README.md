# 4. redirect & forward - BE
## 1) redirect
### 리다이렉트
- HTTP 프로토콜로 정해진 규칙이다.
- 서버는 클라이언트로부터 요청을 받은 후, 클라이언트에게 특정 URL로 이동하라고 요청할 수 있다. 이를 리다이렉트라고 한다.
- 서버에서는 클라이언트에게 응답으로 상태코드를 302와 함께 이동할 URL 정보를 Location 헤더에 담아 전소앟ㄴ다.
- 클라이언트는 서버로부터 받은 상태값이 302면 Location 헤더값으로 재요청을 보내게 된다.
- 이 때, 브라우저의 주소창은 전송받은 URL로 바뀌게 된다.
- 서블릿이나 jsp는 redirect 하기 위해서 HttpServletResponse가 가지고 있는 sendRedirect()메소드를 사용한다.
### redirect 실습
- 웹 브라우저가 redirect01.jsp을 요청
- redirect01은 redirect02.jsp로 리다이렉팅하는 로직이 실행되도록 함
- 브라우저에서 리다이렉트 확인
  - redirect01.jsp를 실행하면 서버로부터 응답코드로 302를 받는 것을 확인 가능
## 2) forward
### forward 이해하기
- forward란?
1. 웹 브라우저에서 Servlet1에게 요청을 보냄
2. Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송
### forward 실습
- FrontServlet, NextServlet 작성
- FrontServlet에서는 랜덤한 주사위 값을 구하고, 그 값을 NextServlet에게 forward
- NextServlet에서는 FrontServlet으로 부터 전달받은 주사위 값만큼 hello를 출력
## 3) Servlet & JSP 연동
### Servlet과 JSP 연동
- Servlet은 프로그램 로직이 수행되기에 유리하다. IDE 등에서 지원을 좀 더 잘해준다.
- JSP는 결과를 출력하기에 Servlet보다 유리하다. 필요한 html문을 그냥 입력하면 된다.
- 프로그램 로직 수행은 Servlet에서, 결과 출력은 JSP에서 하는 것이 유리하다.
- Servlet과 JSP의 장단점을 해결하기 위해서 Servlet에서 프로그램 로직이 수행되고, 그 결과를 JSP에게 포워딩하는 방법이 사용되게 되었다.
### 실습
- LogicServlet에서 1부터 100 사이의 random한 값 2개와, 그 값의 합을 구한 후 그 결과를 result.jsp에 포워딩하는 방법을 전송하여 결과를 출력한다.
