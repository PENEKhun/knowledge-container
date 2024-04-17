`build.gradle`를 보면 아래와 같은 dependency blocks이 있다.
```groovy
dependencies {
// ...
}
```

여기서 사용되는 키워드를 알아보자.
## implementation
`implementation`는 만능이라 전 scope에 적용된다. (테스트 포함) (어노테이션 프로세싱은 동작안됨)
## runtimeOnly
`runtimeOnly`는 런타임에서만 동작한다.
## compileOnly
`compileOnly`는 컴파일 단계에서만 동작하는 라이브러리 입니다. 따라서 빌드 결과물에 포함되지 않으므로 런타임에선 사용할 수 없다.
## annotationProcessor
`annotationProcessor`도 컴파일 단계에서 동작하지만, 추가적인 [어노테이션 프로세싱](어노테이션%20프로세서%20(Annotation%20Processor).md) 작업이 진행된다.
## testImplementation
`testImplementation`은 테스트에서만 적용된다.
## api
![[implementation vs api]]
