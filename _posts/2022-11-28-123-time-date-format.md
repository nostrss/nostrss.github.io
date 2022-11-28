---
layout: post
title: '[코드지갑] Intl(Time & Date Format)'
author: 'Nostrss'
comments: true
tags: time date intl format
excerpt_separator:
sticky:
hidden:
---

간단해 보이지만 까다롭고 어려운 작업이 있는데 바로 날짜와 시간 표기 방법이다.

나라마다도 다르고, 표기법이 너무나 다양하기 때문에 일일히 전부 커스터 마이징하기에는 너무 손이 많이 가는 작업이다.

다행히 javascript에서 편하게 쓸 수 있는 내장 객체가 있어서 정리해봤다.

## Intl

[MDN 문서보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat)

[ECMAScript Internationalization API Specification](https://tc39.es/ecma402/#datetimeformat-objects)

### 사용법

```javascript
const date = new Date();
const options = {
  weekday: 'long',
  year: 'numeric',
  month: 'long',
  day: 'numeric',
};
console.log(new Intl.DateTimeFormat('en-US', options).format(date));
```

### Options

옵션이 상당히 다양한데 정리하면 아래와 같다.

```javascript
[
  { weekday: ['narrow', 'short', 'long'] },
  { era: ['narrow', 'short', 'long'] },
  { year: ['2-digit', 'numeric'] },
  { month: ['2-digit', 'numeric', 'narrow', 'short', 'long'] },
  { day: ['2-digit', 'numeric'] },
  { dayPeriod: ['narrow', 'short', 'long'] },
  { hour: ['2-digit', 'numeric'] },
  { minute: ['2-digit', 'numeric'] },
  { second: ['2-digit', 'numeric'] },
  {
    timeZoneName: [
      'short',
      'long',
      'shortOffset',
      'longOffset',
      'shortGeneric',
      'longGeneric',
    ],
  },
];
```

저 많은 옵션이 어떻게 보이는지 전부 확인해보기가 어려워서 페이지에 선택 할 수 있도록 간단히 구현을 해봤는데 유용하게 쓸 수 있을 듯하다.

[option 사용해보기](https://nostrss.github.io/playground/javascript/intl)
