---
layout: post
title: "자유자재로 변하는 웹디자인(반응형디자인)"
author: "Nostrss"
comments: true
tags: network secure http https
excerpt_separator:
sticky:
hidden:
---

## Responsive Design(반응형 디자인)이란? 
[MDN 반응형 디자인 바로가기](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Responsive_Design)

PC화면 만 있던 시대와 달리 현재는 스마트폰, 태블릿과 같이 디스플레이 사이즈가 다양하게 존재한다. 그런데 PC모니터의 넓은 화면을 그대로 작은 기기의 화면에 보여주게 되면 가독성과 심미성, 기능성이 원래의 의도와는 달라지는 경우가 발생한다.

그래서 화면의 사이즈에 따라 격자시스템을 달리 적용하여 보여주는 것을 반응형 디자인이라고 한다. 

## 디스플레이 사이즈별 그리드 시스템
[부트스트랩의 그리드 시스템](http://bootstrapk.com/css/#grid-options)

많이 쓰이는 CSS라이브러리인 부트스트랩에서는 위의 링크처럼 그리드 시스템을 정의하고 있다. 워낙 유명한 라이브러리이기 때문에 위의 기준에 맞춰서 반응형 디자인을 구축하게 된다면 큰 무리는 없을 듯 하다.

## 미디어 쿼리 
[MDN 미디어쿼리 바로가기](https://developer.mozilla.org/ko/docs/Web/CSS/@media)

반응형 디자인 코드 예시
```javascript
import styled from '@emotion/styled';

export default function ResponsiveDesignPage() {
  const Wrapper = styled.div`
    width: 1000px;
    height: 1000px;
    background-color: red;

    @media (min-width: 768px) and (max-width: 991px) {
      width: 500px;
      height: 500px;
      background-color: green;
    }

    @media (max-width: 767px) {
      width: 100%;
      height: 100px;
      background-color: blue;
      /* display: none; */
    }
  `;

  return <Wrapper>상자</Wrapper>;
}
```
위와 같이 반응형 디자인을 할 경우 다양한 사이즈의 디스플레이에 맞춰서 화면을 보여 줄수 있는 장점이 있다.



