# 5. Servlet - BE
## 1) Servlet 이란?
### 자바 웹 어플리케이션 (Java Web Application)
- WAS에 설치(deploy)되어 동작하는 어플리케이션
- 자바 웹 어플리케이션에는 HTML, CSS, 이미지, 자바로 작성된 클래스 (Servlet, package, 인터페이스 등), 각종 설정 파일 등이 포함된다.
### 자바 웹 어플리케이션의 폴더 구조
WEB_INF 폴더 +--- web.xml 파일 ( 배포기술자, DeploymentDescriptor : servlet 3.0미만 필수, 3.0이상은 어노테이션 사용)
            +--- lib 폴더 --- jar파일들
            +--- classes 폴더 ---- java 패키지, class들
리소스들
+--- 각종 폴더, 이미지, 다양한 리소스들
### Servlet이란?
- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- 서블릿을 정의해보면
  - WAS에서 동작하는 java 클래스
  - HttpServlet 클래스를 상속받아야 한다
  - 서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 2가지를 조화롭게 사용해야 한다.
  - ex) 웹 페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현
## 2) Servlet 작성 방법
### Servlet 작성방법은 2가지로 나뉨
1. Servlet 3.0 spec 이상에서 사용하는 방법
- web.xml파일을 사용하지 않음
- 자바 어노테이션을 사용
- ex) @WebServlet("/ten")
2. Servlet 3.0 spec 미만에서 사용하는 방법
- Servlet을 등록할 때 web.xml 파일에 <servlet-name>, <servlet-class>, mapping, <url-pattern>등으로 사용
### Servlet 3.0 spec 이상에서, 3.0 spec 미만에서 사용하는 방법
- Tenservlet 클래스 내부에 @WebServlet("/ten") annotation을 통해 서블릿 3.0 이상에서 주소 인지
- <display-name>, <servlet-name>,  <servlet-class>와 같은 servlet
- <servlet-name>, <url-pattern>을 이용한 <servlet-mapping>을 통해 3.0 미만에서 구현
```html
ex)
<?xml version="1.0" encoding="UTF-8"?>
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
         version="2.5">
    <display-name>exam25</display-name>
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>default.html</welcome-file>
        <welcome-file>default.htm</welcome-file>
        <welcome-file>default.jsp</welcome-file>
    </welcome-file-list>
    <servlet>
        <description></description>
        <display-name>TenServlet</display-name>
        <servlet-name>TenServlet</servlet-name>
        <servlet-class>exam.TenServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>TenServlet</servlet-name>
        <url-pattern>/ttt</url-pattern>
    </servlet-mapping>
</web-app>
```
## 3) Servlet 라이프 사이클
### LifecycleServlet 작성
- 서블릿 생명주기를 확인할 수 있는 LifecycleServlet을 작성한다.
- HttpServlet의 3가지 메소드를 오버라이딩
  - init()
  - service(request, response)
  - destroy()
```java
ex)
        package examples;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet("/LifecycleServlet")
public class LifecycleServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;


    public LifecycleServlet() {
        System.out.println("LifecycleServlet 생성!!");
    }

    public void init(ServletConfig config) throws ServletException {
        System.out.println("init test 호출!!");
    }


    public void destroy() {
        System.out.println("destroy 호출!!");
    }

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
    {
        System.out.println("service호출!!");
    }
}
```
- WAS는 서블릿 요청을 받으면, 해당 서블릿이 메모리에 있는지 확인
- 만약 메모리에 없다면,
  - 해당 서블릿 클래스를 메모리에 올림
  - init() 메소드를 실행
- service() 메소드를 실행
- WAS 가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 메소드가 실행됨
### service(request, response) 메소드
- HttpServlet의 service 메소드는 템플릿 메소드 패턴으로 구현
- 클라이언트의 요청이 GET일 경우에는 자신이 가지고 있는 doGet(request, response) 메소드를 호출
- 클라이언트의 요청이 POST일 경우에는 자신이 가지고 있는 doPost(request, response) 메소드를 호출
```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    response.setContentType("text/html");
    PrintWriter out = response.getWriter();
    out.println("<html>");
    out.println("<head><title>form</title></head>");
    out.println("<body>");
    out.println("<form method='post' action='/firstweb/LifecycleServlet'>");
    out.println("name : <input type='text' name='name'><br>");
    out.println("<input type='submit' value='ok'><br>");
    out.println("</form>");
    out.println("</body>");
    out.println("</html>");
    out.close();
}

protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    response.setContentType("text/html");
    PrintWriter out = response.getWriter();
    String name = request.getParameter("name");
    out.println("<h1> hello " + name + "</h1>");
    out.close();
}
```
- doGet에서, input text를 받는 창과, input submit 클릭 칸을 만들어두고, submit이 눌리면 form의 action의 클래스에서 method post를 실행하도록 한다.
- 이때, doPost에서는 name 파라미터를 받아와서 hello + name을 응답하게 된다.
## 4) Request, Response 객체 이해하기
### 요청과 응답
- WAS는 웹 브라우저로부터 Servlet 요청을 받으면,
- 요청할 때 가지고 있는 정보를 HttpServletRequest 객체를 생성하여 저장
- 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse 객체를 생성
- 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달
### HttpServletRequest
- http 프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용
- 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있다.
- Body의 Stream을 읽어들이는 메소드도 가지고 있다.
### HttepServletResponse
- WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServletresponse객체를 생성하여 서블릿에게 전달
- 서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메시지 등을 전송
### 헤더 정보 읽어 들이기
- 웹 브라우저가 요청정보에 담아서 보내는 header 값을 읽어 들여 브라우저 화면에 출력한다.
### 파라미터 읽어 들이기
- URL 주소의 파라미터 정보를 읽어들여 브라우저 화면에 출력한다.
```java
response.setContentType("text/html");
PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>form</title></head>");
        out.println("<body>");

String name = request.getParameter("name");
String age = request.getParameter("age");

        out.println("name : " + name + "<br>");
        out.println("age : " +age + "<br>");

        out.println("</body>");
        out.println("</html>");
```
- 위의 코드의 경우, name과 age를 받아오는 코드가 없기 때문에, url에 param?name=kim&age=5와 같이 값을 넣으면, 잘 표시된다.
### 그 외의 요청정보 출력
- URI, URl, PATH, Remote host 등에 대한 정보 출력
```java
response.setContentType("text/html");
PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>info</title></head>");
        out.println("<body>");

String uri = request.getRequestURI();
StringBuffer url = request.getRequestURL();
String contentPath = request.getContextPath();
String remoteAddr = request.getRemoteAddr();

        out.println("uri : " + uri + "<br>");
        out.println("url : " + url + "<br>");
        out.println("contentPath : " + contentPath + "<br>");
        out.println("remoteAddr : " + remoteAddr + "<br>");

        out.println("</body>");
        out.println("</html>");
```
- URI는 URL에서 포트번호 이하 부분이 출력됨
- URL은 요청정보 전체가 출력
- 기본적으로 현재 프로젝트 이름이 contentPath로 지정됨
- remoteAddr을 통해 클라이언트의 주소가 표시 -> 로컬호스트여서 1로 뜬다.
## 키워드 정리
1. 웹 프로그래밍 기초 - 웹 프론트엔드
- 프론트엔드와 백엔드의 역할과 관계
- HTML로 웹페이지 구조 설계
- CSS 레이아웃에 필요한 속성과 활용방법
2. 웹 프로그래밍 기초 - 웹 백엔드
- 웹 개발에 대한 이해
- 개발 환경 설정 (Tomcat, intellij)
- 서블릿 (Servlet)