---
layout: post
title: '가끔은 스킵.. 디바운싱과 쓰로틀링'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---


## Debouncing
`디바운싱`이란, 연이어 발생한 이벤트를 하나의 그룹으로 묶어 처리하는 방식이다. 주로 그룹에서 마지막, 혹은 처음에 처리된 함수를 처리하는 방식으로 사용되는데 그 대표적인 예시가 `자동검색`이다.

구글이나 네이버에 `debouncing`이라는 단어를 검색을 하는 상황을 가정해보자

d
de
deb
debo
debou
deboun
debounc
debounci
debouncin
debouncing

우리는 총 10개의 텍스트를 입력한 후애 검색을 실행할 것이다.

그렇다면 10개의 텍스트를 입력하는 동안 자동검색이 실행이 될 필요가 있는가?

물론 필요할 수도 있지만, 회사입장에서는 제한된 리소스의 낭비가 발생하는 것으로 볼 수 있다.

왜냐하면 텍스트가 하나 하나 입력 될때 마다 서버와 통신이 발생하게 되고 이때 마다 비용이 발생하기 때문이다. 

그래서 이런 상황에 예를 들면 약 0.2초동안 입력이 없으면 텍스트입력이 끝난 것으로 간주하도록 처리하는 것이 Debouncing이다.


### Lodash를 활용한 Debounce 구현

`Lodash` 임포트
```javascript
import { debounce } from 'lodash';
```

0.5초마다 onChange함수 값을 불러오는 예시코드

```javascript
import { debounce } from 'lodash';
export default function Test2() {
  
	const handleOnChange = debounce((e) => {
		console.log(e.target.value);
	}, 500);

	return (
		<>
			<input onChange={handleOnChange}></input>
		</>
	);
}
```


## Throttling
`쓰로틀링`이란, 연이어 발생한 이벤트에 대해 일정한 `delay`를 포함 시켜, 연속적으로 발생하는 이벤트는 무시하는 방식을 말한다. 즉, 지정한 `delay`동안 호출된 함수는 무시한다.

대표적인 예로 스크롤이나 무한 스크롤이벤트가 있다.

스크롤의 경우에는 쉽게 생각하면 이벤트를 수신하는 감도를 떨어뜨린다고 생각하면 된다. 스크롤이 되는 동안 발생하는 모든 이벤트를 전부 수신하면 그 빈도가 너무 많기 때문에 그 감도를 줄이는 기법이라고 생각하면 된다.


