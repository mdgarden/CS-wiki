---
tags:
  - AWS
  - CodeBuild
  - buildspec
---

`discard-paths: no` 설정은 AWS CodeBuild의 `buildspec.yml` 파일 내에서 아티팩트를 정의할 때 사용됩니다. 이 설정은 빌드 결과물(아티팩트)을 생성할 때 파일 경로를 어떻게 처리할지를 결정합니다.

### `discard-paths: no` 설정의 의미

- `discard-paths: no`를 설정하면, 아티팩트에 포함되는 파일들의 상대적인 파일 경로가 유지됩니다. 즉, 소스 코드의 디렉토리 구조가 그대로 아티팩트에 반영됩니다.
- 이는 특히 여러 디렉토리에 걸쳐 있는 파일들을 아티팩트로 패키징할 때 중요하며, 배포 시 예상한 파일 구조를 유지하고자 할 때 필요합니다.

### `discard-paths` 설정을 하지 않았을 때의 기본 동작

- `discard-paths` 옵션을 명시적으로 설정하지 않으면, 기본값은 `yes`로 설정됩니다.
- `discard-paths: yes`로 설정되어 있으면, 아티팩트를 생성할 때 파일들의 경로 정보가 제거되고, 모든 파일이 아티팩트의 루트 디렉토리에 위치하게 됩니다.
- 이는 파일들 사이의 원래 디렉토리 구조를 무시하고, 모든 파일을 평탄하게(flatten) 처리하므로, 다수의 서브 디렉토리를 가진 프로젝트의 경우 파일 구조가 단순화되어 배포 과정에서 문제가 발생할 수 있습니다.

### 예시

예를 들어, 소스 코드 내에 `src`와 `config` 두 개의 디렉토리가 있고 각각의 디렉토리에 파일들이 포함되어 있는 경우,

- `discard-paths: no` 설정 시, 아티팩트 내에서도 `src`와 `config` 디렉토리 구조가 유지되며 파일들이 각각 해당 디렉토리 안에 위치하게 됩니다.
- `discard-paths: yes` 설정 시, 모든 파일이 아티팩트의 루트에 위치하게 되어 원래의 디렉토리 구조가 사라집니다.

따라서, 배포 과정에서 디렉토리 구조가 중요하다면 `discard-paths: no`를 설정하여 파일 경로를 유지하는 것이 좋습니다.

`discard-paths` 항목을 `buildspec.yml`에서 명시적으로 설정하지 않았을 경우, AWS CodeBuild의 기본 동작은 `discard-paths: yes`입니다. 이는 아티팩트를 생성할 때 파일의 원본 경로를 무시하고, 모든 파일을 아티팩트의 루트 디렉토리에 평탄하게(flatten) 배치한다는 것을 의미합니다. 따라서, 디렉토리 구조를 유지하고 싶지 않는 경우에는 이 항목을 설정할 필요가 없습니다. 하지만, 파일의 디렉토리 구조를 유지하고 싶은 경우에는 `discard-paths: no`를 명시적으로 설정해야 합니다.

`discard-paths` 설정의 영향을 보여주는 구체적인 예시를 들어보겠습니다.

### 프로젝트 구조 예시:

프로젝트의 소스 코드 구조가 다음과 같다고 가정해 보겠습니다.

```
/my-app
│
├── src
│   ├── index.js
│   └── lib.js
│
└── assets
    ├── logo.png
    └── style.css
```

여기서, `index.js`, `lib.js`, `logo.png`, `style.css` 파일들을 빌드 아티팩트로 패키징하려고 합니다.

### `buildspec.yml` 설정:

#### 1. `discard-paths: yes` (기본값 또는 명시적 설정)

```yaml
version: 0.2

phases:
  build:
    commands:
      - echo "Building..."
artifacts:
  files:
    - src/*
    - assets/*
  discard-paths: yes
```

이 설정으로 빌드한 아티팩트의 구조는 다음과 같이 됩니다.

```
/build-output
│
├── index.js
├── lib.js
├── logo.png
└── style.css
```

- `src`와 `assets` 디렉토리의 구조가 사라지고, 모든 파일이 아티팩트의 루트 디렉토리에 직접 위치합니다.
- 원본 경로 정보가 무시되어 파일 구조가 평탄화됩니다.

#### 2. `discard-paths: no`

```yaml
version: 0.2

phases:
  build:
    commands:
      - echo "Building..."
artifacts:
  files:
    - src/*
    - assets/*
  discard-paths: no
```

이 설정으로 빌드한 아티팩트의 구조는 다음과 같이 됩니다.

```
/build-output
│
├── src
│   ├── index.js
│   └── lib.js
│
└── assets
    ├── logo.png
    └── style.css
```

- `src`와 `assets` 디렉토리 구조가 유지됩니다. 파일들은 원본 경로에 따라 해당 디렉토리 안에 위치하게 됩니다.
- 파일의 원본 디렉토리 구조를 유지하므로, 복잡한 프로젝트에서 파일 구조의 명확성을 유지할 수 있습니다.

이 예시를 통해 `discard-paths` 설정이 아티팩트의 파일 구조에 어떠한 영향을 미치는지 명확하게 이해할 수 있습니다. 따라서, 배포 과정에서 원하는 파일 구조를 유지하기 위해 적절한 설정을 선택해야 합니다.