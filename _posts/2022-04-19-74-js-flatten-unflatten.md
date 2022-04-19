---
layout: post
title: "[JS]깊이가 있는 배열과 객체 "
author: "Nostrss"
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

## flatten
일반적으로 알고 있는 객체와 배열의 모습은 아래와 같다.

```javascript
[itme1, item2, item3]

{
  key1 : value1,
  key2 : value2,
  key3 : value3,
  key4 : value4,
}
```
위와 같은 배열과 객체의 구조를 가진 경우 flat 또는 flatten 배열 또는 객체라고 부른다.

## unflatten

```javascript
[[itme1,item2], [item3,item4]]

{
  key1 : {
    depth1 : dapth1value,
    depth2 : dapth2value,
    depth3 : dapth3value,
  },
  key2 : value2,
  key3 : value3,
  key4 : value4,
}
```

그리고 위와 같이 중첩된 구조의 배열, 객체를 unflatten 또는 nested 배열 또는 객체라고 부른다.

### unflatten 배열을 flat하게 바꾸는 메소드

[MDN Array.prototype.flat() 문서보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

>flat() 메서드는 모든 하위 배열 요소를 지정한 깊이까지 재귀적으로 이어붙인 새로운 배열을 생성합니다.

#### 예시
```javascript
const arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]

const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

그리고 flat 메소드는 아래처럼 배열의 구멍을 제거하기 위해 사용되기도 한다.

```javascript
const arr5 = [1, 2, , 4, 5];
arr5.flat();
// [1, 2, 4, 5]
```





