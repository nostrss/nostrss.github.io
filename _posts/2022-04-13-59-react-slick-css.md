---
layout: post
title: 'React Slick Css 수정하기'
author: 'Nostrss'
comments: true
tags: react javascript nextjs emotionjs
excerpt_separator:
sticky:
hidden:
---

## React Slick 이란??

[React Slick 공식문서 보러가기](https://react-slick.neostack.com/)

페이지에 `캐러셀` 효과를 주는 React 라이브러리 중에 하나이다. 다운로드 수도 높고 믿을 수 있는 라이브러리 라고 한다.

나는 라이브러리를 설치해서 캐러셀 효과를 지금 프로젝트에 적용하고 있는데, 캐러셀의 이전, 다음 Arrow가 흰색이라 배경화면이 하얀색이면 보이지 않아 문제가 있었다. 그리고 사이즈도 작아서 키울수 있는 방법이 있을지 찾아봤다.

### React 공식 문서상 방법 

[React 공식 문서상 Arrow 커스터마이징 하는 법](https://react-slick.neostack.com/docs/example/custom-arrows)

이와 동일하게 나의 코드에 적용을 해보면 Arrow가 바뀌는 것을 확인 할 수 있었다. 하지만..

```javascript
function SampleNextArrow(props) {
  const { className, style, onClick } = props;
  return (
    <div
      className={className}
      style={{ ...style, display: "block", background: "red", 
      //내가 추가한 항목
      color: "black"
      }}
      onClick={onClick}
    />
  );
}
```
색깔을 black으로 지정을 해봐도 바뀌지 않아서.. 다른 방법을 시도 해봤다.

### Emotion으로 Css 바꿔주기

현재 나의 프로젝트는 `react`, `next.js` 그리고 `emotion.js`를 사용하고 있다.
혹시 `emotion.js`를 안쓰시는 분들은 이 방법으로 될지 모르겠다.

아래와 같이 react-slick의 컴포넌트를 다시 css로 스타일링을 하고 jsx로 작성을 해주니 변경이 되는 것을 확인했다.

```javascript
import styled from '@emotion/styled';
import Slider from 'react-slick';
import 'slick-carousel/slick/slick.css';
import 'slick-carousel/slick/slick-theme.css';

 const StyledSlider = styled(Slider)`

  .slick-prev {
    left: 0px;
    z-index: 10;
  }
  .slick-next {
    right: 15px;
    z-index: 10;
  }
  .slick-next:before {
    color: black;   // arrow 색상 변경
    font-size: 40px; // arrow 크기 변경
  }

  .slick-prev:before {
    color: black;
    font-size: 40px;
  }
`;

```

`.slick-prev` `.slick-next` 는 클래스명인데 `slick-theme.css` 파일에 들어가면 여러 클래스명을 확인 할 수 있고 좀 더 다양한 커스터마이징을 하려면 클래스명을 추가해서 사용하면 된다.
