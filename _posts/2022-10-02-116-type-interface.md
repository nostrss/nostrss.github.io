---
layout: post
title: '[ts] 추상 클래스와 interface'
author: 'Nostrss'
comments: true
tags: typescript
excerpt_separator:
sticky:
hidden:
---

## 추상 클래스란?

- 추상 클래스는 추상 메소드를 하나 이상 포함한 클래스이다.

### 추상 메소드란?

- 정의되지 않은 메소드를 말한다.

```typescript
abstract class User {
  constructor(protected firstName: string, protected lastName: string) {}
  // 추상 메소드
  abstract sayHi(name: string): string;
  abstract fullName(): string;
}
```

### 추상 클래스 특징

- 인스턴스를 생성할 수 없다. (new를 쓸수 없다!)
- 상속만 가능하다.

## typescript로 추상 클래스 구현

```typescript
abstract class User {
  constructor(protected firstName: string, protected lastName: string) {}
  abstract sayHi(name: string): string;
  abstract fullName(): string;
}
```

```typescript
// protected 추상 클래스로부터 상속받은 클래스들이 property에 접근하도록 허용해준다

class Player extends User {
  sayHi(name: string) {
    return `Hello ${name}.`;
  }
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}
```

### javascript로 빌드 code

```javascript
class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

class Player extends User {
  sayHi(name) {
    return `Hello ${name}.`;
  }
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}
```

## typescript interface 키워드로 추상 클래스 구현

```typescript
interface User {
  firstName: string;
  lastName: string;
  sayHi(name: string): string;
  fullName(): string;
}

class Player implements User {
  constructor(public firstName: string, public lastName: string) {}
  sayHi(name: string) {
    return `Hello ${name}.`;
  }
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}
```

### javascript로 빌드 시 code

```javascript
class Player {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  sayHi(name) {
    return `Hello ${name}.`;
  }
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}
```

- interface로 작성한 부분이 javascirpt에서는 보이지 않는다.
- 단순히 object의 모양만 설명하기 때문에 js에는 보이지 않게 된다.
