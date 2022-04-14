---
layout: post
title: '[코드캠프#12] 메모'
author: 'Nostrss'
comments: true
tags: memo codecamp
excerpt_separator:
sticky:
hidden:
---

useQuery : 요청과 렌더링 모두 자동이다.

useLazyQuery : 요청은 내가 원할때, 렌더링은 자동
- 최초 실행만 내가 원하는 곳에서 가능하고 그 이후에는 useQuery와 동일

useApolloClient : 요청도 수동, 렌더링도 수동 가능, axios로 생각하면 된다?

- 내가 원하는곳에서 query불러오기 가능(apolloclient에서 import)
자동으로 되지 않는다?

제어컴포넌트 : state에 저장해서 쓴다
비제어 컴포넌트 : react-hook-form은 비제어라 빠르다? 꼭 비제어가 더 좋은건 아니다


yup 커스터마이징?

```javascript
let schema = number().test(
  'is-42',
  "this isn't the number i want",
  (value) => value != 42,
);

schema.validateSync(23); 
```



