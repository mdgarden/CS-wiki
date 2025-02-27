---
tags:
  - AWS
  - CodeCommit
  - CodeArtifact
  - CodeBuild
  - CodeDeploy
  - CodePipeline
  - Deployment
  - Build
  - CI/CD
aliases:
  - AWS 개발자 도구 개요
---
> [!abstract] Tldr
> - **CodeCommit**: 소스 코드 저장 및 버전 관리.
> - **CodeArtifact**: 패키지 저장 및 공유.
> - **CodeBuild**: 빌드 및 테스트 자동화.
> - **CodeDeploy**: 애플리케이션 자동 배포.

참고 : [[Build, Deployment]]

AWS에서 제공하는 Code 시리즈 서비스들은 개발 및 배포 프로세스를 자동화하고, 효율적인 소프트웨어 개발 워크플로우를 지원하기 위해 디자인되었습니다. 각각의 서비스는 CI/CD 파이프라인의 다른 단계에 초점을 맞추고 있으며, 서로 다른 역할을 수행합니다. 여기서는 AWS CodeCommit, AWS CodeArtifact, AWS CodeBuild, AWS CodeDeploy의 차이점과 역할에 대해 설명하겠습니다.

### AWS CodeCommit

- **역할**: 소스 코드 버전 관리 서비스입니다.
- **차이점과 기능**: CodeCommit은 Git 기반의 소스 컨트롤 서비스로, 안전하게 소스 코드를 저장하고 관리할 수 있게 해줍니다. 프라이빗 Git 리포지토리를 호스팅하며, 개발 팀이 코드 변경을 추적하고 협업할 수 있는 환경을 제공합니다. CodeCommit은 높은 확장성과 보안성을 가지며, 다른 AWS 서비스와 쉽게 통합됩니다.



### AWS CodeArtifact

- **역할**: 소프트웨어 패키지 관리 서비스입니다.
- **차이점과 기능**: CodeArtifact를 사용하면 소프트웨어 개발 중에 필요한 다양한 외부 라이브러리와 패키지를 안전하게 저장하고 공유할 수 있습니다. Maven, Gradle, npm, pip 등 다양한 패키지 관리 도구와 호환되며, 라이브러리의 중앙 집중식 저장소 역할을 합니다. 이를 통해 개발 팀은 의존성 관리를 보다 쉽게 할 수 있고, 보안성 높은 방식으로 패키지를 관리할 수 있습니다.

> [!note]
> AWS Artifact와는 다른 서비스이다.
### [[AWS/Developer Tools/CodeBuild/Q&A|AWS CodeBuild]]

- **역할**: 지속적 통합 서비스입니다.
- **차이점과 기능**: CodeBuild는 소스 코드 컴파일, 테스트 실행, 배포 가능한 소프트웨어 패키지 생성 등의 빌드 작업을 자동화합니다. 서버를 관리할 필요 없이 빌드 프로세스를 구성하고 실행할 수 있으며, GitHub, Bitbucket, CodeCommit 등 여러 소스 공급자와 통합됩니다. CodeBuild는 자동 빌드, 테스트 및 패키지 생성을 통해 빠른 피드백과 배포 준비 과정을 지원합니다.

### [[AWS/Developer Tools/CodeDeploy/Q&A|AWS CodeDeploy]]

- **역할**: 자동화된 애플리케이션 배포 서비스입니다.
- **차이점과 기능**: CodeDeploy는 개발 및 프로덕션 환경에 애플리케이션을 자동으로 배포하는 기능을 제공합니다. EC2 인스턴스, 온프레미스 서버, Lambda 함수, Amazon ECS 서비스 등 다양한 대상에 배포를 지원합니다. CodeDeploy는 배포 과정을 자동화하고, 롤백, 배포 상태 추적 등의 기능을 통해 높은 가용성과 안정성을 보장합니다.


이 서비스들은 AWS의 포괄적인 DevOps 도구 세트를 구성하며, 개발부터 배포까지의 전체 소프트웨어 라이프사이클을 지원합니다. 각각은 독립적인 기능을 가지고 있지만, 함께 사용될 때 최대의 효과를 발휘할 수 있습니다.