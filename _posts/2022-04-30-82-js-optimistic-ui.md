---
layout: post
title: " 컴퓨터의 착한 거짓말 Optimistic-UI "
author: "Nostrss"
comments: true
tags: javascript apollo graphql
excerpt_separator:
sticky:
hidden:
---

## Optimistic UI
[Apollo GraphQl 문서 보러 가기](https://www.apollographql.com/docs/react/v2/performance/optimistic-ui/)

아무리 인터넷과 컴퓨터가 빨라졌다고 하더라도 클라이언트와 서버의 통신에 물리적인 시간과 비용이 드는 것은 사실이다. 
0.001초의 간격이나 지연은 어쩔수가 없다. 하지만 세상 모든 곳의 통신망과 컴퓨터가 동일한 성능을 가지고 있는 것은 아니다.
그래서 마치 트릭과도 같은 기법을 이용하는 경우가 있다.

Optimistic UI 는 서버로부터 응답을 받기 전에 결과를 시뮬레이션하고 UI를 업데이트하는 데 사용할 수 있는 방법이다. 응답을 받기전에 클라이언트에 Optimistic 결과를 반영해두고 서버에서 응답을 받으면 Optimistic 결과는 버리고 실제 받아온 데이터의 결과로 대체한다.

그렇기 때문에 어느정도 높은 확률로 응답이 예상이 되는 경우에 적용하는 것이 바람직 하다고 볼 수 있다.

GraphQl에서는 mutation을 할 때 optimisticResponse 라는 옵션으로 이용할 수 있도록 하고 있다.

### 예시
```javascript
const [updateComment] = useMutation(UPDATE_COMMENT);
const onClickComment = () => {
  updateComment({
    variables: { commentId, commentContent },

    optimisticResponse: {
      updateComment: {
        id: commentId,
        __typename: "Comment",
        content: commentContent,
      },
    },
  });
};
```

### 테스트 방법
사실 우리나라처럼 인터넷이 발달한 나라에서는 크게 체감이 안될수도 있다.
이럴때 일부러 브라우저의 통신 속도를 낮춰서 테스트 해보는 방법이 있다.

[크롬브라우저 웹소켓 요청 쓰로틀링 바로가기 ](https://developer.chrome.com/ko/blog/new-in-devtools-99/#websocket)

위의 링크를 통해 구글 크롬 사이트에서 직접 확인 할 수 있다.
