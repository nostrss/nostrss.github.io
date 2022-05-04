---
layout: post
title: "timeago 쉽게 구현하기"
author: "Nostrss"
comments: true
tags: library timeago
excerpt_separator:
sticky:
hidden:
---

## timeago.js 라이브러리

카카오톡 메시지나 페이스북 게시물에 보면 타임스탬프가 단순 날짜가 아닌 경우가 많다. 

>방금 전 게시 되었습니다.

>1시간 전에 보낸 메시지

이렇게 다양한 경우의 수로 타임스탬프가 표현되는 경우가 있다. 
테스트때 구현사항으로 있어서 하나 하나 구현하기 귀찮아 찾아봤는데
편하게 구현하는 라이브러리가 있어서 사용해봤다.

(timeago 라이브러리 바로가기)[https://www.npmjs.com/package/timeago-react]

라이브러리 용량도 매우 작고 사용법도 쉬워서 적용하기가 매우 쉬웠다.

설치는 위의 링크를 통해 설치하면 되고 사용법은 아래와 같다.

>컨테이너 함수영역

```javascript
const locale = function (number, index, totalSec) {
  // number: the timeago / timein number;
  // index: the index of array below;
  // totalSec: total seconds between date to be formatted and today's date;
    
    return [
      ['방금 전', 'right now'],
      ['%s초 전', 'in %s seconds'],
      ['1분 전', 'in 1 minute'],
      ['%s분 전', 'in %s minutes'],
      ['1시간 전', 'in 1 hour'],
      ['%s시간 전', 'in %s hours'],
      ['어제', 'in 1 day'],
      ['%s일 전', 'in %s days'],
      ['1주일 전', 'in 1 week'],
      ['%s주일 전', 'in %s weeks'],
      ['1달 전', 'in 1 month'],
      ['%s달 전', 'in %s months'],
      ['1년 전', 'in 1 year'],
      ['%s년 전', 'in %s years'],
    ][index];
  };

  timeago.register('kr', locale);
```


>프리젠터 영역
```javascript
  <TimeAgo datetime={props.el?.createdAt} locale='kr' />
 ```

 위와 같이 작성하면 아래와 같이 시간이 자동으로 변환되어 표기 된다.

 ![image with caption](/assets/image/timeago1.png 'timeago 예제1')
 ![image with caption](/assets/image/timeago2.png 'timeago 예제2')
 ![image with caption](/assets/image/timeago3.png 'timeago 예제3')
 ![image with caption](/assets/image/timeago4.png 'timeago 예제4')

다양한 옵션들도 많이 있는데 추후에 사용해봐야 할 듯 싶다.

