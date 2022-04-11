---
layout: post
title: '상태 관리 도구 비교 '
author: 'Nostrss'
comments: true
tags: memo codecamp
excerpt_separator:
sticky:
hidden:
---

## 이번주 과정

지금까진 Props 드릴링 부모 > 자식 > 자식
이젠 글로벌 state를 배운다

>1. 글로벌 스테이트? props가 필요없대 > recoil
>2. 로그인에도 역사가 있다 > AcceessToken / refreshToken
>3. Next.js 렌더링 원리 > diffing /dydration
>4. 잠깐 이것 먼저 실행해줘 > closure /HOC /HOF
>5. 폼을 자동으로 만들어준다 > React-hook-form


## rest와 graphql 차이 
### under-fetching / over-fetching

## Props의 실체
props는 결국 함수의 매개변수다!

## el의 실체
## graphql - variables 실체
- rest-api의 under, over feching문제를 해결한 것이 graphql
  - 관련 링크 : https://www.howtographql.com/basics/1-graphql-is-the-better-rest/

## 정규표현식
https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions

이메일 검증 정규표현식 : 

## glober state
- props drilling 이 발생한다. > 모든 컴포넌트가 사용할 수 있는 state가 있으면 좋겠다
- https://slog.website/post/13

발전순서
- global-state > redux > mobX > swr 

최근 트렌드

1. api 저장용 state
  - rest : react-query
  - gql : apollo-client

2. 일반 global-state로 구분하여
  - context-api(react 자체 제공) > recoil

이렇게 2개로 나뉜 이유 : fetchPolicy 정책 때문

cashestate에 fetch data가 일단 저장 - 그래서 undefined
그 이후 cashestate에서 {data}에 들어온다. 그래서 state변화가 있으니 리랜더링 된다.

fetchPolicy
https://www.apollographql.com/docs/react/data/queries/#setting-a-fetch-policy

  - cache-first (디폴트값)
    - cashestate에 기존에 받아둔 정보가 있는 것을 불러오는 것
  - network-only
    - cashestate 확인 안하고 바로 쿼리 날리는것?

recoil-state(store라고 부른다)









