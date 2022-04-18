---
layout: post
title: "useMutaion은 왜 배열로 구조분해할당을 받는가"
author: "Nostrss"
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

## Q : 왜 useMutation은 배열로 구조분해 할당을 받나요?

[GraphQl 문서보기](https://www.apollographql.com/docs/react/data/mutations/)

구조 분해 수업을 듣고 문득 궁금한 점이 있어서 알아본 내용이 있어서 정리를 위해 남긴다.

나는 useMutation의 경우 아래와 같이 배열로 구조분해 할당을 지금까지 받고 있었다. 

```javascript
const [createBoard] = useMutation(CREATE_BOARD);
```

구조분해할당을 배우기 전이라 막연히 이렇게 써야하는 줄만 알고 있었는데 문득 궁금한 점이 생겨서 조금 더 들여다 보았다.

`playground`에서 `useMutation`을 수행하면 아래와 같은 결과 값을 받는다.

```javascript
{
  "data": {
    "createBoard": {
      "_id": "625d0dfea8255b0029887dcc",
      "writer": "유즈뮤테이션",
      "title": "유즈뮤테이션은 왜 배열로 받나",
      "contents": "알려달라~"
    }
  }
}
```
결과 값을 보면 `객체`인 것을 알고 있다. 그런데 위의 코드에서 보면 `배열`로 `구조분해할당`을 받고 있는 이유가 궁금해서 `console`을 찍어보았다.

```javascript
console.log(createBoard);


ƒ (executeOptions) {
        if (executeOptions === void 0) { executeOptions = {}; }
        var _a = ref.current, client = _a.client, options = _a.options, mutation = _a.mutation;
        var baseOpti…
```

createBoard에는 `함수`가 들어있었다. 의외의 결과이다.

이번에는 다르게 콘솔에 찍어보았다.

```javascript
console.log(useMutation(CREATE_BOARD));


(2) [ƒ, {…}]
0: ƒ (executeOptions)
1: {called: false, loading: false, client: ApolloClient, reset: ƒ}
length: 2
[[Prototype]]: Array(0)

```
`배열`이다. 배열이 나오고 그 `첫번째 요소`로 함수가 들어있는 것을 볼 수 있었다.
즉 useMutation에서 배열로 구조분해 할당을 받은 건 이 이유였고 `함수를 할당`받으려고 하는 것이었다.

`query`처럼 먼가 plaryground의 결과값을 받아올 줄 알았는데 그게 아니라 `함수`를 받아오고 있었음을 확인 할 수 있었다.