---
layout: post
title: 'Shallow-Routing : URL로 상태값 알아내기 '
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---


## Shallow Routing
[Shallow Routing Next.js 공식문서 바로가기](https://nextjs.org/docs/routing/shallow-routing)

### URL로 현재 상태를 알 수 있다?
- 예를 들어 `PageNumber=2`라는 `state` 값이 있다고 가정해보자. `props`로 다른 컴포넌트에 넘겨줄 일이 있을 수 있다. 이때 만약에 `URL`이 아래와 같다면 `props`가 아니라 `URL`을 통해서 `state`값을 얻을 수 있다.


>http://www.yes24.com/24/category/bestseller?CategoryNumber=001&sumgb=06&fetchSize=40&PageNumber=2

물론 중요한 값들은 URL로 보여주면 안되겠지만 사소한 값들은 이렇게 URL로 보여줘도 되는데, 이럴때 유용하게 사용할 수 있는 것이 `Shallow Routing`이다.

예시
```javascript
import { useEffect } from 'react'
import { useRouter } from 'next/router'

// Current URL is '/'
function Page() {
  const router = useRouter()

  useEffect(() => {
    // Always do navigations after the first render
    router.push('/?counter=10', undefined, { shallow: true })
  }, [])

  useEffect(() => {
    // The counter changed!
  }, [router.query.counter])
}

export default Page
```
즉, setState를 해야할때 부모 컴포넌트에서 setState를 자식 컴포넌트의 prop으로 넘겨주는 방식이 아니라 그냥 어느 컴포넌트든지 `router.push + shallow : true` 로 url만 바꿔주면 알아서 `setState`한 것과 동일한 효과로 전부 리랜더링을 시킬 수 있게 되는거다.
