---
tags:
  - Troubleshooting
  - AWS
  - CodeBuild
  - CodeDeploy
---

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

### 방화벽 및 네트워크 설정

- 인스턴스의 네트워크 설정이나 방화벽 규칙이 CodeDeploy 서버와의 통신을 방해하고 있지 않은지 확인합니다. 특히, 인터넷 연결이 필요한 환경에서 인스턴스가 외부 네트워크와 통신할 수 있는지 검토해야 합니다.
---
## lifecycle 이벤트를 수신할 수 없음
- 에이전트 관련 문제 확인
## BeforInstall 에서 실패함
### 1. AppSpec 파일의 이름 및 위치 확인

- AppSpec 파일의 이름이 `appspec.yml` 또는 `appspec.yaml`이 맞는지 확인하세요.
- AppSpec 파일이 프로젝트의 루트 디렉토리에 위치해 있는지 확인하세요. [[discard-paths|CodeDeploy는 이 파일을 루트 디렉토리에서 찾기를 기대합니다.]]
### 2. 빌드 아티팩트 확인

- CodePipeline의 빌드 단계에서 생성된 아티팩트에 AppSpec 파일이 포함되어 있는지 확인하세요. 이를 위해 빌드 후 생성된 아티팩트를 직접 다운로드하여 내용을 확인할 수 있습니다.
- 빌드 스크립트 또는 빌드 설정에서 AppSpec 파일이 아티팩트에 포함되도록 명시적으로 지정되어 있는지 확인하세요.

> [이 이슈의 원인](https://github.com/mdgarden/fastcampus-sns/issues/2)이 이것이었음. appspec파일이 아티팩트에 포함되도록 buildspec.yml 파일에서 정의해야함.
### 3. [에이전트 관련 문제 확인](#CodeDeploy 에이전트 관련 문제 해결법)


## CodeDeploy 에이전트 관련 문제 해결법
### 1. CodeDeploy 에이전트 상태 확인
먼저, 대상 EC2 인스턴스에서 CodeDeploy 에이전트가 실행 중인지 확인해야 합니다.
- Linux 기반 시스템의 경우:
  ```bash
  sudo service codedeploy-agent status
  ```
- Windows 기반 시스템의 경우:
  ```powershell
  Get-Service -Name codedeploy-agent
  ```

### 2. CodeDeploy 에이전트 재시작
에이전트가 실행 중이지 않다면, 에이전트를 시작하거나 재시작해야 합니다.
- Linux:
  ```bash
  sudo service codedeploy-agent start
  ```
- Windows:
  ```powershell
  Start-Service -Name codedeploy-agent
  ```

### 3. CodeDeploy 에이전트 로그 확인
에이전트의 상세한 동작 내역은 로그 파일을 통해 확인할 수 있습니다. 로그 파일에서 구체적인 에러 메시지를 찾아보세요.
- Linux 기반 시스템의 경우, 로그 파일은 주로 `/var/log/aws/codedeploy-agent/codedeploy-agent.log` 위치에 있습니다.
- Windows 기반 시스템의 경우, 로그 파일은 주로 `C:\ProgramData\Amazon\CodeDeploy\log\codedeploy-agent.log` 위치에 있습니다.

### 4. 인터넷 연결 및 방화벽 설정 확인
CodeDeploy 에이전트가 AWS CodeDeploy 서버와 통신하기 위해서는 인터넷 연결이 활성화되어 있어야 합니다. 또한, 방화벽 설정이나 보안 그룹, 네트워크 ACL(Access Control List) 등이 에이전트의 연결을 차단하고 있지 않은지 확인해야 합니다.

### 5. IAM 역할과 권한 확인
대상 EC2 인스턴스에 부여된 IAM 역할이 CodeDeploy와의 통신에 필요한 적절한 권한을 가지고 있는지 확인하세요. CodeDeploy 에이전트가 AWS 서비스와 통신하기 위해 필요한 권한을 포함하는 IAM 정책이 역할에 연결되어 있어야 합니다.

### 6. CodeDeploy 에이전트 최신 버전 사용
문제가 지속되면, CodeDeploy 에이전트가 최신 버전인지 확인하고, 필요한 경우 업데이트를 수행하세요. AWS 공식 문서에서는 에이전트의 최신 버전 설치 방법을 제공합니다.

이러한 단계를 통해 대부분의 CodeDeploy 에이전트 관련 문제를 해결할 수 있습니다. 만약 이러한 절차를 따라도 문제가 해결되지 않는다면, 추가적인 지원을 위해 AWS 지원 팀에 문의할 수 있습니다.


## `nohup`을 사용하여 `start.sh`스크립트를 실행했을 때, 서버가 정상적으로 실행되었으나 배포에 실패함

참고 : ![[EC2의 세션#^c2e915]]

일반적으로 터미널에서 직접 명령어를 실행하면, 해당 명령어의 실행이 완료된 후 쉘은 명령어의 종료 코드(exit code)를 반환합니다. 이 종료 코드를 통해 명령어의 실행 성공 여부를 바로 알 수 있습니다. 종료 코드가 0이면 성공을, 0이 아니면 오류를 의미합니다.

반면, `nohup` 명령어로 프로세스를 백그라운드에서 실행시키게 되면, 프로세스가 바로 백그라운드로 이동하고 쉘은 즉시 제어권을 사용자에게 반환합니다. 이 경우, `nohup`으로 시작된 프로세스의 종료 코드를 직접 확인하는 것은 쉽지 않습니다. 왜냐하면 `nohup`으로 실행된 프로세스는 독립적으로 실행되기 때문에, 그 종료 시점을 알 수 없으며, 바로 종료 코드를 얻을 수 없기 때문입니다.

따라서, `nohup`을 사용해 백그라운드에서 애플리케이션을 실행하는 경우, 애플리케이션이 정상적으로 실행되었는지 확인하기 위해서는 별도의 방법이 필요합니다. 예를 들어:

- 애플리케이션 로그 파일을 주기적으로 확인하여 특정 로그 메시지(예: "Application started" 또는 유사한 메시지)가 출력되었는지 검사하는 방법
- 애플리케이션이 제공하는 헬스 체크 API에 요청을 보내어 응답을 확인하는 방법

### 예시: `appspec.yml` 내에서 헬스 체크 스크립트 실행


```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /opt/app
hooks:
  ApplicationStart:
    - location: scripts/check_health.sh
      timeout: 300
      runas: appuser
  ValidateService:
    - location: scripts/validate_service.sh
      timeout: 300
      runas: appuser
```


여기서 `check_health.sh` 스크립트는 애플리케이션의 헬스 체크 엔드포인트를 호출하고, 응답을 기반으로 서버가 정상적으로 실행되었는지 확인합니다. 스크립트가 0을 반환하면 성공으로 간주하고, 그렇지 않으면 실패로 판단합니다.

### 결론

AWS CodeDeploy 자체는 서버의 실행 상태를 직접 확인하지 않습니다. 대신, 배포 과정에서 사용자가 제공한 검증 스크립트의 실행 결과를 통해 서버의 상태를 간접적으로 파악할 수 있습니다. 따라서, 애플리케이션의 상태를 정확히 모니터링하고 관리하려면, 상태 확인 로직을 포함한 스크립트를 적절히 구현하고 `appspec.yml`에 정의해야 합니다.