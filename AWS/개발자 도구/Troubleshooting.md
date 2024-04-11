---
tags:
  - Troubleshooting
  - AWS
  - CodeBuild
  - CodeDeploy
---
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
[# Spring Boot 3.x 실행이 안될 경우 (feat. IntelliJ)](https://jojoldu.tistory.com/698)
- gradle 버전이 8.7 로 설치되어있는지 확인
[[AWS] EC2 에 Spring boot 올리는 과정 및 삽질 (with java 17 + spring boot3.0)](https://thalals.tistory.com/408)
- build.gradle파일에 `targetCompatibility` 설정 추가
```java
sourceCompatibility = '17'
targetCompatibility = '17'
```
- 프로젝트에서 node-gradle을 사용했기 때문에, node와 npm 또한 EC2에 설치를 해줘야한다.
- ----
## 코드 디플로이에서 배포 실패

현재 상황

파이프라인에서 빌드까지 정상적으로 되었으나, 디플로이에서 실패함.

`The overall deployment failed because too many individual instances failed deployment, too few healthy instances are available for deployment, or some instances in your deployment group are experiencing problems.`

로그를 확인해본 결과 AWS CodeDeploy 에이전트는 정상적으로 작동하고 있는 것으로 확인됨.

```
1. **에이전트 버전**: 로그에는 CodeDeploy 에이전트의 버전이 `OFFICIAL_1.7.0-92_deb`로 기록되어 있습니다. 이는 에이전트가 해당 버전으로 정상적으로 설치되어 있음을 의미합니다.
    
2. **폴링 메시지**: `[Aws::CodeDeployCommand::Client 200 45.142183 0 retries] poll_host_command(...)` 메시지는 CodeDeploy 에이전트가 CodeDeploy 서비스에 주기적으로 "폴링(polling)"하여 새로운 배포 명령이 있는지 확인하는 과정을 나타냅니다. 이 과정은 에이전트가 AWS CodeDeploy 서버와 정상적으로 통신하고 있음을 의미합니다.
```

다음 확인해보기

### 배포 트리거 문제

- AWS CodeDeploy 콘솔에서 해당 배포 그룹과 연관된 배포가 트리거되었는지 확인합니다. 배포가 예정되었거나 진행 중이지만 에이전트 로그에 반영되지 않는다면, 연결이나 권한 문제가 있을 수 있습니다.

### 인스턴스 권한 설정

- 배포 대상 인스턴스에 부여된 IAM 역할이 CodeDeploy 서비스와의 통신을 위한 적절한 권한을 가지고 있는지 확인합니다. CodeDeployAgentPolicy와 같은 필요한 권한이 IAM 역할에 포함되어 있어야 합니다.
> 권한이 제대로 설정되어있지 않았음. 풀액세스 권한 부여함

### 방화벽 및 네트워크 설정

- 인스턴스의 네트워크 설정이나 방화벽 규칙이 CodeDeploy 서버와의 통신을 방해하고 있지 않은지 확인합니다. 특히, 인터넷 연결이 필요한 환경에서 인스턴스가 외부 네트워크와 통신할 수 있는지 검토해야 합니다.
---
BeforInstall 에서 진행이 안되는 것을 확인
appspec.yml 파일을 못찾아서 발생하는 문제
