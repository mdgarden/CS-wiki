https://leetcode.com/problems/minimum-number-of-operations-to-make-array-xor-equal-to-k/

- XOR 연산은 순서와 상관없다.
- XOR 연산은 두 비트가 다를 경우 1을 반환하고 같을 경우 0을 반환하는 특성
- XOR 연산은 두 비트가 서로 다를 때 `1`을, 같을 때 `0`을 반환함. 예를 들어:

- `0 XOR 0 = 0`
- `1 XOR 1 = 0`
- `0 XOR 1 = 1`
- `1 XOR 0 = 1`

- 주어진 nums 끼리의 XOR 연산결과가 k가 되어야 한다.
	- 예) 2 XOR 1 XOR 3 XOR 4 의 값이 1이 되어야 한다.
- 모든 숫자를 2진수로 전환했을 때, 각 자릿수의 비트값이 홀수면 결과는 1이다.
	- 예) 

| bit - 1 | bit - 2 | bit - 3 | XOR |
| ------- | ------- | ------- | --- |
| 0       | 0       | 0       | 0   |
| 0       | 0       | 1       | 1   |
| 0       | 1       | 0       | 1   |
- 각 num을 k와 XOR 하면 비트가 몇개나 다른지 알 수 있다.