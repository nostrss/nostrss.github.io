---
layout: post
title: '브라우저는 비밀번호를 어떻게 기억할까?'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---

## Cookie(쿠키)

HTTP `쿠키`(웹 쿠키, 브라우저 쿠키)는 서버가 사용자의 웹 브라우저에 전송하는 `작은 데이터 조각`이다. 브라우저는 그 데이터 조각들을 저장해 놓았다가, 동일한 서버에 재 요청 시 저장된 데이터를 함께 전송합니다. 쿠키는 두 요청이 동일한 브라우저에서 들어왔는지 아닌지를 판단할 때 주로 사용합니다. 이를 이용하면 사용자의 로그인 상태를 유지할 수 있습니다.

### Cookie의 목적

>1. 세션 관리(Session management)
  - 서버에 저장해야 할 로그인, 장바구니, 게임 스코어 등의 정보 관리
>2. 개인화(Personalization)
  - 사용자 선호, 테마 등의 세팅
>3. 트래킹(Tracking)
  - 사용자 행동을 기록하고 분석하는 용도

### Cookie의 라이프타임

1. 세션 쿠키
- `세션쿠키`는 현재 세션이 끝날 때 삭제됩니다. 브라우저는 "현재 세션"이 끝나는 시점을 정의하며, 어떤 브라우저들은 재시작할 때 세션을 복원해 세션 쿠키가 무기한 존재할 수 있도록 합니다.
2. `영속적인 쿠키`는 `Expires` 속성에 명시된 날짜에 삭제되거나, Max-Age 속성에 명시된 기간 이후에 삭제됩니다.


## 세션스토리지와 로컬 스토리지
- `HTML5`에서 추가된 저장소

### Session(세션)
- `sessionStorage`는 `localStorage`와 비슷하지만, `localStorage`의 데이터는 만료되지 않고, `sessionStorage`의 데이터는 페이지 세션이 끝날 때 제거되는 차이가 있습니다.

- 페이지 세션은 브라우저가 열려있는 한 새로고침과 페이지 복구를 거쳐도 남아있습니다.
- 페이지를 새로운 탭이나 창에서 열면, 세션 쿠키의 동작과는 다르게 최상위 브라우징 맥락의 값을 가진 새로운 세션을 생성합니다.
- 같은 URL을 다수의 탭/창에서 열면 각각의 탭/창에 대해 새로운 sessionStorage를 생성합니다.
- 탭/창을 닫으면 세션이 끝나고 sessionStorage 안의 객체를 초기화합니다.
- sessionStorage에 저장한 자료는 페이지 프로토콜별로 구분합니다. 특히 HTTP(http://example.com)로 방문한 페이지에서 저장한 데이터는 같은 페이지의 HTTPS(https://example.com)와는 다른 sessionStorage에 저장됩니다.
- `세션`은 `쿠키`를 기반하고 있지만, 사용자 정보 파일을 브라우저에 저장하는 쿠키와 달리 세션은 `서버` 측에서 관리한다.
- 서버에서는 클라이언트를 구분하기 위해 세션 ID를 부여하며 웹 브라우저가 서버에 접속해서 브라우저를 종료할 때까지 인증상태를 유지한다.
- `보안`면에서 `쿠키(cookie)`보다 유리하다.

### 로컬 스토리지
- 저장한 데이터는 브라우저 세션 간에 공유됩니다. localStorage는 sessionStorage와 비슷하지만, `localStorage`의 데이터는 만료되지 않고 sessionStorage의 데이터는 페이지 세션이 끝날 때, 즉 페이지를 닫을 때 사라지는 점이 다릅니다. ("사생활 보호 모드" 중 생성한 localStorage 데이터는 마지막 "사생활 보호" 탭이 닫힐 때 지워집니다.)

- localStorage에 저장한 자료는 페이지 프로토콜별로 구분합니다. 특히 HTTP(http://example.com)로 방문한 페이지에서 저장한 데이터는 같은 페이지의 HTTPS(https://example.com)와는 다른 localStorage에 저장됩니다.

