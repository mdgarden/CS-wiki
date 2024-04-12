---
tags:
  - AWS
  - CodeDeploy
  - Deployment
  - CI/CD
aliases:
  - AWS CodeDeploy
---

Q. `CodePipeline`을 통해 빌드와 배포를 진행할 때, `CodeDeploy`는 어디서 아티팩트를 찾아오는가?
- AWS CodePipeline을 사용할 때, 파이프라인의 각 단계(stage)는 서로 연결되어 있으며, 빌드 단계(CodeBuild)에서 생성된 아티팩트는 자동으로 다음 단계(예: 배포 단계, CodeDeploy)로 전달됩니다. 즉, CodeBuild에서 생성된 JAR 파일과 같은 아티팩트는 파이프라인을 통해 자동으로 관리되며, 별도로 CodeDeploy에서 이를 "찾아오도록" 설정할 필요가 없습니다. 파이프라인 설정 과정에서 아티팩트의 소스와 대상을 명확히 정의하기 때문입니다. 

![[AWS/Developer Tools/CodePipeline/README#아티팩트 전달 메커니즘|AWS CodePipeline]]
