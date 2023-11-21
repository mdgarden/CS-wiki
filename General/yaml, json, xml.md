---
tags:
  - JSON
  - 터미널
  - General
aliases:
---


#터미널 #JSON
터미널에서 그냥 curl명령어로 실행하면 위와 같이 JSON 결과가 읽기 편하게 출력되지는 않습니다. 출력을 예쁘게 보려면 예를 들어 다음과 같이 jq에 파이프로 전달하면 됩니다.

```
$ curl -X GET http://localhost:3000/users/0 | jq
```

자세한 정보는 홈페이지를 참고하세요
https://stedolan.github.io/jq
