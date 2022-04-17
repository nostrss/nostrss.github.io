---
layout: post
title: '[js기초] node.js란?'
author: 'Nostrss'
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

## node.js란?
Ryan Dahl이 2009년에 발표했다. 
[node.js 홈페이지 바로가기](https://nodejs.org/ko/)
위의 홈페이지에 들어가보면 아래와 같은 문구가 있다.

> Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임입니다.

그렇다면 JavaScript 런타임은 무엇을 뜻하는 것일까?
> 브라우저가 아닌 다른 곳에서 javascript를 실행시킬 수 있는 환경을 만들어준다

흔히 node.js가 서버용 언어, 서버에서만 사용하는 것으로 말하지만 정확히 말하면 그건 틀린 말이다.(물론 서버에서 많이 사용하긴 한다 ^^)
javscript를 이용해 데스크탑 App을 만들수 있는 electron의 경우에도 node.js를 이용한다.
[electron 홈페이지 바로가기](https://www.electronjs.org/)

즉, 정리하자면 web의 환경에서 벗어 날 수 있도록 해준 것이 node.js라고 볼 수 있다.


### node.js의 장점
- 아파치 등 별도의 소프트웨어 없이 http 서버 라이브러리를 포함하여 웹 서버 동작이 가능하다.
- socket.io API만 이용하면 싱글 스레드 기반 멀티 플랙싱을 기반으로 대용량 사용자에 대한 푸쉬 처리를 가능하게 한다. (WAS는 쓰레드 수 만큼 밖에 동시 connection처리를 할 수 없다 )
- 서버 플랫폼으로서 높은 인기를 가지고 있어 개발자 커뮤니티가 활성화 되어있고, npm을 통해 왠만한 기능은 이미 다른 개발자가 모듈로 구현해 두었다.






