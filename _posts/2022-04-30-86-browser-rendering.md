---
layout: post
title: " 브라우저는 무슨일을 하고 있을까? "
author: "Nostrss"
comments: true
tags: javascript 
excerpt_separator:
sticky:
hidden:
---


[MDN 공식문서 보기](https://developer.mozilla.org/ko/docs/Web/Performance/Critical_rendering_path)
>참고로 위 링크의 한글 문서는 현재 초안 작성 중이다


## DOM 트리 생성
- 브라우저는 다운로드 받은 문서에서 HTML을 통해 DOM(Document Object Model)트리를 생성한다.

## CSSOM 트리 생성
- CSS를 분석하여 CSSOM 트리를 생성한다.

![image with caption](https://web-dev.imgix.net/image/C47gYyWYVMMhDmtYSLOWazuyePF2/b6Z2Gu6UD1x1imOu1tJV.png?auto=format&w=1600 'Render-tree Construction, Layout, and Paint')

## Render Tree 생성
- 위에서 생성한 DOM과 CSSOM을 합쳐서 render Tree를 생성한다.

>The render tree only captures visible content. The head section (generally) doesn't contain any visible information, and is therefore not included in the render tree. If there's a display: none; set on an element, neither it, nor any of its descendants, are in the render tree.

- 그리고 위의 구문에서 조금 더 자세한 설명이 나오는데, 이 단계에서는 오직 보이는 것에만 집중한다고 한다.

- 즉 `head` 태그 안의 내용, 아니면 `display : none`과 같이 현재 보이지 않는 것들은 Render Tree에 포함되지 않는다고 한다.

## 레이아웃 단계

>Once the render tree is built, layout becomes possible. Layout is dependent on the size of screen. The layout step determines where and how the elements are positioned on the page, determining the width and height of each element, and where they are in relation to each other.

- 렌더 트리가 생성되면 이제 레이아웃을 생성할 수가 있게 된다. 레이아웃은 스크린의 사이즈에 따라 달라지게 된다.
- 레이아웃 단계에서는 엘레멘트 요소들이 페이지 어디에 위치할지, 각 엘레멘트의 가로 세로 크기, 그리고 각 엘레멘트들의 관계가 결정되게 된다.

## Paint 단계
- 마지막 단계로 스크렌의 픽셀을 색칠하는 단계


### 착안점
- 애니메이션 효과처럼 위치의 변화를 주게 될 경우 리렌더링에 많은 리소스가 소모됨을 알 수 있다
- 위치가 변하는 경우와 색깔만 변하는 경우를 비교해 보자면

1) 위치가 변하는 경우
- DOM > CSSOM > Render Tree > Layout > Paint > (Layout > Paint) > (Layout > Paint) ...

2) 색깔만 변하는 경우
- DOM > CSSOM > Render Tree > Layout > Paint > Paint > Paint > Paint >...

2번의 경우와 비교했을 떄 Layout 단계를 1번 더 거쳐야 하기 때문에 브라우저 렌더링시 더 부하가 걸리게 됨을 알 수 있다.

추후 최적화를 고려한다면 이렇게 브라우저 렌더링도 고려하는 것도 좋을 것 같다.
