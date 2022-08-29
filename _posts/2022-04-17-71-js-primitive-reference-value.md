---
layout: post
title: "[JS] 값의 종류(Primitive, reference)"
author: "Nostrss"
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

### 값의 종류(타입)

자바스크립트에서 값의 종류는 아래와 같다

- 원시값(Primitive)
  - 수 (Number)
  - BigInt
  - 문자열 (String)
  - 부울 (Boolean)
  - 기호 (Symbol) `(ES2015에 새롭게 추가)`
  - 정의되지 않음 (Undefined)
  - 널 (Null)

- 객체 (레퍼런스 타입)
  - 함수 (Function)
  - 배열 (Array)
  - 날짜 (Date)
  - 정규식 (RegExp) 등

### 원시값

객체를 제외한 모든 타입은 불변 값(변경할 수 없는 값)을 정의합니다. 예를 들어 (C 언어와는 달리) 문자열은 불변합니다. 이런 일련의 타입을 "원시 값"이라고 합니다. 

불변이라는 말이 사람을 조금 헷갈리게 해서 검색을 해봤다.
[참고 블로그 바로가기](https://velog.io/@dishate/Javascript-%EC%9B%90%EC%8B%9C%EA%B0%92-%EC%B0%B8%EC%A1%B0%EA%B0%92-%EB%B6%88%EB%B3%80%EC%84%B1-const)
이해하기가 쉽지 않은데, 일단은 스킵해야 할듯 하다. 언젠가는 깨닫는 날이 오겠지 ㅎ

#### BigInt
원시값중 잘 모르는 부분만 찾아봤다.

- BigInt는 원시값이 가장 안정적으로 나타낼수 있는 최대치를 넘는 큰 정수를 표현하는 내장 객체라고 한다.

최대치 정수 구하기

```javascript
Number.MAX_SAFE_INTEGER; // 9007199254740991
```

`9007199254740991`를 넘는 정수 범위는 `BigInt` 타입이라고 하는 것 같다.

그런데 그럼 가장 작은 정수 범위는 마이너스(-)만 붙이면 되는건가?

```javascript
Number.MIN_SAFE_INTEGER; // -9007199254740991
```

오 그냥 쳐봤는데 나온다.

> 즉, BigInt는 -9007199254740991 보다 작고 9007199254740991 보다 큰 정수형을 표현 할 수 있는 타입

이렇게 일단 이해를 해두면 될 것 같다.

#### NULL(널)

`typeof` 연산자를 사용하면 어떤 자료형인지 아래와 같이 알 수가 있다.

```javascript
typeof undefined; // undefined
typeof true; // boolean
typeof "string"; // string
typeof 123; //number
typeof 9007199254740992n; //bigint
typeof Symbol(); //symbol
typeof null;
```

그런데 `널(NULL)`의 경우에는..

```javascript
typeof null; //object
```

`object`라고 나온다. number 또는 0 이렇게 나오면 오히려 수긍을 하겠는데 객체라고 나온다. 이는 자바스크립트 태생적으로 이렇게 만들어졌고 오류(?)라고 봐야 하는지 모르겠지만, 이대로 유지하기로 했다고 하니 그냥 관습적으로 알고 있어야 할 내용 같다.




### 객체
MDN에서는 객체를 아래와 같이 정의하고 있다.

>JavaScript에서의 객체는 속성의 컬렉션으로 볼 수 있습니다. 객체 리터럴 구문을 사용해 제한적으로 속성을 초기화할 수의 있고, 그 후에 속성을 추가하거나 제거할 수도 있습니다. 속성 값으로는 다른 객체를 포함해 모든 타입을 사용할 수 있으므로 복잡한 자료구조의 구축이 가능합니다. 속성은 '키' 값으로 식별하며, 키 값으로는 문자열 값이나 심볼을 사용할 수 있습니다.

여기서 객체 리터럴이란 
>객체 리터럴은 중괄호({})로 묶인 0개 이상인 객체의 속성명과 관련 값 쌍 목록입니다. 문의 시작에 객체 리터럴을 사용해서는 안됩니다. 이는 {가 블록의 시작으로 해석되기 때문에 오류를 이끌거나 의도한 대로 동작하지 않습니다.

텍스트로 보니 이해가 어려운데 자세히 보니 지금까지 사용해오던 객체의 모습, 형태를 말하는 듯하다

```javascript
const car = {
   myCar: "Saturn", 
   getCar: carTypes("Honda"), 
   special: sales 
   };
```

그리고 객체 속성에는 데이터 속성과 접근자 속성 두 종류가 있습니다.
자세한 내용은 MDN을 참고하자. 솔직히 이 부분도 잘 이해가 가지 않는다.

[MDN 공식문서 보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures#%EA%B0%9D%EC%B2%B4)

#### 객체를 레퍼런스 타입 이라고 부르는 이유?

사실상 자바스크립트에서 원시 타입을 제외한 나머지는 참조타입(객체(Object))이라 할 수 있다. 배열과 객체, 그리고 함수가 대표적이며, 원시타입과 가장 큰 차이점은 변수의 크기가 동적으로 변한다는 것이다. 이러한 특징 때문에 Object의 데이터 자체는 별도의 메모리 공간(heap)에 저장되며, 변수에 할당 시 데이터에 대한 주소값이 저장되기 때문에 자바스크립트 엔진이 변수가 가지고 있는 메모리 주소를 이용해서 변수의 값에 접근하게 되는것이다.

이렇게 실제 값이 아닌 데이터의 주소를 가지고 있기 때문에 참조타입, Reference Type이라고 부른다.

### ECMA 공식 명세서

몇달을 공부했지만 처음으로 ECMA 공식 문서를 찾아서 들어가봤다. 전부 영문이긴 하지만 어찌보면 가장 표준 문서이기에 기록을 위해 남겨 놓았다
[ECMA 명세서 바로가기 ](https://tc39.es/ecma262/#sec-ecmascript-data-types-and-values)
