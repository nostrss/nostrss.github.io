---
layout: post
title: '이것 좀 실행해줘 useEffect'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---

[useEffect 공식문서 바로가기](https://ko.reactjs.org/docs/hooks-effect.html)

## useEffect 개요
- `useEffect` Hook은 우리가 React에게 컴포넌트가 `렌더링` 이후에 어떤 일을 수행해야하는 지를 지정할 수 있다.
- 페이지가 렌더링 된 후 무조건 `1번`은 실행된다.
- `useEffect`의 배열에 담긴 `state`값이 변경되면 무조건 실행된다.

```javascript
const [count, setCount] = useState(0);

 useEffect(() => {

    inputRef.current?.focus();
    return () => {
    };
  }, [count]); 
```
위의 코드를 보면
만약 카운터 컴포넌트가 있다고 가정할때 count의 스테이트가 변할 때마다 useEffect가 실행된다.

### useEffect가 컴포넌트 안에 있는 이유
useEffect를 컴포넌트 내부에 둠으로써 effect를 통해 count state 변수(또는 그 어떤 prop에도)에 접근할 수 있게 됩니다. 
함수 범위 안에 존재하기 때문에 특별한 API 없이도 값을 얻을 수 있는 것입니다. 

### 렌더링 이후에 매번 수행되는 건가?
네, 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행됩니다.

### 클래스의 생명주기와의 비교
React의 `class 생명주기` 메서드에 친숙하다면, useEffect Hook을 `componentDidMount`와 `componentDidUpdate`, `componentWillUnmount`가 합쳐진 것으로 생각해도 좋다.

## (주의)useEffect 안에서 setState의 사용

컴포넌트가 마운트된 이후에 `setState`를 적용하게 되면,
1. state가 변경되고, 
2. 변경된 state로 컴포넌트가 다시그려지게(=리렌더)됩니다.

즉, useEffecrt 내에서 setState를 사용하게 되면 `불필요한 리렌더`나 `무한루프`를 일으키게 되고 성능면에서 비효율적이게 됩니다. 




