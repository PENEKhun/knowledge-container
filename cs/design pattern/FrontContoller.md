FrontController는 앞단에서 공통된 로직을 중복없이 처리하는 패턴이다.

만약 이를 사용하지 않는다면 아래와 같이 [[DispatcherServlet]]을 매번 구현해야 할 것이다.
- *without* FrontController
![[Pasted image 20250127144749.png]]
> 이미지 출처 : https://jwdeveloper.tistory.com/291

사용한다면, 한개의 [[DispatcherServlet]] 으로 여러개의 요청을 처리할 수 있다.
- *with* FrontController
![[Pasted image 20250127144823.png]]