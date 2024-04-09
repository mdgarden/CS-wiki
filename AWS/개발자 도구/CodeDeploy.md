---
tags:
  - AWS
  - CodeDeploy
  - Deployment
  - CI/CD
---
현재 상황
파이프라인에서 빌드까지 정상적으로 되었으나, 디플로이에서 실패함.
로그를 확인해본 결과 AWS CodeDeploy 에이전트는 정상적으로 작동하고 있는 것으로 확인됨.

```
1. **에이전트 버전**: 로그에는 CodeDeploy 에이전트의 버전이 `OFFICIAL_1.7.0-92_deb`로 기록되어 있습니다. 이는 에이전트가 해당 버전으로 정상적으로 설치되어 있음을 의미합니다.
    
2. **폴링 메시지**: `[Aws::CodeDeployCommand::Client 200 45.142183 0 retries] poll_host_command(...)` 메시지는 CodeDeploy 에이전트가 CodeDeploy 서비스에 주기적으로 "폴링(polling)"하여 새로운 배포 명령이 있는지 확인하는 과정을 나타냅니다. 이 과정은 에이전트가 AWS CodeDeploy 서버와 정상적으로 통신하고 있음을 의미합니다.
```

다음 확인해보기