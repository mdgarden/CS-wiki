---
tags:
  - AWS
  - EC2
  - CodeBuild
  - CI/CD
---

프로젝트에서 Gradle과 함께 Node.js를 사용한다면 (예를 들어, `node-gradle` 플러그인을 사용하여 프론트엔드 빌드 작업을 수행하는 경우), EC2 인스턴스에도 Node.js를 별도로 설치해야 할 수 있습니다. 이는 프로젝트 빌드 또는 실행 시 Node.js 환경이 필요하기 때문입니다.

### Node.js 설치 방법

EC2 인스턴스(여기서는 Ubuntu를 기준으로)에 Node.js를 설치하는 방법은 다음과 같습니다:

1. **NodeSource 노드.js 바이너리 배포의 PPA(Personal Package Archive)를 추가합니다.** 이를 통해 최신 버전의 Node.js를 설치할 수 있습니다. 예를 들어, Node.js 14.x 버전을 설치하려면 다음 명령을 사용합니다:

   ```bash
   curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
   ```

2. **Node.js를 설치합니다.** PPA를 시스템에 추가한 후, 다음 명령으로 Node.js를 설치할 수 있습니다:

   ```bash
   sudo apt-get install -y nodejs
   ```

3. **설치 확인:** 설치가 성공적으로 완료되었는지 확인하기 위해, 다음 명령으로 Node.js와 npm의 버전을 확인할 수 있습니다:

   ```bash
   node -v
   npm -v
   ```

### 추가 고려 사항

- **node-gradle 사용**: 프로젝트에서 `node-gradle` 플러그인을 사용한다면, Gradle 빌드 스크립트 내에서 Node.js와 npm (또는 yarn) 관련 작업을 정의할 수 있습니다. 이 경우, 빌드 프로세스 중에 Node.js 환경이 필요하기 때문에, EC2 인스턴스에 Node.js를 설치해야 합니다.

- **CI/CD 파이프라인**: 프로젝트를 AWS CodeBuild, Jenkins 등 CI/CD 도구를 사용하여 EC2 인스턴스로 배포하는 경우, 해당 도구의 빌드 환경에서도 Node.js가 필요할 수 있습니다. 이 경우, 빌드 스펙 또는 Docker 이미지에 Node.js 설치 단계를 포함시킬 수 있습니다.

- **버전 관리**: 특정 Node.js 버전에 의존하는 프로젝트의 경우, `n` 또는 `nvm` 같은 Node.js 버전 관리 도구를 사용하는 것이 좋습니다. 이를 통해 프로젝트에 필요한 정확한 Node.js 버전을 관리하고 사용할 수 있습니다.

EC2 인스턴스에 Node.js를 설치함으로써, Node.js를 필요로 하는 다양한 빌드 스크립트와 애플리케이션을 실행할 수 있게 됩니다.