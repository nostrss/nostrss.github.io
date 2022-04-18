---
layout: post
title: "[JS]나를 부르는 함수 재귀함수"
author: "Nostrss"
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

## 재귀함수(Recursive function)

[MDN 문서 바로가기](https://developer.mozilla.org/en-US/docs/Glossary/Recursion#recursive_function_calls_itself_until_condition_met)

- 자신을 호출하는 함수의 행위를 재귀함수라 한다. 재귀함수는 더 작은 하위 문제를 포함하는 문제를 해결하는 데 사용된다. 

- 재귀 함수는 기본 케이스(재귀 종료) 또는 재귀 케이스(재귀 재개)의 두 가지 입력을 수신할 수 있다.

### 예시1 팩토리얼

아래는 팩토리얼을 재귀함수로 구하는 예시이다.

```javascript
const factorial = (n) => {
  if (n === 0) return 1;
  else {
      console.log(`${n} * factorial(${n-1})`)
      return n * factorial(n - 1);
  }
};

```
위의 식을 콘솔에 찍어보면 아래와 같이 결과가 나오게 된다.

```javascript
factorial(10)
10 * factorial(9)
9 * factorial(8)
8 * factorial(7)
7 * factorial(6)
6 * factorial(5)
5 * factorial(4)
4 * factorial(3)
3 * factorial(2)
2 * factorial(1)
1 * factorial(0)
3628800
```
n으로 10을 입력 받았을 때 재귀가 종료가 되는 시점은 n이 0이 되는 시점이고
0이 될때까지 계속 해서 자기 자신을 호출하는 것을 볼 수 있다.

조금 더 풀어 써보면 아해와 같이 스택에 쌓여 있다고 보면 이해가 빠를 듯하다.

```
stp=9   n=1  일때 : 1 * factorial(0)
stp=8   n=2  일때 : 2 * factorial(1)
stp=7   n=3  일때 : 3 * factorial(2)
stp=6   n=4  일때 : 4 * factorial(3)
stp=5   n=5  일때 : 5 * factorial(4)
stp=4   n=6  일때 : 6 * factorial(5)
stp=3   n=7  일때 : 7 * factorial(6)
stp=2   n=8  일때 : 8 * factorial(7)
stp=1   n=9  일때 : 9 * factorial(8)
stp=0   n=10 일때 : 10 * factorial(9)
```
stp가 작은 스택이 먼저 쌓인 스택이고 n이 0이 되는 순간에 제일 위에 있는 스택(stp=9)부터 꺼내어 연산을 실행한다.

### 예시2 피보나치 수열

피보나치 수열도 재귀함수로 간단하게 답을 구할 수 있다.

```javascript
const fibonacci = (n) => (
  n <= 2 ? 1 : fibonacci(n - 1) + fibonacci(n - 2));
console.log(fibonacci(10));
```
다만 개인적으로 재귀함수로 피보나치 수열을 구한 적이 있었는데, 피보나치수 50 정도만 구하려고 해도 상당한 시간이 소요되었던걸로 기억한다.

재귀함수가 속도면에서는 그렇게 효율적이지 않은 것 같다.



