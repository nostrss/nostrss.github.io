---
layout: post
title: '[js기초] Strict equality'
author: 'Nostrss'
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---



## 1. ==(동등 비교 연산자 : 느슨한 비교)
[MDN 공식문서 보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Equality)
동등 비교 연산자(==)는 두 개의 피연산자가 동일한지 확인하며,
Boolean을 반환한다.

```javascript
console.log('1' ==  1);
// expected output: true
```

## 2. ===(일치 비교 연산자 : 엄격한 비교)

[MDN 공식문서 보기](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)

일치 비교 연산자(===)는 두 개의 피연산자가 동일한지 확인하며,
Boolean을 반환한다.
```javascript
console.log('1' ===  1);
// expected output: false
```

동등 비교 연산자와 일치 비교 연산자는 좌항과 우항의 피연산자가 같은 값으로
평가되는지 비교해 불리언 값을 반환한다.

하지만 비교하는 엄격성의 정도가 다르다.
동등 비교 연산자는 느슨한 비교를 하지만 일치 비교는 연산자는 엄격한 비교를 한다.


따라서 동등 비교 연산자는 사용하지 않는 편이 좋다.

엄격한 비교를 하는 `===`를 애용하자!