---
layout: post
title: '알아두면 좋은 Object 메소드'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---


## Object.keys()
[Object.keys() 공식문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

### 객체의 키를 전부 알려줄께
- 주어진 객체의 속성 `이름(key)`들을 일반적인 반복문과 동일한 순서로 순회되는 열거할 수 있는 `배열`로 반환한다.

예제
```javascript
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]
```

## Object.values()
[Object.values() 공식문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/values)

### 이번에는 객체의 값을 전부 알려줄께
- 주어진 객체의 `속성의 값`들을 일반적인 반복문과 동일한 순서로 순회되는 열거할 수 있는 `배열`로 반환한다.

예제
```javascript
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.values(object1));
// expected output: Array ["somestring", 42, false]
```

## Object.entries()
[Object.entries() 공식문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

### 그럼 나는 객체의 키와 값을 전부 알려줄께
- 주어진 객체의 속성의 `키`와 `값`들을 일반적인 반복문과 동일한 순서로 순회되는 열거할 수 있는 `배열`로 반환한다.

```javascript
const object1 = {
  a: 'somestring',
  b: 42
};

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"
```

## Object.assign()
[Object.assign()공식문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

### 객체의 키와 값을 전부 덮어 써줄께
- 목표 객체의 속성 중 출처 객체와 `동일한 키`를 갖는 속성의 경우, 그 속성 값은 출처 객체의 속성 값으로 덮어씁니다. 출처 객체들의 속성 중에서도 키가 겹칠 경우 `뒤쪽 객체의 속성 값`이 `앞쪽 객체의 속성 값`보다 우선합니다.

구문
>Object.assign(target, ...sources)


```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(source);
// expected output: Object { b: 4, c: 5 }

```