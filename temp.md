
- 껍데기 design
	- 조건사항
		- 공통 명세
			- ![[Pasted image 20250213154726.png]]
			- 근데 요건 불가능 할수도 OAS상으론,


JAVA/Spring 진영 에서는 REST docs를 사용해서 Test driven API document를 만들 수 있음.
하지만 JS진영에서는 이러한 라이브러리가 없다. 따라서 이를 만들려고 함.

# 인터페이스 예상 / 사용 방법 예상

restdocs의 mockMvc와 같은 문서를 위한 인터페이스를 대충 설계하고자 함.

- 중점으로 두는 것
	- 어떻게하면 사용자 입장에서 가독성 좋게 테스트를 작성할 수 있을지
		- 테스트코드에 문서를 위한 중복코드가 많이 발생하면 안됨.
			- 모카나, JEST의 인터페이스를 wrapping한 custom한 DSL를 만들어야 함.
			  그래야 하나의 API당 동일 describe()로 묶어 API 설명을 함께 보내어,
			  it(test case)마다 api정보를 dry하게 유지할 수 있을 것 같음.
	- 또한 기술적으로 충분히 구현가능한 방식의 인터페이스여야 함.

## 1안		

```js
describe("GET", "/api/v1/users", {
	name : "사용자 목록 조회", // API 이름
	tag : "user", // 분류 태그
	description : "사용자의 목록을 조회합니다.", // API 상세 설명	
}, (document) => {

	// API의 세부 동작 명세
	it("조회 성공", () => {
		document
			.requestHeaders(
				header("Authorization", "접속에 필요한 JWT 토큰 값", "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c")
			)
			.requestParam(
				field("page", "조회할 페이지", 1),
			)
			.responseStatus(HTTP_STATUS.OK)
			.responseBody(
				field("result", "조회된 사용자 목록", {
					id: 1,
					username: "penekhun",
					name: "문성훈"
				}),
				ignoredField("status")
			)
	});
	
	it("페이지가 음수인 경우엔 에러 발생", () => {
		api...
	});
})
```


## 2안

```js
describeAPI("GET", "/api/v1/users/{userId}", {
  name: "사용자 상세 조회",
  tag: "admin",
  description: "관리자가 특정 사용자의 상세 정보를 조회합니다.",
  defaults: {
    requestHeaders: {
      Authorization: header(
        "Authorization",
        "관리자 인증 토큰 값",
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
      )
    }
  }
}, (apiDoc) => {
  itDoc("조회 성공", async () => {
    await apiDoc.test()
      .withPathParams({
        userId: field("조회할 사용자 ID", 1)
      })
      .withQueryParams({
        includeDetails: field("추가 정보를 포함할지 여부", true)
      })
      .expectStatus(HTTPStatus.OK)
      .expectResponseBody({
        username: field("사용자 이름", "penekhun"),
        name: field("사용자 이름", "문성훈")
      });
  });

  itDoc("존재하지 않는 사용자 조회 시 404 에러 발생", async () => {
    await apiDoc.test()
      .withPathParams({
        userId: field("조회할 사용자 ID", 9999)
      })
      .expectStatus(HTTPStatus.NOT_FOUND)
      .expectResponseBody({
        error: field("에러 메시지", "사용자를 찾을 수 없습니다.")
      });
  });

  itDoc("인증 정보가 없는 경우 접근 불가(401)", async () => {
    await apiDoc.test()
      .withoutHeader("Authorization")
      .withPathParams({
        userId: field("조회할 사용자 ID", 1)
      })
      .expectStatus(HTTPStatus.UNAUTHORIZED)
      .expectResponseBody({
        error: field("에러 메시지", "인증 정보가 필요합니다.")
      });
  });
});
```

- 주의사항 :
	- `PATH VARIABLE`은 고려되지 않은 인터페이스.



Bean Validation 같은 JsonSchema 보완도 지원해야함.
![[Pasted image 20250213180831.png]]



Error Code들에 대해서 상세 description이 되면 좋을련만
