---
layout: post
title: " 객체가 어떻게 변할수 있니? 불변 & 가변 "
author: "Nostrss"
comments: true
tags: javascript 
excerpt_separator:
sticky:
hidden:
---

## Immutable 이란?
- 내용이 변하지 않는 것을 말한다.그렇기에 불변하다, 불변 객체라고 부르기도 한다.
- 이전 변수 관련 글에서도 언급했지만 자바스크립트에서 아래의 원시값들은 전부 불변하다
1. Boolean
2. null
3. undefined
4. Number
5. String
6. Symbol (New in ECMAScript 6)


## Mutable 이란?
[MDN 공식문서 보기](https://developer.mozilla.org/ko/docs/Glossary/Mutable)

"Mutable"은 변경 가능(가변)한 변수의 유형을 말한다.
 JavaScript에서는, 원시 값이 아닌 객체와 배열만이 mutable하다.

### 특징
- 객체와 변수는 이전에 알아봤지만 메모리 주소를 참조하는 하여 값에 접근한다.
- 그래서 변수 이름이 새 값을 가리키도록 "만들 수 있지만" 이전 값은 여전히 메모리에 유지됩니다. 
- 따라서 Garbage collection이 필요하다.

### Mutable의 불변화

자바스크립트에서는 객체를 불변화하여 사용할 수 있는 방법이 2가지가 있다.
1. 객체의 방어적 복사(defensive copy)
- Object.assign
2. 불변객체화를 통한 객체 변경 방지
- Object.freeze

### 객체의 방어적 복사

```javascript
const user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

// 새로운 빈 객체에 user1을 copy한다.
const user2 = Object.assign({}, user1);
// user1과 user2는 참조값이 다르다.
console.log(user1 === user2); // false

user2.name = 'Kim';
console.log(user1.name); // Lee
console.log(user2.name); // Kim

// 객체 내부의 객체(Nested Object)는 Shallow copy된다.
console.log(user1.address === user2.address); // true

user1.address.city = 'Busan';
console.log(user1.address.city); // Busan
console.log(user2.address.city); 
```
위 코드에서 user1 객체를 빈객체에 복사하여 새로운 객체 user2를 생성하였다. user1과 user2는 어드레스를 공유하지 않으므로 한 객체를 변경하여도 다른 객체에 아무런 영향을 주지 않게 된다.


### 불변객체화를 통한 객체 변경 방지

```javascript
const user1 = {
  name: 'Lee',
  address: {
    city: 'Seoul'
  }
};

// Object.assign은 완전한 deep copy를 지원하지 않는다.
const user2 = Object.assign({}, user1, {name: 'Kim'});

console.log(user1.name); // Lee
console.log(user2.name); // Kim

Object.freeze(user1);

user1.name = 'Kim'; // 무시된다!

console.log(user1); // { name: 'Lee', address: { city: 'Seoul' } }

console.log(Object.isFrozen(user1)); // true
```
Object.freeze()를 사용하여 불변(immutable) 객체로 만들수 있다. 하지만 객체 내부의 객체(Nested Object)는 변경가능하다.


### 라이브러리를 통한 객체 불변화

Object.assign과 Object.freeze을 사용하여 불변 객체를 만드는 방법은 번거러울 뿐더러 성능상 이슈가 있어서 큰 객체에는 사용하지 않는 것이 좋다.그래서 또 다른 대안으로 Facebook이 제공하는 Immutable.js를 사용하는 방법이 있다. 아래의 링크를 통해서 내용을 확인할 수 있다.

[Immutable.js 바로가기](https://immutable-js.com/)