## 아티팩트 저장 위치 설정하기

### AWS Management Console을 통한 설정

1. **AWS Management Console에 로그인**한 후, **CodeBuild 서비스로 이동**합니다.
2. **빌드 프로젝트 목록에서 원하는 프로젝트를 선택**합니다.
3. **프로젝트 세부 정보 페이지에서 "편집" 또는 "빌드 설정"을 클릭**합니다.
4. **"아티팩트" 섹션을 찾아** 설정을 조정합니다. 여기서 "아티팩트 유형"을 "Amazon S3"로 설정하고, 원하는 S3 버킷의 이름과 아티팩트가 저장될 경로를 지정합니다.
5. **변경 사항을 저장**합니다.
### `buildspec.yml` 파일을 통한 설정

`buildspec.yml` 파일 내에서 아티팩트 저장 위치를 지정하려면, `artifacts` 섹션에 해당 정보를 포함시켜야 합니다. 예를 들어:

```yaml
version: 0.2

phases:
  pre_build:
    commands:
      - echo Installing source dependencies...
  build:
    commands:
      - echo Build started on `date`
      - ./gradlew build
  post_build:
    commands:
      - echo Build completed on `date`

artifacts:
  files:
    - build/libs/*.jar
  discard-paths: yes
  name: my-application-$(date +%Y-%m-%d)
  type: s3
  bucket: my-s3-bucket-name
  path: my-application/builds

```

위의 예시에서 `type`은 아티팩트 저장 유형을 의미하며, `s3`로 설정되어 있습니다. `bucket`은 아티팩트를 저장할 S3 버킷의 이름이며, `path`는 해당 버킷 내에서 아티팩트가 저장될 경로를 지정합니다.