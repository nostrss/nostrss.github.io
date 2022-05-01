---
layout: post
title: "[js] 줄서서 Promise를 할 필욘 없자나? Promise all "
author: "Nostrss"
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

## Promise.all
[MDN Promise All 문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

만약 여러개의 프라미스를 동시에 실행시킨다고 가정을 해보자.

>1번 Promise 실행 -> 완료 10초

>1번 종료 후 2번 Promise 실행 -> 완료 10초

>2번 종료 후 3번 promise 실행 -> 완료 10초

위의 경우 처럼 3개의 promise를 순서대로 실행할 경우 총 30초의 시간이 소요된다.

그렇다면 이런 방법은 어떨까?

> 1번 Promise 실행, 2번 Promise 실행, 3번 Promise 실행

> 1번 Promise 완료 10초, 2번 Promise 실행 완료 10초, 1번 Promise 완료 10초

동시에 3개의 Promise를 실행시키게 되면 총 10초의 시간이 소요된다.
이렇게 복수의 URL에 동시에 요청을 보내고, 다운로드가 모두 완료된 후에 콘텐츠를 처리할 때 이런 상황이 발생하는데
이럴 때 Promise.all을 사용할 수 있다.

### 예시

사용문법
```javascript
let promise = Promise.all([...promises...]);
```

`Promise.all`은 요소 전체가 프라미스인 배열(엄밀히 따지면 이터러블 객체이지만, 대개는 배열임)을 받고 새로운 프라미스를 반환합니다.
배열 안 프라미스가 모두 처리되면 새로운 프라미스가 이행되는데, 배열 안 프라미스의 결과값을 담은 배열이 새로운 프라미스의 result가 됩니다.

예시
```javascript
Promise.all([
  new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
  new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
  new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
]).then(alert); // 프라미스 전체가 처리되면 1, 2, 3이 반환됩니다. 각 프라미스는 배열을 구성하는 요소가 됩니다.
```

위의 Promise.all은 3초 후에 처리되고, 반환되는 프라미스의 result는 배열 [1, 2, 3]이 됩니다.
배열 result의 `요소 순서`에 주목할 필요가 있다. 
Promise.all의 첫 번째 프라미스는 가장 늦게 이행되더라도 처리 결과는 배열의 첫 번째 요소에 저장됩니다.

### 주의사항
- Promise.all에 전달되는 프라미스 중 `하나`라도 거부되면, Promise.all이 반환하는 프라미스는 `에러`와 함께 바로 거부된다.

```javascript
Promise.all([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
]).catch(alert); // Error: 에러 발생!
```
2초 후 두 번째 프라미스가 거부되면서 Promise.all `전체`가 거부되고, .catch가 실행되고 거부 에러는 Promise.all 전체의 결과가 된다.
즉 `하나의 프라미스라도 거부`가 되면 정상적으로 처리된 다르 프라미스들도 무시가 되어 버린다.


