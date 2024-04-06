---
tags:
  - Recursion
  - Algorithm
---

1. 종료 조건을 가장 앞에 적는다.
2. 반복할 내용을 적는다.

```ts
function countWays(n: number): number {
  if (n === 0) {
    // 맨 위에 도착했으니, 방법을 하나 찾았다고 칩니다.
    return 1;
  } else if (n < 0) {
    // 계단을 너무 많이 올라서 범위를 벗어났으니, 이건 유효한 방법이 아닙니다.
    return 0;
  }

  // 1계단 올라가는 방법과 2계단 올라가는 방법을 모두 탐색합니다.
  return countWays(n - 1) + countWays(n - 2);
}

const totalSteps = 3;
console.log(`총 ${totalSteps}계단을 오르는 방법은 ${countWays(totalSteps)}가지입니다.`);

```