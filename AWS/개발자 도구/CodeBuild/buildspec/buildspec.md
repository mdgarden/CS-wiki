
- 프로젝트의 루트 디렉토리에 위치해야함
- appspec파일을 포함시키려면 아티팩트 항목에 appspec 파일을 명시해야함
```yaml
version: 0.2

phases:
  install:
    commands:
      # 필요한 의존성 설치 명령
  pre_build:
    commands:
      # 테스트 실행 등 사전 빌드 단계 명령
  build:
    commands:
      # 빌드 명령 (예: 컴파일)
artifacts:
  files:
    - appspec.yml
    - 기타 포함할 파일 또는 디렉토리
  discard-paths: no

```
