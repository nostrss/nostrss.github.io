---
layout: post
title: '[t] type과 interface'
author: 'Nostrss'
comments: true
tags: typescript
excerpt_separator:
sticky:
hidden:
---

## type

`typescript`에서 `type` 키워드의 사용 방법

- 타입을 정해줄 때

```javascript
type Nickname = string;
```

- 타입에 특정 값을 지정해 줄 때

```javascript
type Team = 'Red' | 'Blue' | 'Yellow';
```

- object의 모양을 typescript에 전달할 때

```javascript
type Player = {
  nickname: Nickname,
  team: Team,
};
```

## interface

- 보기에는 문법도 크게 다른 것 같지는 않지만
  `interface`는 오로지 오브젝트의 모양을 타입 스크립트에게 설명해 주기 위해서만 사용되는 키워드이다.

```javascript
interface Player{
    nickname: Nickname,
    team: Team
    health : Health
}
```

그리고 여러개의 동일한 이름의 `interface`가 선언되어 있을 경우 자동으로 합쳐주는 기능이 있다.

```javascript
interface UserAdd {
  name: string;
}

interface UserAdd {
  lastName: string;
}

interface UserAdd {
  age: number;
}

const userInfo: UserAdd = {
  name: 'Add interface',
  lastName: 'also Add',
  age: 10,
};
```

type 키워드의 경우 위와 같이 사용하지 못한다.
