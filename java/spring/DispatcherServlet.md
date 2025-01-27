![[Pasted image 20250127155148.png]]
> 출처 : 네이버 백과사전

[[Spring MVC]] 요청 (혹은 HTTP 요청)을 처리하기 위한 가장 [[FrontContoller|앞단]]이다.  
`DispatcherServlet`을 통해서 모든 요청을 확인해서 적절한 핸들러로 전달한다.

# 간단한 확인
## `DispatcherServelet` 내 `doDispatch` 메소드
```java
// DispatcherServlet.java

/**  
 * Process the actual dispatching to the handler. * <p>The handler will be obtained by applying the servlet's HandlerMappings in order.  
 * The HandlerAdapter will be obtained by querying the servlet's installed HandlerAdapters * to find the first that supports the handler class. * <p>All HTTP methods are handled by this method. It's up to HandlerAdapters or handlers  
 * themselves to decide which methods are acceptable. * @param request current HTTP request  
 * @param response current HTTP response  
 * @throws Exception in case of any kind of processing failure  
 */@SuppressWarnings("deprecation")  
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {  
    HttpServletRequest processedRequest = request;  
    HandlerExecutionChain mappedHandler = null;  
    boolean multipartRequestParsed = false;  
  
    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);  
  
    try {  
       ModelAndView mv = null;  
       Exception dispatchException = null;  
  
       try {  
          processedRequest = checkMultipart(request);  
          multipartRequestParsed = (processedRequest != request);  
  
          // Determine handler for the current request.  
          mappedHandler = getHandler(processedRequest);  
          if (mappedHandler == null) {  
             noHandlerFound(processedRequest, response);  
             return;  
          }  
  
          // Determine handler adapter for the current request.  
          HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());  
  
          // Process last-modified header, if supported by the handler.  
          String method = request.getMethod();  
          boolean isGet = HttpMethod.GET.matches(method);  
          if (isGet || HttpMethod.HEAD.matches(method)) {  
             long lastModified = ha.getLastModified(request, mappedHandler.getHandler());  
             if (new ServletWebRequest(request, response).checkNotModified(lastModified) && isGet) {  
                return;  
             }  
          }  
  
          if (!mappedHandler.applyPreHandle(processedRequest, response)) {  
             return;  
          }  
  
          // Actually invoke the handler.  
          mv = ha.handle(processedRequest, response, mappedHandler.getHandler());  
  
          if (asyncManager.isConcurrentHandlingStarted()) {  
             return;  
          }  
  
          applyDefaultViewName(processedRequest, mv);  
          mappedHandler.applyPostHandle(processedRequest, response, mv);  
       }  
       catch (Exception ex) {  
          dispatchException = ex;  
       }  
       catch (Throwable err) {  
          // As of 4.3, we're processing Errors thrown from handler methods as well,  
          // making them available for @ExceptionHandler methods and other scenarios.          dispatchException = new ServletException("Handler dispatch failed: " + err, err);  
       }  
       processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);  
    }  
    catch (Exception ex) {  
       triggerAfterCompletion(processedRequest, response, mappedHandler, ex);  
    }  
    catch (Throwable err) {  
       triggerAfterCompletion(processedRequest, response, mappedHandler,  
             new ServletException("Handler processing failed: " + err, err));  
    }  
    finally {  
       if (asyncManager.isConcurrentHandlingStarted()) {  
          // Instead of postHandle and afterCompletion  
          if (mappedHandler != null) {  
             mappedHandler.applyAfterConcurrentHandlingStarted(processedRequest, response);  
          }  
          asyncManager.setMultipartRequestParsed(multipartRequestParsed);  
       }  
       else {  
          // Clean up any resources used by a multipart request.  
          if (multipartRequestParsed || asyncManager.isMultipartRequestParsed()) {  
             cleanupMultipart(processedRequest);  
          }  
       }  
    }  
}
```


---

1. HTTP 요청이 들어오면, `doDispatch` 에서 `getHandler` 호출을 통해 요청 처리에 필요한 핸들러를 찾는다. ([[#`DispatcherServelet` 내 `doDispatch` 메소드|Line 26]])
	- ![[Pasted image 20250127160025.png]]
2. 핸들러를 찾았으면, 실행을 위해 적절한 `HandlerAdapter` 형태로 담는다. ([[#`DispatcherServelet` 내 `doDispatch` 메소드|Line 33]]))
	- 핸들러가 다양한 방식으로 구현되었을 수 있기 때문에, 제너럴하게 실행 할 수 있게 어댑터 패턴을 적용한다.
3. 핸들러 어탭터를 통해 핸들러로 `invoke` 한다. ([[#`DispatcherServelet` 내 `doDispatch` 메소드|Line 33]])
4. 비동기 작업일 경우 `invoke` 이후 작업을 종료한다. ([[#`DispatcherServelet` 내 `doDispatch` 메소드|Line 52~53]])
	- 비동기 작업일 경우, invoke 과정에서 비동기 처리 가능한 형태로 반환되기 때문에 작업이 오래 점유되지 않는다.
	





