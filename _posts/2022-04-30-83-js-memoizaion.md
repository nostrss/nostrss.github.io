---
layout: post
title: " 왜 전부다 리렌더링해? 난 메모해 "
author: "Nostrss"
comments: true
tags: javascript apollo graphql
excerpt_separator:
sticky:
hidden:
---

## Memoization
메모이제이션은 특정 연산이나 특정 함수의 값을 기억해 놓은 후 State의 변화로 화면이 리렌더 되더라도 함수가 초기화 되지 않고,
기존에 저장된 값을 그대로 사용할 수 있게한다.

메모이제이션 기능을 사용하면 컴포넌트의 불필요한 리렌더링을 줄여 최적화 할 수 있어서 성능 향상을 기대할 수 있게 된다.

### Memoization의 종류
- memo[React 공식 문서 보러가기](https://ko.reactjs.org/docs/react-api.html#reactmemo)
- useMemo[React 공식 문서 보러가기](https://ko.reactjs.org/docs/hooks-reference.html#usememo)


### Memo

사용방법
```javascript
const MyComponent = React.memo(function MyComponent(props) {
  /* props를 사용하여 렌더링 */
});
```
React.memo는 고차 컴포넌트(Higher Order Component)입니다.

컴포넌트가 동일한 props로 동일한 결과를 렌더링해낸다면, React.memo를 호출하고 결과를 메모이징(Memoizing)하도록 래핑하여 경우에 따라 성능 향상을 누릴 수 있습니다. 
>즉, React는 컴포넌트를 렌더링하지 않고 마지막으로 렌더링된 결과를 재사용합니다.

React.memo는 props 변화에만 영향을 줍니다. React.memo로 감싸진 함수 컴포넌트 구현에 useState, useReducer 또는 useContext 훅을 사용한다면, 여전히 state나 context가 변할 때 다시 렌더링됩니다.

#### Memo 주의사항
이 메서드는 오직 성능 최적화를 위하여 사용됩니다. 렌더링을 “방지”하기 위하여 사용하지 마세요. 버그를 만들 수 있습니다.


### useMemo
useEffect처럼 의존성 배열배열을 사용한하며 메모이제이션된 값을 반환합니다.

예시
```javascript
const aaa = useMemo(() => Math.random(), []);
```
위의 코드를 사용하면 리렌더가 되더라도 랜덤 숫자가 변하지 않는 것을 확인 할 수 있다.



“생성(create)” 함수와 그것의 의존성 값의 배열을 전달하세요. useMemo는 의존성이 변경되었을 때에만 메모이제이션된 값만 다시 계산 할 것입니다. 이 최적화는 모든 렌더링 시의 고비용 계산을 방지하게 해 줍니다.

useMemo로 전달된 함수는 렌더링 중에 실행된다는 것을 기억하세요. 통상적으로 렌더링 중에는 하지 않는 것을 이 함수 내에서 하지 마세요. 예를 들어, 사이드 이펙트(side effects)는 useEffect에서 하는 일이지 useMemo에서 하는 일이 아닙니다.

배열이 없는 경우 매 렌더링 때마다 새 값을 계산하게 될 것입니다.

