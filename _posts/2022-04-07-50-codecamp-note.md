---
layout: post
title: '[코드캠프#9] 메모'
author: 'Nostrss'
comments: true
tags: memo codecamp
excerpt_separator:
sticky:
hidden:
---

## CORS

브라우저가 차단하는 기능
CORS는 Cross-Origin Resource Sharing의 약자
출처(Origin)란?
출처(Origin)란 URL 구조에서 살펴본 Protocal, Host, Port를 합친 것을 말합니다. 브라우저 개발자 도구의 콘솔 창에 location.origin를 실행하면 출처를 확인할 수 있습니다.

cors가 허용되지 않는 api의 경우
이 경우 백엔드나 모바일에서 api요청을 하고 프론트는 백엔드에서 받아와야한다.
이런 경우 백엔드를 프록시 서버라고 한다. 최초api 요청자를 숨기는 역할

리버스 프록시 서버
요청자가 아닌 출처를 숨기는 프록시 서버(nginx)
애플리케이션 서버를 감추는 역할

## 이미지 처리

이미지는 일반적으로 데이터 베이스에 저장하지 않는다. 이미지 실제 파일은 별도로 저장을 하는 서버를 둔다. 이미지 주소를 DB에 저장한다.

useRef를 통해 이미지 업로드 버튼과 파일명등을 받고 

