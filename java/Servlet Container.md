> WAS내부에서 [[Servlet]]의 생명주기를 관리하고, 클라이언트의 HTTP 요청을 처리할 수 있도록 함.

# Servlet 생명 주기
- **init**()
	- 초기 한번만 실행됨.
	- 서블릿을 초기화 하는 역할을 진행
- **service**()
	- 공용 서비스 메서드에서 표준 HTTP 요청을 수신하여 이 클래스에 정의된 doXXX 메서드로 전송합니다. 이 메서드를 재정의할 필요는 없습니다. ([ref : javadoc](https://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpServlet.html#service-javax.servlet.http.HttpServletRequest-javax.servlet.http.HttpServletResponse-))
	- 요청 발생시 `doGet` 혹은 `doPost`로 분기되어 실행됨.
- **destroy**()
	- 서블릿 컨테이너가 서블릿이 서비스 중단 중임을 서블릿에 알리기 위해 호출합니다. ([ref: javadoc](https://docs.oracle.com/javaee/7/api/javax/servlet/GenericServlet.html#destroy--))
	- 종료시 마지막에 한번 실행됨.
## 생명주기 순서 실험
- Example 코드
```java
package kr.huni;  
  
import jakarta.servlet.ServletConfig;  
import jakarta.servlet.ServletException;  
import jakarta.servlet.annotation.WebServlet;  
import jakarta.servlet.http.HttpServlet;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
  
import java.io.IOException;  
  
@WebServlet("/ServletLifeCycle")  
public class ServletLifeCycle extends HttpServlet {  
  
    public ServletLifeCycle() {  
        super();  
        System.out.println("ServletLifeCycle 생성자 실행");  
    }  
  
    public void init(ServletConfig config) {  
        System.out.println("init() 실행");  
    }  
  
    protected void service(HttpServletRequest request, HttpServletResponse response)  
            throws ServletException, IOException {  
        System.out.println("service() 실행");  
        super.service(request, response);  
    }  
  
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {  
        System.out.println("doGet() 실행");  
    }  
  
    protected void doPost(HttpServletRequest request, HttpServletResponse response) {  
        System.out.println("doPost() 실행");  
    }  
  
    public void destroy() {  
        System.out.println("destroy() 실행");  
    }  
}
```
- 순서
	- 첫 페이지 접속 시
		- `ServletLifeCycle 생성자 실행`
		- `init() 실행`
		- `service() 실행`
		- `doGet() 실행`
	- 두번째 접속 시
		- `service() 실행`
		- `doGet() 실행`
	- Application 종료시
		- `destory() 실행`
# 내부 동작


