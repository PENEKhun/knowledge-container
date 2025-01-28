> Java에서 HTTP 요청을 처리하기 위한 API  


Servlet API를 통해 Application을 작성하면, tomcat과 같은 WAS를 통해 손쉽게 구동할 수 있다.  

- 이용 예시
	- Repository :  https://github.com/PENEKhun/pratice-servlet
	```java
@WebServlet("/penek")  
public class HelloServlet extends HttpServlet {  
  
    @Override  
    protected void doGet(HttpServletRequest request, HttpServletResponse response)  
            throws IOException {  
        response.setContentType("text/html");  
        response.getWriter().println("<h1>Hello, World!</h1>");  
    }  
}
```





