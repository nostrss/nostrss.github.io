---
layout: post
title: "callback 과 promise(.. then)"
author: "Nostrss"
comments: true
tags: javascript callback promise then
excerpt_separator:
sticky:
hidden:
---



## callback
콜백에 관련한 설명은 이전에 작성한 글로 대신하도록 하겠다.
[callback 관련 이전 글 보기](https://nostrss.github.io/2022-04-20/75-js-callback)

이전 글에서 설명했듯이 콜백의 경우 너무 남발하게 될 경우 콜백지옥 또는 멸망의 피라미드에 빠지게 된다.

다시 한번 예시를 보자
```javascript
loadScript('1.js', function(error, script) {

  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('2.js', function(error, script) {
      if (error) {
        handleError(error);
      } else {
        // ...
        loadScript('3.js', function(error, script) {
          if (error) {
            handleError(error);
          } else {
            // 모든 스크립트가 로딩된 후, 실행 흐름이 이어집니다. (*)
          }
        });

      }
    })
  }
});
```
위와 같이 꼬리에 꼬리를 무는 동작이 많아지면 콜백 지옥에 빠지는 경우가 생기게 되는데 어쩔수 없이 비동기적인 동작이 많은 경우라서 위와 같이 코드를 짤 수 밖에 없는 상황이 온다면 어떻게 해야할까?

이럴때 사용할 수 있는것이 promise이다

## promise

기본적으로 promise는 함수에 콜백을 전달하는 대신에, 콜백을 첨부하는 방식의 객체라고 보면 된다.

콜백 함수를 전달해주는 고전적인 방식과는 달리, Promise는 아래와 같은 특징을 보장한다.

- 콜백은 자바스크립트 Event Loop가 현재 실행중인 콜 스택을 완료하기 이전에는 절대 호출되지 않습니다.
- 비동기 작업이 성공하거나 실패한 뒤에 then() 을 이용하여 추가한 콜백의 경우에도 위와 같습니다.
- then()을 여러번 사용하여 여러개의 콜백을 추가 할 수 있습니다. 그리고 각각의 콜백은 주어진 순서대로 하나 하나 실행되게 됩니다.


## 비교

콜백을 썼을 때와 promise를 사용했을때의 코드로 비교를 해보자

```javascript
const onClickCallback = () => {
    const aaa = new XMLHttpRequest();
    aaa.open('get', 'http://numbersapi.com/random?min=1&max=200');
    aaa.send();
    aaa.addEventListener('load', (res) => {
      const num = res.target.response.split(' ')[0]; // 랜덤숫자

      const bbb = new XMLHttpRequest();
      bbb.open('get', `http://koreanjson.com/posts${num}`);
      bbb.send();
      bbb.addEventListener('load', (res) => {
        const userId = res.target.response.UserId;

        const ccc = new XMLHttpRequest();
        ccc.open('get', `http://koreanjson.com/posts?userId=${userId}`);
        ccc.send();
        ccc.addEventListener('load', (res) => {
          console.log(res);
        });
      });
    });
  };

```

```javascript
const onClickPromise = () => {
    console.log('1번입니다');
    axios
      .get('http://numbersapi.com/random?min=1&max=200')
      .then((res) => {
        console.log('2번입니다');
        const num = res.data.split(' ')[0]; // 랜덤숫자
        return axios.get(`http://koreanjson.com/posts/${num}`);
      })
      .then((res) => {
        console.log('3번입니다');
        const userId = res.data.UserId;
        return axios.get(`http://koreanjson.com/posts?userId=${userId}`);
      })
      .then((res) => {
        console.log('4번입니다');
        console.log(res);
      });
    console.log('5번입니다');
  };

```

위의 2코드는 동일한 결과를 보여주는 코드이다. 위의 콜백을 이용한 코드는 점점 중첩된 구조로 들어가면서 곧 콜백 지옥에 빠질 수도 있을 것 같이 보인다.

하지만 propmise를 사용한 코드의 경우 then을 이용해 콜백을 추가하여 코드의 흐름이 보다 직관적인것을 알 수 있다.

