---
layout: post
title: "[js]객체 복사가 이렇게 어려운 것인가.."
author: "Nostrss"
comments: true
tags: javascript secure
excerpt_separator:
sticky:
hidden:
---

## 얕은 복사(Shallow Copy)

일반적으로 사용하는 `배열`, `객체`의 경우 원시값과 다른 점 중 하나가 `참조에 의해(by reference)` 저장되고 복사된다는 것이다.
원시값의 경우 값을 할당하면 `값 그대로 저장` 할당이 되는점에서 차이가 있다. 여기서 `값 그대로 저장`에 주의를 가질 필요가 있다.
배열과 객체는 할당이 객체가 저장되어있는 '메모리 주소’인 객체에 대한 `참조 값, 메모리주소`가 저장된다.

아래의 예시를 보자

```javascript
let user = { name: 'John' };

let admin = user;

admin.name = 'Pete'; // 'admin' 참조 값에 의해 변경됨

alert(user.name); // 'Pete'가 출력됨. 'user' 참조 값을 이용해 변경사항을 확인함
```

위의 예제에서 이상한 점이 있다. admin.name에 Pete를 할당 했는데, user.name이 Pete가 되었다.
이 이유가 바로 참조에 의해 저장 때문이다. 다른 말로는 이것을 `shallow copy`라고 부른다.

## 깊은복사(Deep Copy)

그렇다면 정말 진짜 복사 및 할당을 하려면 어떻게 해야할까?

### 1.JSON 활용법
MDN에서는 이렇게 안내를 하고 있는 것을 찾았다.

[MDN Deep Copy 바로가기](https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy)

>In JavaScript, standard built-in object-copy operations (spread syntax, Array.prototype.concat(), Array.prototype.slice(), Array.from(), Object.assign(), and Object.create()) do not create deep copies (instead, they create shallow copies).

일반적으로 사용하는 `스프레드 함수`등의 방법이 대부분 `얕은 복사`라고 애기하고 있다. 조금 더 정확히 말하자면 스프레드 함수는 1뎁스는 깊은복사가 되는데 중첩객체 처럼 2뎁스 이상은 깊은복사가 되지 않는다.


>One way to make a deep copy of a JavaScript object, if it can be serialized, is to use JSON.stringify() to convert the object to a JSON string, and then JSON.parse() to convert the string back into a (completely new) JavaScript object:

`MDN`에서는 `JSON`으로 `String`형식으로 바꿨다가 다시 `객체`로 바꾸어 저장하는 방법을 알려주고 있었다...

하지만 이 경우 `느리다는 것`과 객체가 `function`일 경우,`undefined`로 처리한다는 것이 단점이라고 한다.

### 2.재귀함수 활용

[커스텀 재귀함수로 깊은 복사하기 : 출처 바로가기](https://leonkong.cc/posts/js-deep-copy.html)
```javascript
function cloneObject(obj) {
  var clone = {};
  for (var key in obj) {
    if (typeof obj[key] == "object" && obj[key] != null) {
      clone[key] = cloneObject(obj[key]);
    } else {
      clone[key] = obj[key];
    }
  }

  return clone;
}
```
음 매번 이런 함수를 객체에 맞춰서 짜준다는게 쉽지 않아 보인다. 재귀함수 자체도 어려운데 말이다.

### 3. lodash의 cloneDeep() 사용
[lodash 바로가기](https://lodash.com/docs/4.17.15#cloneDeep)

많이 쓰이는 라이브러리 중 하나인 `lodash`를 쓰는 방법이 있다.
설치만 하면 쉽게 쓸 수 있겠지만 만약 `코딩테스트`처럼 설치할 환경이 아니라면..  사용이 불가능할 수도 있다.

때에 따라 적절한 깊은 복사 방법을 찾아서 사용하는 수밖에 없을 것 같다










