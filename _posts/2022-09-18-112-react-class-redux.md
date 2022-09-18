---
layout: post
title: '[React] 게시판 만들기 1일차'
author: 'Nostrss'
comments: true
tags: react class router redux firebase
excerpt_separator:
sticky:
hidden:
---

## 프로젝트의 목적

혼자서 공부할 겸 간단한 게시판 `CRUD` 기능을 가진 페이지를 만들어 보려고 한다.

이 프로젝트를 하는 학습 목적은 아래와 같다.

> - 리액트 Class형
> - Redux
> - react-router-dom

그동안 나는 `리액트 함수형`, 글로벌 스테이트는 `Recoil`, 라우팅은 `nextjs`를 이용해서 했었다.
그런데 회사에서는 이 기술들을 전혀 사용하지 않기 때문에 어쩔 수 없이 공부를 좀 해야겠다는 생각이 들었다..

타입스크립트는 제외하고 위의 3개만 빠르게 실습하면서 익혀보려고 한다.

### 페이지

- 글 리스트
- 글 상세

### 기능

- 글, 이미지 업로드
- 삭제
- 수정
- 읽기

### 백엔드

- Firebase를 써보려고 한다.

### 디자인

- CSS에 시간을 쓰고 싶지 않아서 기본 html 태그로만 만들 예정이다
- 참고 링크 : https://www.berkshirehathaway.com/

## react-router-dom 세팅

Next.js와 사용법이 사뭇 달라서 문서를 보면서 시행착오를 겪어가면서 세팅했다.

- https://reactrouter.com/en/main

### index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter basename={process.env.PUBLIC_URL}>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

1. `BrowserRouter`를 임포트 하고 App 컴포넌트로 감싸주면 된다.
2. `BrowserRouter`에 props로 `basename={process.env.PUBLIC_URL}`을 작성해줘야 한다.

- 이 props가 없으면 github-page에 배포시 경로를 찾지 못한다..

### index.js

```javascript
import './App.css';
import { Route, Routes } from 'react-router-dom';
import Home from './components/Home';

function App() {
  return (
    <Routes>
      <Route path='/' element={<Home />} />
    </Routes>
  );
}

export default App;
```

1. `Routes`, `Route`를 임포트 해준다

- 구글에서 검색하다 보면 `react-router-dom` 버전에 따라 사용법이 조금씩 달라서 시행착오가 있었다.
  > 현재 내가 사용하는 버전은 `"react-router-dom": "^6.4.0",`인데, 5.x.x 버전과 많이 달라졌다고 하니 주의가 필요하다.

2. `Routes`안에 `Route`를 배치해준다.

이렇게 세팅을 하면 첫화면에 `Home` 컴포넌트가 바로 보이게 된다.
