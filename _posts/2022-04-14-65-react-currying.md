---
layout: post
title: 'React 커링기법이란?'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---

## 커링(Currying) 기법
`커링(Currying)` 기법은 인자가 여러개인 함수의 일부 인자를 고정시키는 새로운 함수를 만드는 기법이다.

```javascript
function helloFunc(word, name) {
    console.log(`${word}, ${name}`);
}
```
word와 name이라는 두 개의 인자를 받아서 출력해주는 단순한 형태의 함수입니다.

이 함수에 커링을 적용해 봅시다.
```javascript
function helloFunc(word) {
    return function (name) {
        console.log(`${word}, ${name}`);
    };
}

const printHello = helloFunc("hello"); 
printHello("Tibetan Fox"); // hello, Tibetan Fox
printHello("Tiger");       // hello, Tiger
```
아까의 함수에 커링을 적용하면 이렇게 됩니다.
첫 번째로 받던 인자인 word를 hello라는 값으로 고정하고 name만 변경하면서 사용 가능한 것 또한 볼 수 있습니다.

즉 커링 기법은 일부 인자에 `같은 값`을 `반복적`으로 사용할 때 그 반복되는 인자를 `고정`함으로써 중복을 최소화 하기에 적합한 기법입니다.

## 주의사항

커링 기법을 적용할 때는 `인자의 순서`가 매우 중요합니다. `변동 가능성`이 `적은` 인자는 `앞`에, 변동 가능성이 높은 인자는 뒤에 배치해야 합니다. 반드시 이 점을 고려하면서 커링을 사용해야 합니다.