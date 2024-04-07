---
tags:
  - Algorithm
Topics:
  - String
  - Dynamic Programming
  - Stack
  - Greedy
StartDate: 2024-04-04
EndDate: 2024-04-07
---

## 괄호 문제
대체로 괄호가 유효한지 ( ()형태로 닫히는지)에 대한 문제
기본적으로 정석 풀이는 스택이나 반드시 짝이 있다는 괄호의 특징상 단순히 +-로 계산해도 풀리는 경우가 많음

## 유효하지 않은 케이스
### 어느 한 쪽의 괄호가 더 많을 때
짝을 맞추어야 하므로, 각각의 갯수가 일치하지 않으면 유효하지 않은 괄호가 뜻이다.
#### 여는 괄호보다 닫는 괄호가 더 많을 때
배열 혹은 문자열을 순회하면서, 여는 괄호가 더 많아져도 후에 닫는 괄호가 얼마나 더 많이 있을지 모르기 때문에 여는 괄호의 숫자는 상관이 없다. 그러나 닫는 괄호가 여는 괄호보다 많아지면, 확실하게 유효하지 않은 괄호가 된다.

> [!example]
> // 세번째 괄호부터 유효하지 않다.
> "()))(("

## 출제 문제

[1614. Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)
[1544. Make The String Great](https://leetcode.com/problems/make-the-string-great/)
[1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)
[678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)