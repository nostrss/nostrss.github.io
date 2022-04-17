---
layout: post
title: '[js기초] 변수 선언 3가지 방법'
author: 'Nostrss'
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

`자바스크립트`에서 변수 선언은 3가지 방법이 존재한다.
- `var` : 오래된 변수 선언 키워드입니다. 현재는 사용을 권장하지 않는다. 오래된 코드에서 볼 수 있다.
- `const` : `ES2015`에 추가되었다. let과 비슷하지만, 변수의 값을 변경할 수 없습니다.
- `let` : `ES2015`에 추가되었다. 모던한 변수 선언 키워드입니다.


## const
변화하지 않는 변수를 선언할 땐, `const`를 사용합니다.

```javascript
const myBirthday = '18.04.1982';
```
이렇게 const로 선언한 변수를 '상수(constant)'라고 부릅니다. 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생합니다.

```javascript
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```
변수값이 절대 변경되지 않을 것이라 확신하면, `const`를 사용해 변수를 선언하도록 해야한다.

## let
const와 반대로 변화하는 변수를 선언할 떄 사용한다.

```javascript
let message;

message = 'Hello!';

message = 'World!'; // 값이 변경되었습니다.

alert(message);
```

## var
현재는 거의 사용되지 않지만 오래된 코드에서 볼수 있는 변수 선언 키워드이다.

### var는 블록 스코프가 없습니다.
var로 선언한 변수의 스코프는 함수 스코프이거나 `전역 스코프`입니다. 블록 기준으로 스코프가 생기지 않기 때문에 `블록 밖에서 접근 가능`합니다.

예시:
```javascript
if (true) {
  var test = true; // 'let' 대신 'var'를 사용했습니다.
}

alert(test); // true(if 문이 끝났어도 변수에 여전히 접근할 수 있음)
```
var는 코드 블록을 무시하기 때문에 test는 전역 변수가 됩니다. 전역 스코프에서 이 변수에 접근할 수 있습니다.

만약 두 번째 행에서 var test가 아닌 let test를 사용했다면, 변수 test는 if문 안에서만 접근할 수 있습니다.
```javascript
if (true) {
  let test = true; // 'let'으로 변수를 선언함
}

alert(test); // Error: test is not defined
```

위와 같은 문제로 인해 `var`은 `호이스팅` 등의 문제를 일으키게 된다. 앞으로는 사용하지 않도록 하자!!
