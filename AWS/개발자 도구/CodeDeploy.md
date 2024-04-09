---
tags:
  - AWS
  - CodeDeploy
  - Deployment
  - CI/CD
---
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

### 방화벽 및 네트워크 설정

- 인스턴스의 네트워크 설정이나 방화벽 규칙이 CodeDeploy 서버와의 통신을 방해하고 있지 않은지 확인합니다. 특히, 인터넷 연결이 필요한 환경에서 인스턴스가 외부 네트워크와 통신할 수 있는지 검토해야 합니다.