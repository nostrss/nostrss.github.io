---
layout: post
title: '[코드캠프#11] 메모'
author: 'Nostrss'
comments: true
tags: memo codecamp
excerpt_separator:
sticky:
hidden:
---

리코일이 redux를 대체하기는 어렵다

로그인 방식 

scale up
sacle out
https://tecoble.techcourse.co.kr/post/2021-10-12-scale-up-scale-out/

stateful
Stateless
https://www.redhat.com/ko/topics/cloud-native-apps/stateful-vs-stateless

jwt 암호화 복호화
https://jwt.io/

jwt 토큰은 누구나 볼수나 있다. 그래서 중요한 정보는 적으면 안된다. 하지만 조작은 할 수 없다.
계좌번호, 포인트 기껏해야 아이디 정도

조작이 되었는지 알 수 있다.

암호화
양방향 암호화(jwt) - 다시 복호화가 가능해서 보안 문제가 있음
단방향 암호화 - 복호화 할 수 없는 암호화, hash해서 저장


1. 인증(Authentication) - 1번만 하면 된다
인증은 유저의 identification을 확인하는 절차이다
쉽게 설명하면 유저의 아이디와 비번을 확인하는 절차
인증을 하기 위해서 먼저 유저의 아이디와 비번을 생성할 수 있는 기능도 필요하다
login accessToken

2. 인가(Authorization) - 매번, header에 토큰만 넘기면 된다
사용자가 로그인하면, 해당 사용자가 맞는지 확인하는 절차
JSON WEB TOKEN(JWT)를 쓰면 인가가 수월함(서버가 유저 정보를 갖고 있으므로 데이터에서 유저의 권한 정보도 읽어들이면 됨)
access token을 통해 해당 유저 정보를 얻을 수 있으므로 해당 유저가 가지고 있는 권한(permission)도 확인가능

자기 자식에서만 사용할 수 있습니다. 라이브러리 오류시, 빈번하게 발생한다
- 해당 라이브러리만 컴포넌트로 빼낸다
