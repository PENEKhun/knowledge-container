모카나, JEST의 인터페이스를 wrapping한 custom한 DSL를 만들어야 함.
그래야 하나의 API당 동일 describe()로 묶어 API 설명을 함께 보내어,
it(test case)마다 api정보를 dry하게 유지할 수 있을 것 같음.


- 껍데기 design
	- 조건사항
		- 공통 명세
			- ![[Pasted image 20250213154726.png]]
			- 근데 요건 불가능 할수도 OAS상으론,
		- API별 명세

```js
describe("GET", "/api/v1/login", {
	name : "로그인 API", // API 이름
	tag : "auth", // 분류 태그
	description : "아이디/패스워드 로그인을 통해 JWT 토큰을 가져옵니다", // API 상세 설명	
}, => () {
	// API의 세부 동작 명세
	it("사용자의 아이디가 짧은 경우 에러 발생", () => {
		
	})
})
```


- 대략적인 내부 design
	- 조건 사항
		- Request Structure
			- PATH (**required**)
			- Body
			- QueryString
			- Header

```js
it("입력 아이디가 비어있는 경우, 에러 발생", () => {
	request()
		.
});
```



Bean Validation 같은 JsonSchema 보완도 지원해야함.
![[Pasted image 20250213180831.png]]



Error Code들에 대해서 상세 description이 되면 좋을련만
