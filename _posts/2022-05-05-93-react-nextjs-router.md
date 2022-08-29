---
layout: post
title: "React Router vs Nextjs Router"
author: "Nostrss"
comments: true
tags: router react nextjs
excerpt_separator:
sticky:
hidden:
---

## React Router

React에서는 Router는  Routes안에 있는 Router 들 중에서 조건에 만족한 첫번째 Router를 불러와 실행한다.

```javascript
import React, { Suspense, lazy } from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);
```

### Next.js router 

```javascript
import { useRouter } from 'next/router'

export default function Page() {
  const router = useRouter()

  return (
    <button type="button" onClick={() => router.push('/post/abc')}>
      Click me
    </button>
  )
}
```

Next.js에서는 리액트의 그것보다 훨씬 사용하기가 쉬운 모습이다.
router.push('경로명')만 적어주면 해당주소로 라우팅이 된다.

또한 동적라우팅 역시 아주 쉽게 적용이 가능하다.

[Next.js 다이나믹 라우팅 바로가기](https://nextjs.org/docs/routing/dynamic-routes)

Next는 대괄호로 이루어진 경로 폴더에 [폴더명]으로 생성하고
그 주소로 router.push만 하면 중첩 라우팅 구조가 완성되어 훨씬 편하고 효율적이다.


