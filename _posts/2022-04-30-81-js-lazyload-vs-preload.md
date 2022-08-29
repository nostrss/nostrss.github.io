---
layout: post
title: "[js] 빨리 보여줄까? 나중에 보여줘도 되지? "
author: "Nostrss"
comments: true
tags: javascript 
excerpt_separator:
sticky:
hidden:
---

## Pre Load
[MDN Pre Load 문서 바로가기](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload)

미리 사용자에게 보여줄 컨텐츠를 다운로드 했다가, 필요할 떄 바로 보여주는 것을 말한다.

### Pre Load가 가능한 타입

>audio: Audio file, as typically used in <audio>.
>document: An HTML document intended to be embedded by a <frame> or <iframe>.
>embed: A resource to be embedded inside an <embed> element.
>fetch: Resource to be accessed by a fetch or XHR request, such as an ArrayBuffer or JSON file.
>font: Font file.
>image: Image file.
>object: A resource to be embedded inside an <object> element.
>script: JavaScript file.
>style: CSS stylesheet.
>track: WebVTT file.
>worker: A JavaScript web worker or shared worker.
>video: Video file, as typically used in <video>.

위의 타입들을 보다 보니 생각나는 것이 있다.

```javascript
<link rel="stylesheet" href="style.css">
<script src="main.js" defer></script>
```
그동안 무심결에 사용했던 위의 코드들도 전부 Pre Load 였구나 하는 생각이 든다.

## Lazy Loading
[MDN lazy Loading 문서 바로가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

`Lazy Loading`은 사용자의 행동이나 탐색 패턴에 기반해 유저가 필요할 때 일부 자원(이미지 같은)을 지연해서 로드하는 전략입니다. 통상적으로 이 자원들은 스크롤하여 발견될 때 로드된다.

제대로 구현된 경우에는 자원 지연 로딩은 사용자에게 끊김이 없다는 느낌, 페이지가 움직이기 시작할 때까지 필요한 자원 감소 등 초기 로드 성능 향상에 도움이 된다.

React에서 사용하는 방법 중 하나로 라이브러리가 있다.

[NPM React lazyload 라이브러리 바로가기](https://www.npmjs.com/package/react-lazy-load)

사용방법은 크게 어렵지 않다.

```javascript
import LazyLoad from 'react-lazy-load'; // 설치 후 임포트
 
const MyComponent = () => (
  <div>
    Scroll to load images.
    <div className="filler" />
    // LazyLoad 적용
    <LazyLoad height={762} offsetVertical={300}> 
      <img src='http://apod.nasa.gov/apod/image/1502/HDR_MVMQ20Feb2015ouellet1024.jpg' />
    </LazyLoad>
    <div className="filler" />
    <LazyLoad height={683} offsetTop={200}>
      <img src='http://apod.nasa.gov/apod/image/1502/2015_02_20_conj_bourque1024.jpg' />
    </LazyLoad>
    <div className="filler" />
    <LazyLoad height={480} offsetHorizontal={50}>
      <img src='http://apod.nasa.gov/apod/image/1502/MarsPlume_jaeschke_480.gif' />
    </LazyLoad>
    <div className="filler" />
    <LazyLoad
      height={720}
      onContentVisible={() => console.log('look ma I have been lazyloaded!')}
    >
      <img src='http://apod.nasa.gov/apod/image/1502/ToadSky_Lane_1080_annotated.jpg' />
    </LazyLoad>
    <div className="filler" />
  </div>
);
```






