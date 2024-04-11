## 코드 빌드에서 SpringBoot 3.x 버전과 Java 17 버전 호환문제

빌드 과정에서 다음과 같은 에러 발생

```
Other compatible attribute: - Doesn't say anything about org.gradle.plugin.api-version (required '8.7') - Variant 'mavenOptionalRuntimeElements' declares a library for use during runtime, packaged as a jar, and its dependencies declared externally: - Incompatible because this component declares a component, compatible with Java 17 and the consumer needed a component, compatible with Java 11 - Other compatible attribute: - Doesn't say anything about org.gradle.plugin.api-version (required '8.7') - Variant 'runtimeElements' declares a library for use during runtime, packaged as a jar, and its dependencies declared externally: - Incompatible because this component declares a component, compatible with Java 17 and the consumer needed a component, compatible with Java 11 - Other compatible attribute: - Doesn't say anything about org.gradle.plugin.api-version (required '8.7') - Variant 'sourcesElements' declares a component for use during runtime, and its dependencies declared externally: - Incompatible because this component declares documentation and the consumer needed a library - Other compatible attributes: - Doesn't say anything about its elements (required them packaged as a jar) - Doesn't say anything about its target Java version (required compatibility with Java 11) - Doesn't say anything about org.gradle.plugin.api-version (required '8.7')
```

에러 내용 :
	- Gradle 빌드 과정에서 발생한 에러
	- 프로젝트 또는 의존성 중 하나가 Java 17을 사용하여 컴파일 되었으나
	- 프로젝트 설정이 Java 11과의 호환성을 요구하고 있음

해결 내용 :
- gradle 설정이 java 17로 되어있는지 확인
	- [# Spring Boot 3.x 실행이 안될 경우 (feat. IntelliJ)](https://jojoldu.tistory.com/698)
- gradle 버전이 8.7 로 설치되어있는지 확인
	- [[AWS] EC2 에 Spring boot 올리는 과정 및 삽질 (with java 17 + spring boot3.0)](https://thalals.tistory.com/408)
- build.gradle파일에 `targetCompatibility` 설정 추가
```java
sourceCompatibility = '17'
targetCompatibility = '17'
```
- 프로젝트에서 node-gradle을 사용했기 때문에, node와 npm 또한 EC2에 설치를 해줘야한다.