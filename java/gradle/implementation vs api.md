
`build.gradle` 에서 아래와 같은 방법으로 종속성을 명시할 수 있다.
```groovy
dependencies {
	implementation project(":springdog-project:springdog-datastore") // 1번 방법
	api project(":springdog-project:springdog-datastore") // 2번 방법
}
```

여기서 사용된 [[Gradle dependencies blocks#implementation|implementation]]와 `api` 모두 runtime, compile classpath에 프로젝트를 포함시키는 것이다.

하지만 둘은 미묘하게 다르다.
# 차이점

```mermaid
graph LR;
    A[프로젝트 A] --> B[프로젝트 B];
    B --> C[프로젝트 C];

```
만약 프로젝트 A가 B를 참조하고, B가 C를 참조하고 있는 상황이라 가정해보자.

**implementation**은 프로젝트 A에서 B는 참조할 수 있지만, C는 참조할 수 없다.
하지만, **api**는 프로젝트 A가 B, C 모두 참조 가능하다.
