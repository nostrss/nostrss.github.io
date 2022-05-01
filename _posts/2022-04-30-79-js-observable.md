---
layout: post
title: "[js] Observable Object "
author: "Nostrss"
comments: true
tags: javascript 
excerpt_separator:
sticky:
hidden:
---

## Observable 객체
아쉽게 `MDN`에서 정확한 문서를 찾지는 못했다. 하지만 연관있는 문서 몇개를 찾아서 링크를 남겨둔다
[MDN Observer Api 문서 바로가기](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)
[모던 자바스크립트 Proxy 바로가기](https://ko.javascript.info/proxy)

## Observable
위의 링크들을 남겨둔 이유는 `Observable`가 단어 뜻처럼 `지속`적으로 `관찰` 가능한 `객체`라는 의미이기 때문이다.
변경될 때마다 변경된 값을 `비동기`적으로 제공하겠다는 것을 구현해 놓은 객체라고 생각하면 된다.

자바스크립트에서는 1개 이상의 item을 처리할 때 `async`와 같은 방법을 사용한다.
여기서 `promise` 방식을 사용해 구현하면 단 하나의 data를 받고 종료되어 버리는 패턴을 가지고 있어,
데이터를 시간의 흐름에 따라 순차적으로 받아야 하는 상황이 생긴다면 promise를 사용해 처리할 수 없다.

### Promise와의 차이점 
promise와의 차이점은 `취소`가 가능하다는 것인데
Observable은 순차적으로 데이터를 받아 처리하기 때문에 취소할 수가 있다.

이는 `다수의 비동기`적인 값들을 방출할 때 사용된다.

### Observable의 특성
- Item을 여러개 방출 할 수 있다.
- Item의 발행 완료 이벤트를 방출할 수 있다.
- Item의 발행 도중 에러가 발생했다면 여러 이벤트를 방출 할 수 있다.

### Observable의 사용 용도
- 데이터가 여러번 발행 될 수 있는 곳에서 주로 사용한다.
- 데이터가 1000번 미만으로 발행되는 경우에 사용하는 것이 좋다.
- `Out of Memory Error`가 발생되지 않을 가능성이 높은 곳에서 사용하는 것이 좋다.
- 터치 이벤트, 키보드 입력과 같은 GUI 이벤트를 받을 때 주로 사용한다.
